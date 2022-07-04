---
layout: post
title: Filtering in .NET MAUI DataGrid control | Syncfusion
description: Learn here all about Filtering support in Syncfusion .NET MAUI DataGrid (SfDataGrid) control and more.
platform: MAUI
control: SfDataGrid
documentation: UG
---

# Filtering in MAUI DataGrid (SfDataGrid)

Filtering is the process of retrieving the values from the collection which satisfy the specified condition. The `SfDataGrid` provides the view filtering support.

## View filtering

The `SfDataGrid` supports to filter the records in the view by setting `SfDataGrid.View.Filter` property where `Filter` is a predicate.

>N Note: In order to refresh filtering for the newly added row or column, set the `SfDataGrid.View.LiveDataUpdateMode` to `LiveDataUpdateMode.AllowDataShaping`.

{% tabs %}
{% highlight c# %}
private void Button_Clicked(object sender, EventArgs e)
{
	this.sfDataGrid.View.Filter = FilterRecords;
    this.sfDataGrid.View.RefreshFilter();
}

public bool FilterRecords(object record)
{
	OrderInfo? orderInfo = record as OrderInfo;

	if(orderInfo != null && orderInfo.ShipCity == "Germany")
	{
		return true;
	}
	return false;
}
{% endhighlight %}
{% endtabs %}

>N Note: View filtering is not supported when `ItemsSource` is `DataTable`.

## Filter based on conditions

Additionally, the records can be filtered based on the conditions. For example, the records can be filtered based on the given input or contrast to the input. The condition based filtering can also be achieved for all the columns or any particular column.

The records can be filtered based on any of the following conditions,

* Equals
* Does not equal
* Contains

The above mentioned conditions are the mostly used conditions. You can simply add new condition based on your requirement and alter the following code snippets on the basis of your requirement.

{% tabs %}
{% highlight c# %}
public bool FilterRecords(object record)
{
    OrderInfo orderInfo = record as OrderInfo;

    if (orderInfo != null)
    {
        if (columns.SelectedItem.ToString() == "All Columns")
        {
            if (conditions.SelectedItem.ToString() == "Contains")
            {
                var filterText = FilterText.ToLower();
                if (orderInfo.OrderID.ToString().ToLower().Contains(filterText) ||
                    orderInfo.CustomerID.ToLower().Contains(filterText) ||
                    orderInfo.Customer.ToLower().Contains(filterText) ||
                    orderInfo.ShipCountry.ToLower().Contains(filterText) ||
                    orderInfo.ShipCity.ToLower().Contains(filterText))
                    return true;
                return false;
            }
            else if (conditions.SelectedItem.ToString() == "Equals")
            {
                if (CheckEquals(orderInfo.OrderID.ToString()) ||
                    CheckEquals(orderInfo.CustomerID) ||
                    CheckEquals(orderInfo.Customer) ||
                    CheckEquals(orderInfo.ShipCountry) ||
                    CheckEquals(orderInfo.ShipCity))
                    return true;
                return false;
            }
            else
            {
                if (!CheckEquals(orderInfo.OrderID.ToString()) ||
                   !CheckEquals(orderInfo.CustomerID) ||
                   !CheckEquals(orderInfo.Customer) ||
                   !CheckEquals(orderInfo.ShipCountry) ||
                   !CheckEquals(orderInfo.ShipCity))
                    return true;
                return false;
            }
        }
        else
        {
            var value = record.GetType().GetProperty(columns.SelectedItem.ToString().Replace(" ",""));
            var exactValue = value.GetValue(record, null);
            if (conditions.SelectedItem.ToString() == "Contains")
            {
                return FilterText.ToLower().Contains(exactValue.ToString().ToLower());
            }
            else if (conditions.SelectedItem.ToString() == "Equals")
            {
                return CheckEquals(exactValue.ToString());
            }
            else
            {
                return !CheckEquals(exactValue.ToString());
            }
        }
    }
    return false;
}

public bool CheckEquals(string value)
{
    return FilterText.Equals(value);
}

private void Button_Clicked(object sender, EventArgs e)
{
	this.sfDataGrid.View.Filter = FilterRecords;
	this.sfDataGrid.View.RefreshFilter();
}
{% endhighlight %}
{% endtabs %}

The following code example illustrates how to create a `Picker` for conditions and add appropriate strings to that Picker and how the records will be filtered based on selected conditions,

{% tabs %}
{% highlight xaml %}
<Grid Grid.Row="1" Grid.Column="0">
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="150"/>
        <ColumnDefinition Width="150"/>
        <ColumnDefinition Width="150"/>
    </Grid.ColumnDefinitions>

    <Picker
        x:Name="columns"
        Grid.Row="0" Grid.Column="0">
        <Picker.Items>
            <x:String>All Columns</x:String>
            <x:String>Order ID</x:String>
            <x:String>Customer ID</x:String>
            <x:String>Customer</x:String>
            <x:String>Ship City</x:String>
            <x:String>Ship Country</x:String>
        </Picker.Items>
        <Picker.SelectedItem>
            <x:String>All Columns</x:String>
        </Picker.SelectedItem>
    </Picker>
    <Picker 
        x:Name="conditions"
        Grid.Row="0" Grid.Column="1">
        <Picker.Items>
            <x:String>Equals</x:String>
            <x:String>Does Not Equal</x:String>
            <x:String>Contains</x:String>
        </Picker.Items>
    </Picker>

    <Button Grid.Row="0" Grid.Column="3" Text="Filter" Clicked="Button_Clicked"/>
</Grid>
{% endhighlight %}
{% endtabs %}

## Clear filtering

You can clear the applied filtering by setting the `SfDataGrid.View.Filter` property to `null`.

{% tabs %}
{% highlight c# %}
private void Button_Clicked(object sender, EventArgs e)
{
	this.sfDataGrid.View.Filter = null;
    this.sfDataGrid.View.RefreshFilter();
}
{% endhighlight %}
{% endtabs %}