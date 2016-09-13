---

layout: post
title: Thinking outside the box
category: code
taxonomy:
    tag: [lab, experiment, javascript, canvas]
highlight: true
image: /assets/images/think-outside-the-box.gif
author: axel

---

![Outside the box](/assets/images/think-outside-the-box.gif){: .center .image-zoom}

## Actually, drawing outside the box

Few weeks ago, I stumbled upon [an experiment](http://benjaminbenben.com/){: target="_blank"} by [@benjaminbenben](https://twitter.com/benjaminbenben){: target="_blank"} where he was drawing a shape outside of the window.

I was amazed, and I looked at his code.

The hack works with **canvas** and the **CSS cursor property**.

At every frame, he draws an image in a hidden canvas, turning it to a PNG (with DataURL), and replacing the cursor image with this output.

This is actually pretty easy to implement.

Here is what it looks like once applied to a banner:

<iframe src="https://clients.bannerboy.com/bannerboy/lab/bannerboy_cursorhack_300x250/" width="300" height="250" class="center"></iframe>

<br/>

The gray area is an iFrame, but it even works outside of the browser window.

___

## Limitations

This opens some creative possibilities, but there are still some important limitations to consider:

* The size of a cursor limited to **128px by 128px**. That means you are limited with the size you can draw, and you can draw only close to the window.
* Drawing a canvas every frame can be a lot of work for the CPU, depending on the image.
* The "ethical" aspect of this hack is also to consider. It could be fun, but also ruin the user experience.
* One shouldn't assume it's safe to use in production. Ad platforms or even browsers could prevent the use of this at any time.

Don't forget:

> With great power comes great responsibility.


## The code

{% highlight javascript %}
// limit for cursor size is 128
var canvas = document.createElement('canvas')
canvas.width = canvas.height = 128

var ctx = canvas.getContext('2d')
ctx.fillStyle = 'rgba(54, 177, 197, 0.8)'
ctx.strokeStyle = 'rgba(54, 177, 197, 0.5)'

var cx, cy, x, y, animation

document.body.addEventListener('mousemove', function(e){
	cx = e.clientX
	cy = e.clientY
	x = cx / banner.get("width")
	y = cy / banner.get("height")

	if(!animation) animation = requestAnimationFrame(animate)
})

function animate(time){
	animation = null

	ctx.clearRect(0,0,128,128)

	var angle = Math.atan2(x-.5, y-.5)
	var extent = Math.max(Math.abs(x-.5), Math.abs(y-.5)) * 2

	ctx.save()
	ctx.translate(64, 64)
	ctx.rotate(-angle)
	ctx.translate(-64, -64)

	ctx.beginPath()
	ctx.arc(64, 64 + (54*extent), 8, 0, Math.PI*2)
	ctx.fill()

	ctx.beginPath()
	ctx.moveTo(64,64 + (54*extent))
	ctx.lineTo(64,(1-extent) * 64)
	ctx.stroke()

	ctx.restore()

	var url = canvas.toDataURL()

	banner.style.cursor = 'url('+url+') '+(1-x)*128+' '+(1-y)*128+', crosshair'
}
{% endhighlight %}

*note: in this code, `banner` is custom element, not a standard DOM Element, but you get the idea ;)*

___

*All credit for the code goes to [@benjaminbenben](https://twitter.com/benjaminbenben){: target="_blank"}, image from [www.keypersonofinfluence.com](http://www.keypersonofinfluence.com/how-can-we-think-outside-the-box-from-inside-the-box/){: target="_blank"}*