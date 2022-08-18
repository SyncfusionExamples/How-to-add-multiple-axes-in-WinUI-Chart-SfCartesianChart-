# How-to-add-multiple-axes-in-WinUI-Chart-SfCartesianChart

The WinUI Cartesian chart provides support to add multiple axes inside the same chart area with specified x-axis and y-axis. There are two properties XAxisName and YAxisName in all the Cartesian series type, which is used to provide multiple axes support.

The user guide Documentation helps you to acquire more knowledge on charts and their features. You can also refer to the Feature Tour site to get an overview of all the features in the chart.

![WinUI Chart Multiple Axes](https://user-images.githubusercontent.com/61832185/176182402-3f4b05ca-8869-4d30-b4c6-e38c4a5dc114.png)

### Step 1: 
Create a simple project using the instructions given in the Getting Started with your first WinUI app documentation.

### Step 2: 
Add Syncfusion.Chart.WinUI NuGet to the project and import the SfCartesianChart namespace as follows.

**[XAML]**
```
xmlns:chart="using:Syncfusion.UI.Xaml.Charts"
```
**[C#]**
```
using Syncfusion.UI.Xaml.Charts;
```
### Step 3: 
Initialize an empty chart with XAxes and YAxes as shown in the following code sample.

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
Create a ViewModel class with a data collection property to set the ViewModel instance as the DataContext of your window; this is done to bind properties of ViewModel to the chart.

> Note: Add namespace of ViewModel class to your XAML page, if you prefer to set DataContext in XAML.

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

As we are going to visualize the multiple axes in cartesian chart, add multiple axes to the SfCartesianChart.XAxes or SfCartesianChart.YAxes property.  Then, Assign these axis names to the XAxisName or YAxisName property of the cartesian series.

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
      <chart:LineSeries  YAxisName="yAxis1" />
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
series1.YAxisName = "yAxis1";

SplineSeries series2 = new SplineSeries();
series2.YAxisName = "yAxis2";

chart.Series.Add(series1);
chart.Series.Add(series2);

this.Content = chart;
``` 
