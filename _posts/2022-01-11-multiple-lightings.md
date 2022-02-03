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

### Apply Attenuation

we include this attenuation value in the lighting calculations by multiplying the attenuation value with the ambient, diffuse and specular colors.

{% highlight c %}
    void main()
    {
        ambient  *= attenuation; 
        diffuse  *= attenuation;
        specular *= attenuation;
        ...
    }
{% endhighlight %}

# Spot Light

We need: the spotlight's position vector (to calculate the fragment-to-light's direction vector), the spotlight's direction vector and the cutoff angle.

{% capture images %}
	https://user-images.githubusercontent.com/49530505/152256078-2a3dc7ea-18ac-4868-8244-26c90f35dd79.png
{% endcapture %}
{% include gallery images=images caption="attenuation" cols=2 %}

### Caculate Angles

{: .center}
![image](https://user-images.githubusercontent.com/49530505/152256935-622da7a4-fbaf-4041-83bf-12e0c1b1c8dc.png "angles")
{% capture images %}
{% endcapture %}

We pass the cosine value because it is easier to compare

{% highlight c %}
    struct Light {
        vec3  position;
        vec3  direction;
        float cutOff;
        ...
    };  
{% endhighlight %}

{% highlight c %}
    lightingShader.setFloat("light.cutOff",   glm::cos(glm::radians(12.5f)));
{% highlight c %}

calculate the theta θ value and compare this with the cutoff ϕ value to determine if we're in or outside the spotlight:

if cosθ > cutOff, we can know that θ < ϕ

{% highlight c %}
    float theta = dot(lightDir, normalize(-light.direction));
    
    if(theta > light.cutOff) 
    {       
      // do lighting calculations
    }
    else  // else, use ambient light
      color = vec4(light.ambient * vec3(texture(material.diffuse, TexCoords)), 1.0);
{% endhighlight %}

### Smooth Edges

Set γ as outer cone angle value

intensity = (θ−γ) / (ϕ−γ)

{% highlight c %}
    float theta     = dot(lightDir, normalize(-light.direction));
    float epsilon   = light.cutOff - light.outerCutOff;
    float intensity = clamp((theta - light.outerCutOff) / epsilon, 0.0, 1.0);    
    ...
    // we'll leave ambient unaffected so we always have a little light.
    diffuse  *= intensity;
    specular *= intensity;
    ...
{% endhighlight %}

We use clamp to restrain the intensity in [0, 1]

<div markdown="0"><a href="https://github.com/MuruC/OpenGL-Practice" class="btn btn-info">Download codes</a></div>