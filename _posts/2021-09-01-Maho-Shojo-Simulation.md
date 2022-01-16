---
layout: post
title: "Maho Shojo Simulation"
date: 2021-09-06
tags: [game, VR]
comments: true
game: true
pagetype: 1
figure: maho_figure.png
excerpt_separator: <!--more-->
---
VR hand tracker game on Steam Vive

<b>Role:</b> Programmer and designer

<b>Platform:</b> C# + Unity + Steam Vive + VR
<!--more-->

## Demo
<iframe width="560" height="315" src="https://www.youtube.com/embed/k_CLwO1Jkfg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Collaborated with programmer and designer Huijie Bao, artist Sandra Liu, artist Wenbo Guo, sound designer Yu'an Tan.


## Made a Monster Manager for designer to add custom monsters.
<p>· Used custom struct. So that designer can configure custom monster easily.</p>
{: .center}
![image](https://user-images.githubusercontent.com/49530505/137388268-6972eea4-f365-48b1-bc9d-82f294b83c74.png "Inspector")
<span class="caption">screenshot of Inspector</span>

## Quick Time Event system.
<p>· An easily used QTE system. Other programer can add a new QTE event by on interface. This system contains trigger event, condition, success event, fail event, qte time, etc.</p>

<pre>
<code>
namespace QuickTimeEventNamespace {
    public enum QuickTimeEventState { run, success, fail, start }
    public class QuickTimeEvent
    {
        public QuickTimeEvent(float timeInterval_, Action OnTriggerEvent_, Action SucceedEvent_, Action FailureEvent_, Func<bool> PassCondition_, bool bContinuous_, Action OnUpdateEvent_)
        {
            timeInterval = timeInterval_;
            OnTriggerEvent = OnTriggerEvent_;
            SucceedEvent = SucceedEvent_;
            FailureEvent = FailureEvent_;
            PassCondition = PassCondition_;
            bContinuous = bContinuous_;
            OnUpdateEvent = OnUpdateEvent_;
        }
        public float timeInterval { get; set; }
        public Action OnTriggerEvent { get; set; }
        public Action SucceedEvent { get; set; }
        public Action FailureEvent { get; set; }
        public Func<bool> PassCondition { get; set; }
        public bool bContinuous { get; set; }
        public Action OnUpdateEvent { get; set; }

        public QuickTimeEventState state = QuickTimeEventState.start;

        public void Update()
        {
            if (state != QuickTimeEventState.run)
            {
                return;
            }
            bool result = PassCondition();
            if (OnUpdateEvent != null)
            {
                OnUpdateEvent();
            }            
            if (result)
            {
                Debug.Log("qte success! play success event!");
                SucceedEvent();
                state = QuickTimeEventState.success;
                QTEMgr.Instance.ContinueQTE();
            }
        }

        public void StartQTE()
        {
            //Debug.Log("Start QTE!!!");
            OnTriggerEvent();
            state = QuickTimeEventState.run;
            TimeMgr.Instance.AddDelayEvent(timeInterval, QTEFail);
        }

        public void QTEFail()
        {
            Debug.Log("state: " + state);
            if (state != QuickTimeEventState.run)
            {
                return;
            }
            FailureEvent();
            state = QuickTimeEventState.fail;
            QTEMgr.Instance.ContinueQTE();
        }
    }


    public class QTEMgr : MonoBehaviour
    {
        public static QTEMgr Instance = null;
        public float QTEInterval;
        private int currentQTEIndex = 0;
        private List<QuickTimeEvent> QTEQueue = new List<QuickTimeEvent>();
        private QuickTimeEvent currentQTE;

        // --------------------------example-------------------------------
        private int currentNum;
        public TMP_Text baseValueText;
        public GameObject successText;
        public GameObject failureText;
        private int userInput = -99;
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
            if (currentQTE == null)
            {
                return;
            }
            currentQTE.Update();
        }

        public void AddNewQTE(float timeInterval_, Action OnTriggerEvent_, Action SucceedEvent_, Action FailureEvent_, Func<bool> PassCondition_, bool bContinuous_, Action OnUpdateEvent_)
        {
            QTEQueue.Add(new QuickTimeEvent(timeInterval_, OnTriggerEvent_, SucceedEvent_, FailureEvent_, PassCondition_, bContinuous_, OnUpdateEvent_));
        }

        public void StartNewQTE()
        {
            currentQTE = QTEQueue[currentQTEIndex];
            currentQTE.StartQTE();
        }

        public void ContinueQTE()
        {
            currentQTE = null;
            currentQTEIndex++;
            if (currentQTEIndex >= QTEQueue.Count)
            {
                return;
            }
            QuickTimeEvent nextQTE = QTEQueue[currentQTEIndex];
            if (!nextQTE.bContinuous)
            {
                return;
            }
            TimeMgr.Instance.AddDelayEvent(QTEInterval, StartNewQTE);
        }
</code>
</pre>

## Main Gameplay