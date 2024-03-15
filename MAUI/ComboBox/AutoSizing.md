---
layout: post
title: AutoSizing in .NET MAUI ComboBox control | Syncfusion
description: Learn about auto sizing support in Syncfusion .NET MAUI ComboBox (SfComboBox) control and more here.
platform: maui
control: SfComboBox
documentation: ug
---

# AutoSizing in .NET MAUI ComboBox (SfComboBox)

AutoSizing can be enabled in the [SfComboBox](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Inputs.SfComboBox.html) control so that the control will extend its layout based on the input content.

The EnableAutoSize property is used to enable the auto sizing in the SfComboBox control. To enable the API, set the SelectionMode as Multiple and TokensWrapMode as Wrap. The default value of EnableAutoSize is false.

{% tabs %}
{% highlight xaml %}

<editors:SfComboBox x:Name="comboBox"
             WidthRequest="350"
             ItemsSource="{Binding SocialMedias}"
             SelectionMode="Multiple"
             MaxDropDownHeight="250"
             DisplayMemberPath="Name"
             TextMemberPath="Name"
             TokensWrapMode="Wrap"
             EnableAutoSize="True" />

{% endhighlight %}
{% endtabs %}

![.NET MAUI ComboBox AutoSize.](Images/selection/net-maui-combobox-autosize.png){:width="444" height="393" .lazy .shadow-effect .section-padding .img-padding loading="lazy"}
