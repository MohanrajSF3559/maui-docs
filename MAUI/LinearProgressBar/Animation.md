---
layout: post
title: Animation in .NET MAUI SfLinearProgressBar control | Syncfusion
description: Learn here all about animation support in Syncfusion .NET MAUI SfLinearProgressBar control, its elements and more.
platform: MAUI
control: SfLinearProgressBar
documentation: ug
---

# Animation in .NET MAUI SfLinearProgressBar (Linear Progress Bar)

The progress bar provides animation support to visualize the progress value changes in an interactive way. 

The following properties are used to define the duration of animation for the specific states.

* `AnimationDuration:` Represents animation duration of the determinate state’s progress indicator.
* `SecondaryAnimationDuration:` Represents animation duration of the determinate state’s secondary progress indicator.
* `IndeterminateAnimationDuration:` Represents animation duration of the indeterminate state’s indicator.

## Easing effects

The `AnimationEasing` property allows you specify the transfer function that controls animation speed when they run. 

The following code sample demonstrates the `CubicInOut` easing function of the linear progress bar.

{% tabs %} 

{% highlight xaml %}

<progressBar:SfLinearProgressBar Progress="75" 
                                 AnimationEasing="{x:Static Easing.CubicInOut}" />

{% endhighlight %}

{% highlight c# %}

SfLinearProgressBar linearProgressBar = new SfLinearProgressBar();
linearProgressBar.Progress = 75;
linearProgressBar.AnimationEasing = Easing.CubicInOut;
this.Content = linearProgressBar;

{% endhighlight %}

{% endtabs %} 

![.NET MAUI linear Progress Bar with CubicInOut animation](images/animation/easing-animation.gif)

The `SetProgress()` method in the progress bar is used to set progress value along with animation duration and easing effect applicable for the specific method call.

{% highlight c# %}

void SetProgress(double progress, double? animationDuration = null, Easing? easing = null)

{% endhighlight %}

N> The animation duration and easing effect parameters will not affect the configuration of the `AnimationDuration`and `AnimationEasing` properties.

## Indeterminate Easing Effects

The `IndeterminateAnimationEasing` property allows you to specify a transfer function for indeterminate state, which controls animation speed when they run.

The following code sample demonstrates the `BounceIn` easing function of the linear progress bar.

{% tabs %} 

{% highlight xaml %}

<progressBar:SfLinearProgressBar IsIndeterminate="True" 
                                 IndeterminateAnimationEasing="{x:Static Easing.BounceIn}" />

{% endhighlight %}

{% highlight c# %}

SfLinearProgressBar linearProgressBar = new SfLinearProgressBar();
linearProgressBar.IsIndeterminate = true;
linearProgressBar.IndeterminateAnimationEasing = Easing.BounceIn;
this.Content = linearProgressBar;

{% endhighlight %}

{% endtabs %} 

![.NET MAUI linear Progress Bar with indeterminate animation](images/animation/indeterminate.gif)

N> Refer to our `.NET MAUI SfLinearProgressBar` feature tour page for its groundbreaking feature representations. Also explore our [.NET MAUI SfLinearProgressBar example](https://github.com/syncfusion/maui-demos/) that shows how to configure a SfLinearProgressBar in .NET MAUI.