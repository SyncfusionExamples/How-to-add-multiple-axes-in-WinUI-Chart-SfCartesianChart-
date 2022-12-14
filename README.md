# How to add multiple axes in WinUI Chart (SfCartesianChart)?

The WinUI [Cartesian chart](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.SfCartesianChart.html) provides support to add multiple axes inside the same chart area with the specified x-axis and y-axis. There are two properties [XAxisName](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.CartesianSeries.html#Syncfusion_UI_Xaml_Charts_CartesianSeries_XAxisName) and [YAxisName](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.CartesianSeries.html#Syncfusion_UI_Xaml_Charts_CartesianSeries_YAxisName) in all the [CartesianSeries](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.CartesianSeries.html) types, which are used to provide multiple axes support.

This user guide [Documentation](https://help.syncfusion.com/winui/cartesian-charts/getting-started) helps you to acquire more knowledge on charts and their features. You can also refer to the [Feature Tour](https://www.syncfusion.com/winui-controls/charts) site to get an overview of all the features in the chart.

![WinUI Chart Multiple Axes](https://user-images.githubusercontent.com/61832185/176182402-3f4b05ca-8869-4d30-b4c6-e38c4a5dc114.png)

### Step 1: 
Create a simple project using the instructions given in the Getting Started with your first [WinUI app](https://docs.microsoft.com/en-us/windows/apps/winui/winui3/create-your-first-winui3-app?tabs=csharp) documentation.

### Step 2: 
Add [Syncfusion.Chart.WinUI](https://www.nuget.org/packages/Syncfusion.Chart.WinUI/) NuGet to the project and import the [SfCartesianChart]((https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.SfCartesianChart.html)) namespace as follows.

**[XAML]**
```
xmlns:chart="using:Syncfusion.UI.Xaml.Charts"
```
**[C#]**
```
using Syncfusion.UI.Xaml.Charts;
```
### Step 3: 
Initialize an empty chart with [XAxes](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.SfCartesianChart.html#Syncfusion_UI_Xaml_Charts_SfCartesianChart_XAxes) and [YAxes](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.SfCartesianChart.html#Syncfusion_UI_Xaml_Charts_SfCartesianChart_YAxes) as shown in the following code sample.

**[XAML]**
```
<chart:SfCartesianChart>

    <chart:SfCartesianChart.XAxes >
        <chart:DateTimeAxis/>
    </chart:SfCartesianChart.XAxes >

    <chart:SfCartesianChart.YAxes >
        <chart:NumericalAxis/>
    </chart:SfCartesianChart.YAxes >

</chart:SfCartesianChart>

```
**[C#]**
```
SfCartesianChart chart = new SfCartesianChart();

//Initializing XAxes
DateTimeAxis xAxis = new DateTimeAxis ();
chart.XAxes.Add.(xAxis);

//Initializing YAxes
NumericalAxis yAxis = new NumericalAxis();
chart.YAxes.Add.(yAxis);

this.Content = chart;
```
### Step 4: 
Create a `ViewModel` class with a data collection property to set the `ViewModel` instance as the `DataContext` of your window; this is done to bind properties of `ViewModel` to the chart.

> Note: Add namespace of `ViewModel` class to your XAML page, if you prefer to set `DataContext` in XAML.

**[XAML]**
```
xmlns:viewModel="using:CartesianChartDesktop"
. . .
<chart:SfCartesianChart>

      <chart:SfCartesianChart.DataContext>
             <viewModel:ViewModel/>
      </chart:SfCartesianChart.DataContext>
</chart:SfCartesianChart>
```
**[C#]**
```
SfCartesianChart chart = new SfCartesianChart();
chart.DataContext = new ViewModel();
```
### Step 5: Populate chart with multiple axes.

As we are going to visualize the multiple axes in the cartesian chart, add multiple axes to the [SfCartesianChart.YAxes](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.SfCartesianChart.html#Syncfusion_UI_Xaml_Charts_SfCartesianChart_YAxes) property.  Then, assign the specified axis name to the independent axis required cartesian series [YAxisName](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.CartesianSeries.html#Syncfusion_UI_Xaml_Charts_CartesianSeries_YAxisName) property as illustrated below:

**[XAML]**
```
<chart:SfCartesianChart>
    <chart:SfCartesianChart.DataContext>
           <viewModel:ViewModel/>
     </chart:SfCartesianChart.DataContext>
. . .
    <chart:SfCartesianChart.XAxes>
      <chart:DateTimeAxis />
  </chart:SfCartesianChart.XAxes>

  <chart:SfCartesianChart.YAxes>
      <chart:NumericalAxis x:Name="yAxis1" />
     <chart:NumericalAxis x:Name="yAxis2" OpposedPosition="True"  />
  </chart:SfCartesianChart.YAxes>
. . .
  <chart:SfCartesianChart.Series>
      <chart:LineSeries />
      <chart:SplineSeries YAxisName="yAxis2" />
  </chart:SfCartesianChart.Series>
. . .
</chart:SfCartesianChart>
```
**[C#]**
```
SfCartesianChart chart = new SfCartesianChart();
chart.DataContext = new ViewModel();
. . .

DateTimeAxis xAxis = new DateTimeAxis();
chart.XAxes.Add(xAxis);

NumericalAxis yAxis1 = new NumericalAxis()
{
	Name = "yAxis1",
};

NumericalAxis yAxis2 = new NumericalAxis()
{
	Name = "yAxis2",
};

chart.YAxes.Add(yAxis1);
chart.YAxes.Add(yAxis2);

LineSeries series1 = new LineSeries();

SplineSeries series2 = new SplineSeries();
series2.YAxisName = "yAxis2";

chart.Series.Add(series1);
chart.Series.Add(series2);

this.Content = chart;
``` 
> Note: By default, series are plotted based on the 0th index axis of the [XAxes](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.SfCartesianChart.html#Syncfusion_UI_Xaml_Charts_SfCartesianChart_XAxes) and [YAxes](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.SfCartesianChart.html#Syncfusion_UI_Xaml_Charts_SfCartesianChart_YAxes) collections.

KB article - [How to add multiple axes in WinUI (SfCartesianChart)?](https://www.syncfusion.com/kb/13615/how-to-add-multiple-axes-in-winui-chart-sfcartesianchart)
