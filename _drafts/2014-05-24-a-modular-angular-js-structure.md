---
layout : post
title  : A Conversation Between an Web Guru, A Java Master, and an Intern
snip   : How to structure AngularJS Projects
---

>*This is a hypothetical conversation between a Web Guru, a Java Master, and an Intern. This conversation is basically what I've realized as my current project moves into development iteration 3, and is a culmination of a response to a comment that basically eluded how obnoxious it was that javascript code libraries like Angular have evolved into what is beginning look like server code, and weeks of failing Jasmine tests and conversations with coworkers and on IRC. TL;DR - It is becoming server code.*

_\*Intern (It) enters Web Guru's (Gu) office\*_

*It* : My code keeps failing Unit Tests! AHH!! \*An exasperated look falls upon _IT_'s face\*

*Gu* : Woah, slow down champ. Let's talk it over. What's exactly failing?

*It* : We've added the capability of unit testing on Jasmine, but I can't get it to work since any spec I write fails on Jquery selections. The DOM isn't present in our testing framework so any method call on a selection raises a type error since the selection itself is undefined.

*Gu* : Hm... so is this code in your controller or directive?

*It* : This is mostly everywhere throughout my code.

_*Java Master enters after returning from coffee and begins web surfing rituals\*_

*Gu* : Well, it sort of is right in front of you. Maybe you shouldn't have Jquery code in your controllers. Controllers in MVC frameworks typically handle data manipulation. Not DOM manipulation.

*It* : What? I've never really heard of this. What do you mean by data manipulation and DOM manipulation?

*Gu* : Models are your data, and controllers talk to data to manipulate them. But AngularJS has a great dependency injection feature. Because of this, they should never tell data how to do, but tell data what to do. If you follow this, you'll abstract your data out to services and put the behaviors there.

*It* : That kinda makes sense. We do this with http calls and other built in services. So you're saying abstract all models to the service? What do I gain from this?

*Gu* : Yes. So here's the basic example. You're working for a client and you're in the early development phase. You have some requirement from the client that a button needs to be on the page that will alert text when you click it. You code up a controller for some piece of the code and it looks like this...

<iframe width="100%" height="300" src="http://jsfiddle.net/jrab227/S6vRY/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>



*Gu* : Can you identify what's wrong with it?

*It* : Well, besides it being against what you said, I don't see.

*Gu* : Indeed, but do you see how the controller is __very tightly__ coupled to the model, or data? 

_\*It nods\*_

*Gu* : Now I want you to think of this as if you live in the _real world_. Obviously project managers change their minds. How would you write a controller to do a different behavior but use the same data?

_\*It code fiddles this...\*_

<iframe width="100%" height="300" src="http://jsfiddle.net/jrab227/3w2Uh/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>



_Master (Ma)_ : Gosh that's terrible. So you plan on just hitting copy paste every time a new requirement comes in? Your code will look this this...

<iframe width="100%" height="300" src="http://jsfiddle.net/jrab227/6cU8L/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>



_It_ : What's a better way?

_Gu_ : Well obviously dependency injection. Its mentioned in the [AngularJS Docs](https://docs.angularjs.org/guide/di).

_It_ : Wow I've never even seen this style. I've only read the tutorial.

_Gu_ : Indeed. Even in their tutorial [here](https://docs.angularjs.org/tutorial/step_02) they break this style. Mainly it is a small example and they do push this out to an http request. But at some point you'll want to have data and behaviors. Classes if you will.

_It_ : Gah this is so mindbending. Why is this in the tutorial? Now I have to go back and rethink my entire life!

_\*Gu and Ma start laughing\*_

_Ma_ : Mostly because front end engineering is an emergent field. To be bluntly honest, your job lifespans on a project are less than one year.

_Gu_ : Yup. We're actually are starting to split between designers who strictly work in css and html, but the tools to properly build the middleware are just being developed.

_Ma_ : And you really start being able to realize the proper data model after iteration 3, which takes a professional coder a year to get out of project managers and their bosses. By that time you've written a bad prototype and a second bad refactoring and you've pissed of your project manager who thinks button clicking should be easy. Then you're fired for a new guy who claims to do it better. 

_It_ : Wow. Guess I should have picked finance. So I'm sort of a pioneer?

_\*Gu and Ma burst out laughing\*_

_Ma_ : You'll need a few more years. But, seriously. Back to topic. Before your time, people would have built applications for desktop only. Maybe something in a .jar file.

_It_ : Yuck. The last .jar file I touched was Minecraft.

_Ma_ : Exactly. So we had megolith software houses. And we had MVC sort of. We had access strictly to the clients hard-drive. We'd create, save, modify data on the hardware. There were logic guys that would write the program itself. Then maybe some front-end guys to develop the buttons and fonts. Mind you there would be about a hundred of these guys. Like all a guy would do is work on styling a set of buttons. Then there were deployment and QA engineers. They would arrange pulling all the changes, making sure things don't break when the application is running, and fixing things. All this and there would still be bugs. They developed testing, but now we have the internet. 

_Gu_ : Why do you think windows is such a bad platform?

_It_ : This is true. Kinda stuff that was going on when I was a kid.

_Ma_ : Yup. So now laptops and cellphones are around. Now we have apps. So what's interesting is before apps, websites were always only done once, then completely redone or never redone at all after a year or so. But Facebook, Google, and other companies are having lifespans beyond the developers lifespan. Are they going to re-write their entire middleware every year? No. You probably can guess that the development of Angular coming out of Google's house was necessary since they must write modular frameworks. Things that can change easily, and be tested easily. Check this out.

<script type="text/javascript" src="//www.google.com/trends/embed.js?hl=en-US&q=javascript+unit+testing&content=1&cid=TIMESERIES_GRAPH_0&export=5&w=900&h=330"></script>
<script type="text/javascript" src="//www.google.com/trends/embed.js?hl=en-US&q=unit+testing&content=1&cid=TIMESERIES_GRAPH_0&export=5&w=900&h=330"></script>

_Ma_ : We're actually seeing javascript evolve into mature code before our eyes since people can't re-write an entire web application. And these web applications are becoming seriously long term projects. Facebook.

_Gu_ : Welcome to a new world of application coding!

_It_ : Jeez. So going back to the code, how should I decouple my application into true model-view-controller? In your application you still sort of copied controllers.

_Gu_ : This is true. Let's really write something. Observe how my data is now completely in services, and this time I'll only use a single controller. Now for that case, my user story changed but really I used the same html template. So we'll put this "view" knowledge into directives. Model in services, view in directives, controller in well... controller. 

<iframe width="100%" height="300" src="http://jsfiddle.net/jrab227/azvKH/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

_It_ : Wow this is beautiful. Its easy to see where everything is and I can just depend it into my main module.

_Gu_ : Yup. And you can test it. If you thought about your model before hand, you can see all the controller is in this case is a data manager that combines two versions of data and a behavior. Your view can then look this up. Your controller is indeed a link between your view and your data. And you can test the behaviors in the service, and the controller that its just linking what its given. You could even test your controller if you want.

_Ma_ : Its actually a module at this point. You can submit this Angular module into our code straight up. Along with a test spec of course. Then if it builds using our integration tester and passes, it goes straight into the master.

_It_ : This is very much like old server and application coding. But there's some problems with those code bases too. Obviously this isn't the answer to everything. Right?

_Gu_ : Indeed. There's a big problem with applications talking to each other. Right now they have to agree on an API. Also in this example you still don't have controller to controller talking. But you can take this model and kill about 80% of your problems.

_It_ : Are there alternatives?

_Gu_ : Well we're starting to see a few. We could only use events in a sort of message bus. I spoke to a dev who is [building one for Angular](https://github.com/thebigredgeek/angular-events). Essentially directives and controllers can talk to each other by events. Anyone can fire an event and whatever is listening for it will do what it needs to do.

_It_ : Wait, couldn't you get into an infinite event loop like that? 

_Ma_ : Yes, but you can do that in code. It will be really obvious when you run your code and a compiler can check for it. Theoretically in the type theory, it's really obvious if you set up a never ending loop.

_Gu_ : Also, we're kind of seeing distributed applications. [Wolfram Cloud](http://www.wolfram.com/programming-cloud/?source=frontpage) was the last thing I saw to do this. Within their system, a page can talk to another page. Its sort of the same thing, but there's an underlying API. Essentially all we have now is you have to go through a bus and parts of programs can talk to each other. Program to program over the internet still requires some agreed upon API. It works for now though.

_It_ : This kind of sounds like this [Actor Model](https://www.youtube.com/watch?v=8pTEmbeENF4) I've heard about.

_Ma_ : I've heard of this some time ago. I'm not even familiar with it. Regardless, if programs could talk to each other without programmers physically or virtually meeting up, we couldn't get project managers to pay for our conferences. And obviously its a while away before programs talk to each other by probing each other to find out how to communicate. Its technically considered hacking.

_It_ : So what's next?

_Gu_ : You clean your code.

_Ma_ : And clean your tests.

_\*It grumbles and returns to his lair...\*_
