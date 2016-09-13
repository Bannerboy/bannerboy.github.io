---

layout: post
title: Chat with Firebase
category: code
taxonomy:
    tag: [onetag, twotag]
highlight: true
author: axel

---

## This is just a test article

**[Firebase](https://firebase.google.com){: target="_blank"} is a service allowing (among other things) to use real time database. It was bought by Google few month ago, and was completely redesigned last week, during the Google IO.**

![Firebase logo](/assets/images/firebase-logo.png){: .center}

## Why Firebase ?

One of our customer wanted to implement a chat in a banner. That means that thousands of users could access it at the same time. **We needed a powerful backend for that task.**

> This is what a blockquote looks like

![Overwatch Takeover](/assets/images/overwatch-winston-homepage-takeover@2x.png){: .center .image-zoom}


A great man said once: 

> click the image to zoom

## And another H2

We can also create lists

- **Something important**: I mean, really important.
- **Another bold item** 

*Maybe you just want some italic.*

### Introduce code, with h3 this time

{% highlight html %}
<script src="https://www.gstatic.com/firebasejs/live/3.0/firebase.js"></script>
<script>
	var config = {
		apiKey: "xxxxxxxxxxxxx-xxxx-xxxxxxxxxxxxx-xxxx-x",
		authDomain: "xxxxx.firebaseapp.com",
		databaseURL: "https://xxxxx.firebaseio.com",
		storageBucket: "",
	};
	firebase.initializeApp(config);
</script>
{% endhighlight %}


## Embed banner

> Check out this hack: playing with the cursor property and canvas allows to draw outside of the iFrame's boundaries

<iframe src="http://wall.bannerboy.com/html/bannerboy_cursorhack_300x250/" width="300" height="250" class="center"></iframe>

___


### Markup HTML

{% highlight html %}
<body>
	<div id="messages"></div>
	<input type="textfield" id="textfield"/>
	<script type="text/javascript" src="main.js"></script>
</body>
{% endhighlight %}

Inline code is also possible: `div #messages`

<s>But it might look weird in the middle of a paragraph</s>

___ 

### JavaScript works too

I like Objects in JS.

{% highlight javascript %}
function Chat() {
	var _ = this,
	database = firebase.database(),
	messages = database.ref('messages');
	
	messages.limitToLast(10).on('child_added', function(message){
		_.onnewmessage(message.val());
	})

	this.post = function(message) {
		messages.push({
			text: message,
		})
	}

	this.onnewmessage = function(message){};
}
var chat = new Chat();
{% endhighlight %}

{% highlight javascript %}
document.getElementById('textfield').onchange = function(event) {
	chat.post(event.target.value);
	event.target.value = "";
}
{% endhighlight %}

{% highlight javascript %}
chat.onnewmessage = function(message) {
	var new_message = document.createElement('p');
	new_message.innerHTML = message.text;
	document.getElementById('messages').appendChild(new_message);
}
{% endhighlight %}

{% highlight javascript %}
messages: {
	-KIbY0H0EtilzTE6avuM: { 
		text: "Never gonna give you up..."
	},
	-KIbY4plQII23PLZOurp: {
		text: "Never gonna let you down..."
	},
	-KIbuceFPebbHpM62L90: {
		text: "I love this song!"
	},
	...
}
{% endhighlight %}


![Firebase chat](/assets/images/firebase-chat.gif){: .center}

----

## Conclusion

Did you like it?
