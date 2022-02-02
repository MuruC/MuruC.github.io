---
layout: post
title: "2D Particle System"
date: 2021-01-10
excerpt: "OpenGL + Lua + C++"
tags: [OpenGL, C++]
comments: true
pagetype: 3
figure: 2d-particle-system-figure.png
---

## Demo
<iframe width="560" height="315" src="https://www.youtube.com/embed/J-SP_gg1kiw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Main Principles and processes

## Orthographic camera

Make a orthographic camera that can be zoomed by mouse;

## Click mouse to create particles

Get the position of mouse. Transform the rectangle and pass the matrix position to vertex shader. 

## Object-oriented programming

Create a particle class that includes particle.emit(), particle.render(), particle.update() and some particle properties.

Create a particle pool that contains 1000 particles. Every time when the user create particle, the particle set active from the pool. When the particle's lifetime is less 0, the particle is set to inactive.

[Download codes](https://github.com/MuruC/ParticleSystem){: .btn}