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

# Point Light

{% capture images %}
	https://user-images.githubusercontent.com/49530505/152234750-01b041a9-974a-4a53-96f0-4a47cae95248.png
{% endcapture %}
{% include gallery images=images caption="photos of point light" cols=2 %}

### Calculate Attenuation

reduce the intensity of light over the distance a light ray travels 

{% capture images %}
	https://user-images.githubusercontent.com/49530505/152254949-9df77e6f-f310-4a01-a7bb-8ca4b0e1fed2.png
{% endcapture %}
{% include gallery images=images caption="attenuation" cols=2 %}

{% highlight c %}
    struct Light {
        float constant;
        float linear;
        float quadratic;
        ...
    };
    ...
    void main()
    {
        float distance    = length(light.position - FragPos);
        loat attenuation = 1.0 / (light.constant + light.linear * distance + 
                light.quadratic * (distance * distance));
        ...
    }
{% endhighlight %}

<div markdown="0"><a href="https://github.com/MuruC/OpenGL-Practice" class="btn btn-info">Download codes</a></div>