---
layout: post
title: Sorting in .NET MAUI DataGrid control | Syncfusion
description: Learn here all about Sorting support in Syncfusion .NET MAUI DataGrid (SfDataGrid) control and more.
platform: MAUI
control: SfDataGrid
documentation: UG
---

# Sorting in MAUI DataGrid (SfDataGrid)

The `SfDataGrid` provides the built-in support to sort one or more columns by using the `SfDataGrid.SortingMode` property. When sorting is applied, the datagrid automatically rearranges the data to match with the current sort criteria. You can sort the data simply by tapping the column header. Once sorting is applied, the datagrid shows a sort icon in the respective column header indicating the sort direction.

## Programmatic sorting

You can sort the data programmatically by adding or removing the `SortColumnDescription` in `SfDataGrid.SortColumnDescriptions` property.

The `SortColumnDescription` object holds the following two properties,

* **ColumnName**: Name of the sorted column.
* **SortDirection**: An object of type `ListSortDirection` defines the sorting direction.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfDataGrid x:Name="sfDataGrid" ItemsSource="{Binding OrderInfoCollection}" >

    <syncfusion:SfDataGrid.SortColumnDescriptions>
        <syncfusion:SortColumnDescription ColumnName="OrderID" SortDirection="Ascending" />
    </syncfusion:SfDataGrid.SortColumnDescriptions>
</syncfusion:SfDataGrid>
{% endhighlight %}

{% highlight c# %}
SortColumnDescription sortColumnDescription = new SortColumnDescription() { ColumnName = "OrderID", SortDirection = ListSortDirection.Ascending };
this.sfDataGrid.SortColumnDescriptions.Add(sortColumnDescription);
{% endhighlight %}
{% endtabs %}
## Different modes of sorting

`SfDataGrid` sorts the data against one or more columns based on the `SfDataGrid.SortingMode` property. The `SortingMode` contains the following properties,

* **Single** - It allows to sort only one column at a time.
* **Multiple** - It allows to sort more than one column at a time.
* **None** - None of the columns can be sorted.

To apply sorting for multiple columns, tap the desired column headers after setting the `SfDataGrid.SortingMode` property to `Multiple`.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfDataGrid x:Name="sfDataGrid" SortingMode="Multiple" ItemsSource="{Binding OrderInfoCollection}" >

    <syncfusion:SfDataGrid.SortColumnDescriptions>
        <syncfusion:SortColumnDescription ColumnName="OrderID" SortDirection="Ascending" />
    </syncfusion:SfDataGrid.SortColumnDescriptions>
</syncfusion:SfDataGrid>
{% endhighlight %}
{% endtabs %}

## Tri-state sorting

In addition to sort the data in ascending/descending order, the `SfDataGrid` unsort the data in the original order by clicking the header again after sorting to descending order by setting the `SfDataGrid.AllowTriStateSorting` property to true. When this property is set, sorting in each column iterates through three sort states: ascending, descending, and unsort.

{% tabs %}
{% highlight c# %}
this.sfDataGrid.AllowTriStateSorting = true;
{% endhighlight %}
{% endtabs %}

## Show sort number

The `SfDataGrid` provides support the sequence numbers to display the sorted columns during multi-column sorting by setting `SfDataGrid.ShowSortNumbers` is set to true. This is applicable when the `SfDataGrid.SortingMode` property is `Multiple`.

{% tabs %}
{% highlight c# %}
this.sfDataGrid.ShowSortNumbers = true;
{% endhighlight %}
{% endtabs %}

## Sort column in double tap

By default, column gets sorted when column header is clicked. This behavior can be changed to sort the column in double click action by setting `SfDataGrid.SortingGestureType` property to `DoubleTap`.

{% tabs %}
{% highlight c# %}
this.sfDataGrid.SortingGestureType = DataGridSortingGestureType.DoubleTap;
{% endhighlight %}
{% endtabs %}

## Sorting events

The data grid provides the following events for the sorting functionality,

* **SortColumnsChanging**: This event is invoked while sorting the column at execution time before the column gets sorted. It helps to cancel the sorting action by setting the `Cancel` property of `DataGridSortColumnsChangingEventArgs`.
* **SortColumnsChanged**: This event is invoked after the column is sorted.
These two events are triggered with `DataGridSortColumnsChangingEventArgs` and `DataGridSortColumnsChangedEventArgs` that contains the following properties:

**AddedItems**: Gets the collection of `SortColumnDescription` objects that are added to `SortColumnDescriptions` collection for sorting.
**RemovedItems**: Gets the collection of `SortColumnDescription` objects that are removed from `SortColumnDescriptions` collection.

Following code snippet demonstrates how to cancel sorting for a particular column by using `SortColumnsChanging` event,

{% tabs %}
{% highlight xaml %}
<syncfusion:SfDataGrid x:Name="sfDataGrid" SortingMode="Single" SortColumnsChanging="sfDataGrid_SortColumnsChanging" ItemsSource="{Binding OrderInfoCollection}" />

private void sfDataGrid_SortColumnsChanging(object sender, DataGridSortColumnsChangingEventArgs e)
{
    if (e.AddedItems[0].ColumnName == "OrderID")
    {
        e.Cancel = true;
    }
}
{% endhighlight %}

{% highlight c# %}
this.sfDataGrid.SortColumnsChanging += SfDataGrid_SortColumnsChanging;

private void sfDataGrid_SortColumnsChanging(object sender, DataGridSortColumnsChangingEventArgs e)
{
    if (e.AddedItems[0].ColumnName == "OrderID")
    {
        e.Cancel = true;
    }
}
{% endhighlight %}
{% endtabs %}

## Disable sorting for an individual column

The `SfDataGrid` disables sorting for an individual column by setting the `DataGridColumn.AllowSorting` property to false. The default value of this property is true.

### for auto generated columns

{% tabs %}
{% highlight xaml %}
<syncfusion:SfDataGrid x:Name="sfDataGrid" AutoGeneratingColumn="sfDataGrid_AutoGeneratingColumn" SortingMode="Single" ItemsSource="{Binding OrderInfoCollection}" >
</syncfusion:SfDataGrid>

private void sfDataGrid_AutoGeneratingColumn(object sender, DataGridAutoGeneratingColumnEventArgse)
{
    if (e.Column.MappingName == "OrderID")
    {
        e.Column.AllowSorting = false;
    }
}
{% endhighlight %}
{% endtabs %}

### for manually defined columns

{% tabs %}
{% highlight xaml %}
<syncfusion:SfDataGrid x:Name="sfDataGrid" AutoGenerateColumnsMode="None" SortingMode="Single"ItemsSource="{Binding OrderInfoCollection}" >
    <syncfusion:SfDataGrid.Columns>
        <syncfusion:DataGridNumericColumn HeaderText="Order ID" AllowSorting="False" MappingName="OrderID" />
        <syncfusion:DataGridTextColumn HeaderText="Customer ID" MappingName="CustomerID" />
        <syncfusion:DataGridTextColumn HeaderText="Customer" MappingName="Customer" />
        <syncfusion:DataGridTextColumn HeaderText="Ship City" MappingName="ShipCity" />
        <syncfusion:DataGridTextColumn HeaderText="Ship Country" MappingName="ShipCountry" />
    </syncfusion:SfDataGrid.Columns>
</syncfusion:SfDataGrid>
{% endhighlight %}
{% endtabs %}

## Custom sorting

The `SfDataGrid` sort columns based on custom logic, when the standard sorting techniques do not meet the requirements. For each column, you can apply different sorting criteria by adding `SortComparer` objects to `SfDataGrid.SortComparers` collection.

The `SortComparer` object contains the following properties,

* **PropertyName**: `MappingName` of the column that applies custom sorting.
* **Comparer**: Gets or sets the custom comparer that implements the `IComparer` and `ISortDirection` interfaces.

{% tabs %}
{% highlight xaml %}
<ContentPage
             xmlns:comparer="clr-namespace:GettingStarted.Comparer"
             xmlns:data="clr-namespace:Syncfusion.Maui.Data;assembly=Syncfusion.Maui.Data"
             xmlns:syncfusion="clr-namespace:Syncfusion.Maui.DataGrid;assembly=Syncfusion.Maui.DataGrid">

    <ContentPage.Resources>
        <ResourceDictionary>
            <comparer:CustomSortComparer x:Key="comparer" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <ContentPage.BindingContext>
        <local:ViewModel/>
    </ContentPage.BindingContext>

    <syncfusion:SfDataGrid x:Name="sfDataGrid"  SortingMode="Single" ItemsSource="{Binding OrderInfoCollection}" >
        <syncfusion:SfDataGrid.SortComparers>
            <data:SortComparer Comparer="{StaticResource comparer}" PropertyName="ShipCity" />
        </syncfusion:SfDataGrid.SortComparers>

        <syncfusion:SfDataGrid.SortColumnDescriptions>
            <syncfusion:SortColumnDescription ColumnName="ShipCity" SortDirection="Ascending"/>
        </syncfusion:SfDataGrid.SortColumnDescriptions>
    </syncfusion:SfDataGrid>
</ContentPage>

public class CustomSortComparer : IComparer<object>, ISortDirection
{
    private int cityX;
    private int cityY;

    private ListSortDirection sortDirection;

    public ListSortDirection SortDirection
    {
        get { return this.sortDirection; }
        set { this.sortDirection = value; }
    }

    public int Compare(object x, object y)
    {
        if (x!.GetType() == typeof(OrderInfo))
        { 
            this.cityX = ((OrderInfo)x!).ShipCity.Length;
            this.cityY = ((OrderInfo)y!).ShipCity.Length;
        }
        else
        {
            this.cityX = x.ToString()!.Length;
            this.cityY = y!.ToString()!.Length;
        }
        if (this.cityX.CompareTo(this.cityY) > 0)
        {
            return this.SortDirection == ListSortDirection.Ascending ? 1 : -1;
        }
        else if (this.cityX.CompareTo(this.cityY) == -1)
        {
            return this.SortDirection == ListSortDirection.Ascending ? -1 : 1;
        }
        else
        {
            return 0;
        }
    }
}

{% endhighlight %}
{% endtabs %}