---
layout: post
title: SwipGesture in .NET MAUI Navigation Drawer | Syncfusion
description: Learn here all about SwipGesture support in Syncfusion .NET MAUI Navigation Drawer (SfNavigationDrawer) control and more.
platform: .NET MAUI
control: NavigationDrawer
documentation: ug
---
# SwipeGesture in .NET MAUI Navigation Drawer

The NavigationDrawer supports the swipe gesture for both opening and closing the drawer. 

## Enabling Swipe Gesture

The `EnableSwipeGesture` property can activate or deactivate the swipe functionality in the `SfNavigationDrawer`.

{% tabs %}

{% highlight xaml %}

<navigationdrawer:SfNavigationDrawer x:Name="navigationDrawer">
    <navigationdrawer:SfNavigationDrawer.DrawerSettings>
        <navigationdrawer:DrawerSettings EnableSwipeGesture="True">
        </navigationdrawer:DrawerSettings>
    </navigationdrawer:SfNavigationDrawer.DrawerSettings>
</navigationdrawer:SfNavigationDrawer>

{% endhighlight %}	
	
{% highlight c# %} 

SfNavigationDrawer navigationDrawer = new SfNavigationDrawer();
DrawerSettings drawerSettings = new DrawerSettings()
{
    EnableSwipeGesture= true,
};
navigationDrawer.DrawerSettings = drawerSettings;
this.Content = navigationDrawer;

{% endhighlight %}

{% endtabs %}