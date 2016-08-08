---
layout: post
title: Responsive Layout
---

**Responsive Layout**

Taking a look at some of the projects that I’ve built with Rails and Sinatra, I’m thinking not only about how I can improve the functionality of the projects, but also about how I can improve the site’s accessibility, and ease of navigating on different devices. Color scheme, typography, and layout are all essential things to consider when creating a website, but we must also think about who our users are and what kind of devices they might be viewing our application from. Technology changes rather exponentially, and there is now such a wide variety of devices on which we can surf the web--everything from small cell phone screens to large televisions.

As a web application developer, we must ensure that our application is accessible to a wide variety of users, and therefore available on different kinds of devices. So far, I have designed my applications for the web, but there are some other concepts to consider when designing a website for a tablet or mobile device, for example. I have recently put these concepts to practice when I put to the task of designing a website related to something that interested me.

I’ve always been interested in how animations are created, and so I thought it would be cool to do some research on how animated films are produced, and create a website on my findings. I utilized HTML, CSS, and JavaScript to design the desktop-based version of my website, but I found that designing a website for mobile and print involved a little more tweaking. I had to create a separate mobile and css file, and make my modifications to those. We can use media queries to specify what the design should look like in response to the size of the device.

This is what part of my mobile.css looks like: 

```
@media only screen and (max-device-width: 480px) {

    #menu{
      display: none;
    }

    #header{
      width: 25%;
      height: 20%;
    }

    #border{
      position: absolute;
    }

    #social, #result, img, #craft, #riding{
      display: none;
}

```

As shown in the CSS, we have to specify the media device and the maximum width of the device. We can also specify other aspects of the device such as orientation, resolution, device height, and color index. Other media types that we can design for include print, tv, and handheld.

I included a print css for my website as well, specifying styles for when the user prints any page. 

This is what part of my print CSS file looks like:  

```
@media print {
   #menu{
    display: none;
   }

   @page {
    margin: 0.5cm;
  }

  p{
    font-size: 12pt;
    font-family: 'Times New Roman';
    color: black;
  }

  #about h3, #goals h3, #vision h3, #welcome, .border h1{
    font-size: 24pt;
    font-family: 'Times New Roman';
    color: black;
  }


}
```

I did face some challenges as I created these CSS files. For example, the design would appear just as expected on some mobile devices, but not others. In this case, I had work with the CSS a little bit to find margins and paddings that would work well with all devices. Overall, we can use CSS to specify what we want our page to look like on various devices, and this can be done with the @media keyword. It is important to be able to scale our web app so that users can view them from a variety of devices.
