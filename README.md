Loading animations
==========================

different types of loading animations.

===================================
<br>
Different types of loading animations.

 *"Animation is not the art of drawing that move but the art of movements that are drawn".*
 
<p>
A good mobile app is often defined by fluid animation and a clean UI. 
 Performance does matter, but what if its not intuitive to the user; it's rendered useless. 
 A few trend setting mobile apps such as google plus, path, foursquare etc, are known for their amazing UI.
 These main stream apps have their own unique loading animations. 
My sole purpose of writing this article was to show how you can implement those loading animations and customize your own for your app.
</p>

##Screenshot

![Loading](https://dl.dropboxusercontent.com/u/61919232/raw_blog/LoadingAnimation/loading.gif "loading")

<br>

<p>
The Android framework provides two animation systems: [Property Animation](http://developer.android.com/guide/topics/graphics/prop-animation.html) (introduced in Android 3.0) and 
	[View animation](http://developer.android.com/guide/topics/graphics/prop-animation.html#q=view animation). Both animation systems are viable options, but the property animation system, in general, is the preferred method to use,because it is more flexible and offers more features.
    
</p>    


Property Animation
---------------------------------------------------
A property animation changes a property's (a field in an object) value over a specified length of time. To animate something, you specify the object property that you want to animate, such as an object's position on the screen, how long you want to animate it for, and what values you want to animate between.




Sample app shows how property animation can be implemented. Following points are covered:

```java
PropertyValuesHolder myView_Y = PropertyValuesHolder.ofFloat(myView.TRANSLATION_Y, -40.0f);
PropertyValuesHolder myView_X = PropertyValuesHolder.ofFloat(myView.TRANSLATION_X, 0);
ObjectAnimator waveOneAnimator = ObjectAnimator.ofPropertyValuesHolder(myView, myView_X, myView_Y);
waveOneAnimator.setRepeatCount(-1);        // -1 for infinite
waveOneAnimator.setRepeatMode(ValueAnimator.REVERSE);
waveOneAnimator.setDuration(300);
waveOneAnimator.start();
```

<br>
* How to implement an animation.

```java
PropertyValuesHolder myView_Y = PropertyValuesHolder.ofFloat(myView.TRANSLATION_Y, -40.0f);
PropertyValuesHolder myView_X = PropertyValuesHolder.ofFloat(myView.TRANSLATION_X, 0);
ObjectAnimator waveOneAnimator = ObjectAnimator.ofPropertyValuesHolder(myView, myView_X, myView_Y);
```

<p>
In the above example we are using `PropertyValuesHolder` class to animate Y-co ordinate of the view.
Here we are translating Y-co ordinate by -40 and keeping X-coordinate as 0.
<br>
[ObjectAnimator](http://developer.android.com/reference/android/animation/ObjectAnimator.html#ObjectAnimator() is a subclass of `ValueAnimator`,  provides support for animating properties on target view. 
</p>

* How to loop an animation.

```java
waveOneAnimator.setRepeatCount(-1); // -1 for infinite
```
`setRepeatCount(int n)` this method is use to set animation count.
Here -1 means infinte and 0 means only once.
If n > 0 then then animation will be repeated n times.
Another handy way to repeat an animation is by using listeners.
```java
For example:

waveOneAnimator.addListener(new AnimatorListener() {

    		@Override
			public void onAnimationStart(Animator animation) {}

			@Override
			public void onAnimationRepeat(Animator animation) {}

			@Override
			public void onAnimationEnd(Animator animation) {
				waveOneAnimator.start();	// infinite loop.
			}

			@Override
			public void onAnimationCancel(Animator animation) {}
		});

```

<br>
   How to run multiple animation's together or independently.

   a. To animate sequentially :

```java
        AnimatorSet animatorSet1 = new AnimatorSet();
		animatorSet1.playSequentially(valueAnimatorOne, valueAnimatorTwo, valueAnimatorThree); 
		animatorSet1.start();
```
    b. To animate all animation at same time.


```java
        AnimatorSet animatorSet1 = new AnimatorSet();
    	animatorSet1.playTogether(valueAnimatorOne, valueAnimatorTwo, valueAnimatorThree);
		animatorSet1.start();
```















