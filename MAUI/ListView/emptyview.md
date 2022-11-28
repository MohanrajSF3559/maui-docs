---
layout: post
title: EmptyView in .NET MAUI ListView control | Syncfusion
description: Learn here all about EmptyView support in Syncfusion .NET MAUI ListView (SfListView) control and more.
platform: MAUI
control: SfListView
documentation: ug
---

# EmptyView in .NET MAUI ListView (SfListView)

`SfListView` allows you to display a string, numeric or view when `SfListView` has no items using `SfListView.EmptyView` property.

`SfListView.EmptyViewTemplate` property is used to customize the appearance of `SfListView.EmptyView`.

## Display a string when listview has no items

The `SfListView.EmptyView` property can be set to a string, which will be displayed when the `ItemsSource` is null, or when the collection specified by the `ItemsSource` property is null or empty.

{% tabs %}
{% highlight xaml tabtitle="MainPage.xaml" %}
<ContentPage xmlns:syncfusion="clr-namespace:Syncfusion.Maui.ListView;assembly=Syncfusion.Maui.ListView">
  <syncfusion:SfListView x:Name="listView"
                         ItemsSource="{Binding Items}"
                         ItemSize="56"
                         EmptyView="No Items">
  </syncfusion:SfListView>
</ContentPage>
{% endhighlight %}
{% highlight c# tabtitle="MainPage.xaml.cs" %}
listView.EmptyView = "No Items";
{% endhighlight %}
{% endtabs %}

## Display views when listview has no items

The `SfListView.EmptyView` property can be set to a view, which will be displayed when the `ItemsSource` property is null, or when the collection specified by the ItemsSource property is null or empty.

{% tabs %}
{% highlight xaml tabtitle="MainPage.xaml" %}
<ContentPage xmlns:syncfusion="clr-namespace:Syncfusion.Maui.ListView;assembly=Syncfusion.Maui.ListView">
  <syncfusion:SfListView x:Name="listView"
                         ItemsSource="{Binding Items}"
                         ItemSize="56">
    <syncfusion:SfListView.EmptyView>
      <StackLayout VerticalOptions="CenterAndExpand" >
        <Label Text="&#xe725;" FontSize="40" HorizontalTextAlignment="Center"
                               FontFamily="{OnPlatform iOS=ListViewFontIcons, MacCatalyst=ListViewFontIcons, Android=ListViewFontIcons.ttf#, UWP=ListViewFontIcons.ttf#ListViewFontIcons}" />                      
        <Label Text="No Items" FontSize="16" FontFamily="Roboto-Regular" HorizontalTextAlignment="Center" />
      </StackLayout>                    
    </syncfusion:SfListView.EmptyView>                       
  </syncfusion:SfListView>
</ContentPage>
{% endhighlight %}
{% highlight c# tabtitle="MainPage.xaml.cs" %}
StackLayout stackLayout = new StackLayout() { VerticalOptions = LayoutOptions.CenterAndExpand };

var label1 = new Label()
{
  Text = "\ue725",
  FontSize = 40,
  HorizontalTextAlignment = TextAlignment.Center,
  FontFamily = "ListViewFontIcons.ttf#"
};
var label2 = new Label()
{
  Text = "No Items",
  FontSize = 16,
  FontFamily = "Roboto-Regular",
  HorizontalTextAlignment = TextAlignment.Center,
};
stackLayout.Children.Add(label1);
stackLayout.Children.Add(label2);

listView.EmptyView = stackLayout;
{% endhighlight %}
{% endtabs %}

N> View displayed by `SfListView.EmptyView` can be a single view or a view that contains multiple child views.

![EmptyView in .NET MAUI ListView](Images/emptyview/maui-listview-emptyview.jpg)

Download the entire source code from GitHub [here](https://github.com/SyncfusionExamples/how-to-display-a-view-when-.net-maui-listview-has-no-items).

## Display a templated custom type when listview has no items
The appearance of `SfListView.EmptyView` can be customized by `SfListView.EmptyViewTemplate`, when `SfListView.EmptyView` property is set to a custom type.

{% tabs %}
{% highlight xaml tabtitle="MainPage.xaml" %}
<ContentPage xmlns:syncfusion="clr-namespace:Syncfusion.Maui.ListView;assembly=Syncfusion.Maui.ListView"
             xmlns:local="clr-namespace:EmptyViewTemplate">
  <Grid>
    <Grid.RowDefinitions>
      <RowDefinition Height="30"/>
      <RowDefinition Height="*" />
    </Grid.RowDefinitions>
    <SearchBar x:Name="filterText" 
               FontSize="16"                              
               Placeholder="Filter Inventory" TextChanged="SearchBar_TextChanged"/>                                                   
    <syncfusion:SfListView Grid.Row="1" x:Name="listView"
                           ItemsSource="{Binding Items}"
                           ItemSize="56">
      <syncfusion:SfListView.EmptyView>
        <local:FilterItem Filter="{Binding Source={x:Reference filterText},Path=Text}"/>
      </syncfusion:SfListView.EmptyView>
      <syncfusion:SfListView.EmptyViewTemplate>
        <DataTemplate>
          <Label Text="{Binding Filter,StringFormat='{0} is not found'}" HorizontalTextAlignment="Center"     
                 VerticalOptions="CenterAndExpand"
                 FontSize="18" FontFamily="Roboto-Regular"/>
        </DataTemplate>
      </syncfusion:SfListView.EmptyViewTemplate>                         
    </syncfusion:SfListView>
  </Grid>
</ContentPage>
{% endhighlight %}
{% highlight c# tabtitle="MainPage.xaml.cs" %}
listView.EmptyView = new FilterItem() { Filter = filterText.Text};

listView.EmptyViewTemplate = new DataTemplate(() =>
{
  Label label = new Label()
  {					
    FontSize = 18,
    FontFamily = "Roboto-Regular",
    VerticalOptions = LayoutOptions.CenterAndExpand,
    HorizontalTextAlignment = TextAlignment.Center
  };
  label.SetBinding(Label.TextProperty, new Binding("Filter", stringFormat : "{0} is not found"));
  return label;
});
{% endhighlight %}
{% endtabs %}

The `FilterItem` type defines a `Filter` property.

{% tabs %}
{% highlight c# tabtitle="FilterItem.cs" %}
public class FilterItem : BindableObject
{
  public static readonly BindableProperty FilterProperty = BindableProperty.Create(nameof(Filter), typeof(string), typeof(FilterItem), null);

  public string Filter
  {
      get { return (string)GetValue(FilterProperty); }
      set { SetValue(FilterProperty, value); }
  }
}
{% endhighlight %}
{% endtabs %}

FilterItem object is set to `SfListView.EmptyView` property and `Filter` property is binds to `SearchBar.Text` property. When SearchBar.TextChanged event is raised, value of `SearchBar.Text` property is stored in `Filter` property.   

![EmptyView Template in .NET MAUI ListView](Images/emptyview/maui-listview-emptyviewtemplate.jpg)

Download the entire source code from GitHub [here](https://github.com/SyncfusionExamples/how-to-customize-the-appearance-of-empty-view-using-empty-view-template-in-.net-maui-listview).

## Choose an EmptyView at runtime

The `SfListView` allows you to change `EmptyView` at run time. Views can be defined as ContentView objects in ResourceDictionary.

{% tabs %}
{% highlight xaml tabtitle="MainPage.xaml" %}
<ContentPage xmlns:syncfusion="clr-namespace:Syncfusion.Maui.ListView;assembly=Syncfusion.Maui.ListView"
             xmlns:local="clr-namespace:EmptyViewDemo">
  <ContentPage.Resources>
    <ResourceDictionary>
      <ContentView x:Key="SingleView">
        <Label Text="No Items" FontSize="18" FontFamily="Roboto-Regular" 
               HorizontalTextAlignment="Center" VerticalOptions="CenterAndExpand"/>
      </ContentView>
      <ContentView x:Key="MultiView">
        <StackLayout VerticalOptions="CenterAndExpand">
          <Label Text="&#xe725;" FontSize="40"
                 FontFamily="{OnPlatform iOS=ListViewFontIcons, MacCatalyst=ListViewFontIcons, Android=ListViewFontIcons.ttf#, UWP=ListViewFontIcons.ttf#ListViewFontIcons}"
                 HorizontalTextAlignment="Center" />
          <Label TextColor="#666666" Text="No Items" FontSize="16" FontFamily="Roboto-Regular" HorizontalTextAlignment="Center" />
        </StackLayout>
      </ContentView>
    </ResourceDictionary>
  </ContentPage.Resources>

  <ContentPage.Content>
    <Grid>
      <Grid.RowDefinitions>
        <RowDefinition Height="30"/>
        <RowDefinition Height="30"/>
        <RowDefinition Height="*" />
      </Grid.RowDefinitions>
      <SearchBar x:Name="filterText" 
                 FontSize="16"                              
                 Placeholder="Filter Inventory" TextChanged="SearchBar_TextChanged"/> 
      <CheckBox Grid.Row="1" x:Name="checkBox" IsChecked="False" 
                             CheckedChanged="CheckBox_CheckedChanged"/>                                                  
      <syncfusion:SfListView Grid.Row="2" x:Name="listView"
                             ItemsSource="{Binding Items}"
                             ItemSize="56"
                             EmptyView="{StaticResource SingleView}">                   
      </syncfusion:SfListView>
    </Grid>
  </ContentPage.Content>
</ContentPage>
{% endhighlight %}
{% highlight c# tabtitle="MainPage.xaml.cs" %}
listView.EmptyView = Resources["SingleView"];

checkBox.CheckedChanged += CheckBox_CheckedChanged;
{% endhighlight %}
{% endtabs %}

`SfListView.EmptyView` is changed based on value of CheckBox.IsChecked property at run time.

{% tabs %}
{% highlight c# tabtitle="MainPage.xaml.cs" %}
private void CheckBox_CheckedChanged(object sender, CheckedChangedEventArgs e)
{
  if(e.Value)
    listView.EmptyView = Resources["MultiView"];
  else
    listView.EmptyView = Resources["SingleView"];
}
{% endhighlight %}
{% endtabs %}

![SingleView EmptyView in .NET MAUI ListView](Images/emptyview/maui-listview-singleview-emptyview.jpg)

![MultiView EmptyView in .NET MAUI ListView](Images/emptyview/maui-listview-multiview-emptyview.jpg)

Download the entire source code from GitHub [here](https://github.com/SyncfusionExamples/how-to-change-empty-view-at-run-time-in-.net-maui-listview).

## Choose an EmptyViewTemplate at runtime

The `SfListView` allows you to choose appearance of `SfListView.EmptyView` at run time based on its value using `SfListView.EmptyViewTemplate` property.

{% tabs %}
{% highlight xaml tabtitle="MainPage.xaml" %}
<ContentPage xmlns:syncfusion="clr-namespace:Syncfusion.Maui.ListView;assembly=Syncfusion.Maui.ListView"
             xmlns:local="clr-namespace:EmptyViewTemplate">
  <ContentPage.Resources>
    <ResourceDictionary>          
      <DataTemplate x:Key="BasicTemplate">
        <Label Text="{Binding .,StringFormat='{0} is not found'}" 
               HorizontalTextAlignment="Center" VerticalOptions="CenterAndExpand"
               FontSize="18" FontFamily="Roboto-Regular"/>
      </DataTemplate>
      <DataTemplate  x:Key="AdvancedTemplate">
        <StackLayout VerticalOptions="CenterAndExpand">
          <Label Text="&#xe725;" 
                 FontSize="40"
                 FontFamily="{OnPlatform iOS=ListViewFontIcons, MacCatalyst=ListViewFontIcons, Android=ListViewFontIcons.ttf#, UWP=ListViewFontIcons.ttf#ListViewFontIcons}"
                 HorizontalTextAlignment="Center"/>
          <Label Text="{Binding .,StringFormat='{0} is not found'}" 
                 FontSize="16" 
                 FontFamily="Roboto-Regular" 
                 HorizontalTextAlignment="Center"/>
        </StackLayout>
      </DataTemplate>
      <local:EmptyViewDataTemplateSelector x:Key="DataTemplateSelector" 
                                           BasicTemplate="{StaticResource BasicTemplate}" 
                                           AdvancedTemplate="{StaticResource AdvancedTemplate}"/>
    </ResourceDictionary>
  </ContentPage.Resources> 

  <Grid>
    <Grid.RowDefinitions>
      <RowDefinition Height="30"/>
      <RowDefinition Height="*" />
    </Grid.RowDefinitions>
    <SearchBar x:Name="filterText" 
               FontSize="16"                              
               Placeholder="Filter Inventory" TextChanged="SearchBar_TextChanged"/>                                                   
    <syncfusion:SfListView Grid.Row="1" x:Name="listView"
                           ItemsSource="{Binding Items}"
                           ItemSize="56"
                           EmptyView="{Binding Source={x:Reference filterText},Path=Text}"
                           EmptyViewTemplate="{StaticResource DataTemplateSelector}">                         
    </syncfusion:SfListView>
  </Grid>
</ContentPage>
{% endhighlight %}
{% highlight c# tabtitle="MainPage.xaml.cs" %}
listView.EmptyView = filterText.Text;

listView.EmptyViewTemplate = new EmptyViewDataTemplateSelector() { BasicTemplate = this.Resources["BasicTemplate"] as DataTemplate, AdvancedTemplate = this.Resources["AdvancedTemplate"] as DataTemplate };
{% endhighlight %}
{% endtabs %}

The `SfListView.EmptyView` property is set to the SearchBar.Text property, and the `SfListView.EmptyViewTemplate` property is set to a EmptyViewDataTemplateSelector object.

{% tabs %}
{% highlight c# tabtitle="EmptyViewDataTemplateSelector.cs" %}
public class EmptyViewDataTemplateSelector : Microsoft.Maui.Controls.DataTemplateSelector
{
  public DataTemplate BasicTemplate { get; set; }
  public DataTemplate AdvancedTemplate { get; set; }

  public EmptyViewDataTemplateSelector()
  {
    
  }

  protected override DataTemplate OnSelectTemplate(object item, BindableObject container)
  {
    if(item.ToString().Count() > 10)
        return AdvancedTemplate;
    else
        return BasicTemplate;
  }
}
{% endhighlight %}
{% endtabs %}

![SingleView EmptyView Template in .NET MAUI ListView](Images/emptyview/maui-listview-singleview-emptyviewtemplate.jpg)

![MultiView EmptyView Template in .NET MAUI ListView](Images/emptyview/maui-listview-multiview-emptyviewtemplate.jpg)

Template for `SfListView.EmptyView` is set to AdvancedTemplate when SearchBar.Text.Count() is greater than 10. Otherwise, set to BasicTemplate.
