---
layout: post
title: "Multiple Lightings"
date: 2021-01-11
excerpt: "OpenGL + Lua + C++"
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

## Calculate light direction

We can just define a light direction in Light class

{% highlight html %}
<a href="#" class="btn btn-success">Success Button</a>
{% endhighlight %}

# Point Light

{% capture images %}
	https://user-images.githubusercontent.com/49530505/152234750-01b041a9-974a-4a53-96f0-4a47cae95248.png
{% endcapture %}
{% include gallery images=images caption="photos of point light" cols=2 %}

## Implementing Attenuation

# Main Principles and processes

## Orthographic camera

Make a orthographic camera that can be zoomed by mouse;

## Click mouse to create particles

Get the position of mouse. Transform the rectangle and pass the matrix position to vertex shader. 

## Object-oriented programming

Create a particle class that includes particle.emit(), particle.render(), particle.update() and some particle properties.

Create a particle pool that contains 1000 particles. Every time when the user create particle, the particle set active from the pool. When the particle's lifetime is less 0, the particle is set to inactive.

[Download codes](https://github.com/MuruC/ParticleSystem){: .btn}