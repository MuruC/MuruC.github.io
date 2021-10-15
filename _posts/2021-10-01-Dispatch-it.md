---
layout: post
title: "Dispatch It!"
date: 2021-09-22
excerpt: "AR narrative game on Hololens"
tags: [game, AR]
comments: true
game: true
pagetype: 1
figure: telephone_figure.png

---

## Demo
<iframe width="560" height="315" src="https://www.youtube.com/embed/lsWpTOg26Pc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Collaborated with programmer Jingyu Zhuang, artist Dannis Wang, artist Nolan Pearson, sound designer Weilin Yuan.


## Made narrtive system for other programmer and designer to add story nodes.
<p>· Using custom class, structure and linked list to build narrative system. The designer and other programmer can add, remove, change or search story nodes easily with this system</p>

<pre>
<code>
    using DictOptionNodes = Dictionary<phonePlugInEnum, Node>;
    public enum phonePlugInEnum { hospital, police, fireStation, conversation, ring, ending }
    class Node
    {
        public Node(float clipLength, string clipName, int score, AudioSource myAudioSource)
        {
            ClipLength = clipLength;
            ClipName = clipName;
            Score = score;
            audioSource = myAudioSource;
            OptionNodes = new DictOptionNodes();
        }

        public Node addOption(phonePlugInEnum option, Node node)
        {
            OptionNodes[option] = node;
            return this;
        }

        public Node addOption(phonePlugInEnum option, float clipLength, string clipName, int score, AudioSource myAs)
        {
            OptionNodes[option] = new Node(clipLength, clipName, score, myAs);
            return this;
        }

        public Node getOption(params phonePlugInEnum[] options)
        {
            Node result = null;
            DictOptionNodes currentOptionNodes = OptionNodes;
            foreach (var option in options)
            {
                Debug.Log(option);
                if(!currentOptionNodes.ContainsKey(option))
                {
                    Debug.Log("Can't find option " + option.ToString() + " for current node.");
                    break;
                }

                result = currentOptionNodes[option];
                currentOptionNodes = result.OptionNodes;
            }
            return result;
        }

        public void PlayAudio()
        {
            SoundMgr.Instance.PlayDialogue(ClipName);
        }

        public float ClipLength { get; set; }
        public string ClipName { get; set; }
        public int Score { get; set;  }
        public AudioSource audioSource { get; set; }
        public DictOptionNodes OptionNodes { get; set; }
    }
</code>
</pre>

## Wrote and refine. the main structure of the game, improving team's working efficiency.
<p>· Made a Time Manager to replace coroutine. The Time Manager includes unloop delayed event interface and loop real time event interface.</p>
<p>· Made public enumeration and dictionary. So that other programmer and designer didn't need to memorize the plug index;</p>
<p>· Made Sound Manager with overriden interfaces.</p>

<pre>
<code>
namespace TimeNameSpace {
    public delegate void Delegate1();
    public class Event
    {
        public Event(float startTime, float gapTime, bool isLoop, Delegate1 handler)
        {
            StartTime = startTime;
            GapTime = gapTime;
            IsLoop = isLoop;
            Handler = handler;
        }
        public float StartTime {get;set;}
        public float GapTime { get; set; }
        public bool IsLoop { get; set; }
        public Delegate1 Handler { get; set; }
    }
    public class TimeMgr : MonoBehaviour
    {
        public static TimeMgr Instance = null;
        List<Event> allEventList = new List<Event>();
        List<Event> activeEventList = new List<Event>();
        private float curTime = 0f;
        private void Awake()
        {
            if (Instance != null && Instance != this)
            {
                Destroy(this.gameObject);
            }
            else
            {
                Instance = this;
            }
        }
        // Start is called before the first frame update
        void Start()
        {

        }

        // Update is called once per frame
        void Update()
        {
            curTime += Time.deltaTime;
            for (int i = allEventList.Count - 1; i >= 0; i--)
            {
                Event timeEvent = allEventList[i];
                if (timeEvent.StartTime + timeEvent.GapTime <= curTime)
                {
                    activeEventList.Add(timeEvent);
                    if (timeEvent.IsLoop)
                    {
                        timeEvent.StartTime = curTime;
                    }
                    else
                    {
                        allEventList.Remove(timeEvent);
                    }
                }
            }
            for (int i = activeEventList.Count - 1; i >= 0; i--)
            {
                Event activeEvent = activeEventList[i];
                activeEvent.Handler();
                activeEventList.Remove(activeEvent);
            }
        }

        public void AddDelayEvent(float gapTime, Delegate1 handler)
        {
            Event newEvent = new Event(curTime, gapTime, false,handler);
            allEventList.Add(newEvent);
        }

        public void AddRtEvent(float startTime, float delayTime, Delegate1 handler)
        {
            Event newEvent = new Event(startTime, delayTime, true, handler);
            allEventList.Add(newEvent);
        }

    }
</code>
</pre>