---
layout: post
title: "Skeleton Dance"
date: 2018-5-18
excerpt: "Group project: Kinect interface of skeleton dancing"
tags: [Kinect]
comments: true
pagetype: 2
figure: skeleton-figure.png
---

[Download the project](https://drive.google.com/open?id=1ZAj88YSsOCMvV9y4Eg7MRwlIMW3OvCCq){: .btn}


{: .center}
![image](https://user-images.githubusercontent.com/49530505/69126280-d1627a00-0ae2-11ea-91b0-972c0fb3e0de.jpg "skeleton dance")
<span class="caption">skeleton graphs credit to https://www.vectorstock.com/royalty-free-vector/dancing-skeleton-vector-760713"</span>

Skeleton Dance is a kinetic interface project. The skeleton on
the screen moved as the player moved. Each part of bones was
connected by string. If players shake their body drastically, the
skeleton might disintegrate, and bones would be swing like Yo-
Yo ball. When two parts got closer, they would restore and be
attached. I did visual design and coding with my partner.

I did graphic deign and coding with Zeping Fei together.

## Ideation

[Proposal](https://docs.google.com/presentation/d/1KYaRkwOhlOOw9rBHRRL0gIvxctvYfwWooAT7egtpD9Q/edit#slide=id.p)

After the idea presentation, we thought that only taking apart the body was not enough. So we decided to add more effect like the user could pick up the bones and put it back on the body.

During the process, we found that the user would need to squat down on the ground to attract and pick up the bones, and that would be very uncomfortable. Then we added a “wire” to dragged the bones like “yoyo”. It made the project much fun.

## Demo

<iframe src="http://s3-ap-southeast-1.amazonaws.com/ima-wp/wp-content/uploads/sites/5/2018/05/12151356/7368a82fea55ba40a30e9d997026da17.mp4?_=2"   
width="100%" height="412" frameborder="0" ></iframe>

{% capture images %}
https://user-images.githubusercontent.com/49530505/69126178-89435780-0ae2-11ea-8380-e78981249faa.jpg
https://user-images.githubusercontent.com/49530505/69126180-89dbee00-0ae2-11ea-9a87-612cd12bf811.jpg
{% endcapture %}
{% include gallery images=images caption="exhibition photos" cols=2 %}



## Techical development

At first we did not use object to store all the values, so the code was just messy

And then we set up a class to store objects, which contained each image’ s speed, position, acceleration and other values.

Some image might have special adjustment on  a certain value, so we used string “name” value. For example, if one object’ s “name” value is “head”, and then adjustentX = 10 (the image up 10).

Also another very important development is we defined our own “frameCount”. We added this number because when the kinect first detects the body, it considers that skeleton’ s position has changed greatly at that instance. So the whole body would be taken apart when the kinect detect the body immediately.

For whether the body part is apart, we added an boolean “isDetached”. We found this boolean is super useful, almost all the functions would use it, especially the attraction event.

### Special thanks to Prof. Moon!!



