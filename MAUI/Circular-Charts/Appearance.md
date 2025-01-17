---
layout: post
title: Appearance in .NET MAUI Chart control  Syncfusion
description: Learn here all about appearance customization in .NET MAUI Chart (SfCircularChart), its elements and more.
platform: maui
control: SfCircularChart
documentation: ug
---

# Appearance in .NET MAUI Circular Chart

## Plotting Area Customization:

[SfCircularChart](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Charts.SfCircularChart.html?tabs=tabid-1) allows you to add any view to the chart plot area, which is useful for adding any relevant data, a watermark, or a color gradient to the background of the chart.

{% tabs %}

{% highlight xaml %}

<chart:SfCircularChart>
   <chart:SfCircularChart.PlotAreaBackgroundView>
      <AbsoluteLayout>
       <Border Stroke="red"
			StrokeThickness="2"
			AbsoluteLayout.LayoutBounds="0,0,1,1"
			AbsoluteLayout.LayoutFlags="All"/>
       <Label Text="Copyright @ 2001 - 2022 Syncfusion Inc"
			FontSize="18"
			AbsoluteLayout.LayoutBounds="1,1,-1,-1"
			AbsoluteLayout.LayoutFlags="PositionProportional"
			Opacity="0.4"/>
       <Label Text="CONFIDENTIAL"
			Rotation="340"
			FontSize="80"
			FontAttributes="Bold,Italic"
			TextColor="Gray"
			Margin="10,0,0,0"
			AbsoluteLayout.LayoutBounds="0.5,0.5,-1,-1"
			AbsoluteLayout.LayoutFlags="PositionProportional"
			Opacity="0.3" />
    </AbsoluteLayout>
   </chart:SfCircularChart.PlotAreaBackgroundView>
</chart:SfCircularChart>

{% endhighlight %}

{% highlight c# %}

SfCircularChart chart = new SfCircularChart();
AbsoluteLayout absoluteLayout = new AbsoluteLayout();
var border = new Border() {Stroke = Colors.Red,StrokeThickness = 2};
AbsoluteLayout.SetLayoutBounds(border, new Rect(0, 0, 1, 1));
AbsoluteLayout.SetLayoutFlags(border, Microsoft.Maui.Layouts.AbsoluteLayoutFlags.All);
absoluteLayout.Children.Add(border);
var copyRight = new Label() {Text = "Copyright @ 2001 - 2022 Syncfusion Inc",FontSize = 18,Opacity = 0.4};
AbsoluteLayout.SetLayoutBounds(copyRight, new Rect(1, 1, -1, -1));
AbsoluteLayout.SetLayoutFlags(copyRight, Microsoft.Maui.Layouts.AbsoluteLayoutFlags.PositionProportional);
absoluteLayout.Children.Add(copyRight);
var watermark = new Label(){Text = "CONFIDENTIAL", Rotation = 340,FontSize = 80,FontAttributes = FontAttributes.Bold,TextColor = Colors.Gray,Opacity = 0.3};
AbsoluteLayout.SetLayoutBounds(watermark, new Rect(0.5, 0.5, -1, -1));
AbsoluteLayout.SetLayoutFlags(watermark, Microsoft.Maui.Layouts.AbsoluteLayoutFlags.PositionProportional);
absoluteLayout.Children.Add(watermark);
chart.PlotAreaBackgroundView = absoluteLayout;
this.Content = chart;

{% endhighlight %}

{% endtabs %}

![Watermark in .NET MAUI Charts](Appearance_images/water_mark.jpg)