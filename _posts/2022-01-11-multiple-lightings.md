---
layout: post
title: "Multiple Lightings"
date: 2021-01-10
excerpt: "Directional light, point light, spot light"
tags: [OpenGL, C++]
comments: true
pagetype: 3
figure: multiple-lightings.png
---

# Directional light

{% capture images %}
	https://user-images.githubusercontent.com/49530505/152238467-faf40da2-b277-4c53-a440-68d8249d74fa.png
{% endcapture %}
{% include gallery images=images caption="photos of directional light" cols=2 %}

### Calculate light direction

We can just define a light direction in Light class

{% highlight c %}
    struct Light {
        vec3 direction;
        ...
    };
    ...
    void main()
    {
      vec3 lightDir = normalize(-light.direction);
      ...
    }
{% endhighlight %}

<div markdown="0"><a href="https://github.com/MuruC/OpenGL-Practice" class="btn btn-info">Download codes</a></div>