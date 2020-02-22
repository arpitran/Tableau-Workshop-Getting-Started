![alt text](https://github.com/arpitran/Tableau-Learning/blob/master/Tableau%20Workshop%20-%20Getting%20Started/Workshop%20Images/Intro%20to%20Tableau.PNG)

# Introduction to Tableau - Part 2

This workshop and the materials in this repo are for anyone who is interested in working with Tableau to produce high quality, interactive data visualizations!

Everyone is welcome, whether you are completely new to Tableau or have some amount of experience, as we will begin with the very basics of using this tool and progress to more advanced techniques.

# Download Tableau
Download one of the following to be able to make your own workbook:
* Tableau Desktop (free trial): https://tableau.com/products/desktop/download
* Tableau Public (always free) - make an account and then download the app: https://public.tableau.com

Note that Tableau only has apps for Mac & Windows.

Tableau Desktop (free trial): https://tableau.com/products/desktop/download
Tableau Public (always free) - make an account and then download the app: https://public.tableau.com
Free license for instructors https://www.tableau.com/academic/teaching
Free license for students: https://www.tableau.com/academic/students
Free 14 day trial: https://www.tableau.com/products/desktop/download


## Agenda
* Using a Parameter to Change Fields
* Pareto Chart


Overview
Parameters can be thought of as a variable whose value is controlled by the end user.
This can be something like choosing a cutoff value for an analysis, or even which field is
displayed in a viz.
Let’s say we want to build a single chart that will be used by two different groups of
people – one who are interested in sales, and the other who are interested in profit. We
only want to make one view but let the person using it chose what value they want to see.

The overall process is easy:
1. Create a parameter to let us select which measure we want to use.
2. Create a calculated field to tie that parameter to the data source.
3. Use the calculated field in the view.
4. Show the parameter control.

### Creating the Parameter
First, we’ll create the parameter itself. Right click in the data pane and select “Create
Parameter”. We’ll name this “Sales or Profit?” For Data Type, select String. This will
allow us to enter text values. For Allowable values, choose “list” so we can type in what
we want. Now we’ll enter the fields we want to use. Type Profit, and hit enter. Note that
the Display As automatically updates to the same value. We need to remember exactly
what we put for the value – we’ll need it later. Then in the next row, we’ll type Sales.
Click OK.

![alt text](https://github.com/arpitran/Tableau-Learning/blob/master/How%20To/Workshop%20Images/Create%20a%20parameter.jpg)


### Creating the Calculated Field
Now we have that parameter, but it doesn’t do us any good because it’s not impacting
anything yet. We need to create a calculated field using the parameter’s input. Right click
in the data pane and select “Create Calculated Field”. We’ll name this “Sales or Profit”.
Because we need to go through several options for the parameter’s input and assign each 3
to a specific field, we’ll use a CASE function. We could also use IF. First, we’ll type CASE,
then drag out the parameter. Type WHEN, then type the first value in quotes “Profit”.
This has to match exactly what we put in the parameter value field, and remember, it is
case sensitive. Next we’ll type THEN, and drag out the Profit field. Repeat with the next
value. WHEN “Sales” THEN [Sales]. And finish with END.
Essentially what this does is tell Tableau “when the parameter says profit, give me the
profit field. When the parameter says sales, give me the sales field”. So now we have a
field we can use in the view that responds to the parameter.

```
CASE [Profit or Sales?]
WHEN "Profit"
THEN [Profit]
WHEN "Sales"
THEN [Sales]
END
```

![alt text](https://github.com/arpitran/Tableau-Learning/blob/master/How%20To/Workshop%20Images/create%20calculated%20field.jpg)

### Building the View
Let’s add this to the viz. We can drag Sales off the Columns shelf. And bring out our new
field, [Sales or Profit] to the Columns shelf. We’re now using a field that will either show
Sales or Profit, but how do we change between those options? Right click on the “Sales or
Profit?” parameter and select Show Parameter Control. The viewer can now change the
parameter and the view will update.

![alt text](https://github.com/arpitran/Tableau-Learning/blob/master/How%20To/Workshop%20Images/build%20a%20view%20with%20parameter.jpg)


### Pareto Charts
What is a Pareto Chart?
A Pareto chart is used to see how many dimension items, such as products, are
contributing to what percentage of an overall measure, such as Sales. Pareto charts are
often used in conjunction with the 80/20 rule, which states that 80% of sales come from
20% of customers, or 80% of value comes from 20% of content, etc.
To make a Pareto chart, we’ll use table calculations to compute the percent of total of the
running total for both the measure and the count distinct of the dimension. 

![alt text](https://github.com/arpitran/Tableau-Learning/blob/master/How%20To/Workshop%20Images/pareto%20chart.jpg)

### Building a Pareto Chart – the line

Our Pareto will deal with products and sales. Bring Product ID to Columns and choose
All Members. Bring Sales to Rows. Sort sales descending, and fit the width. 

![alt text](https://github.com/arpitran/Tableau-Learning/blob/master/How%20To/Workshop%20Images/pareto%20chart%20step%201.jpg)

Next, we want to calculate the running percent of total sales. Right click on the Sales pill on the
Rows shelf and add a quick table calculation for Running Total. Right click again on the
same pill and select Edit Table Calc. Click “Specific Dimensions” and make Sure Product
ID is checked, to make this an addressing field. Check the box to Perform a secondary
calculation on the result. For the secondary type of calculation, choose “Percent of Total”.

![alt text](https://github.com/arpitran/Tableau-Learning/blob/master/How%20To/Workshop%20Images/edit%20table%20calculation.jpg)

Now we need to change the x axis from a sorted list of Product IDs to display a percent
of total as well. Control click drag a copy of Product ID from Columns to the Detail shelf.

![alt text](https://github.com/arpitran/Tableau-Learning/blob/master/How%20To/Workshop%20Images/drag%20sorted%20product%20id%20to%20detail.jpg)

Right click on the Product ID pill on Columns change the aggregation to Count Distinct.
We’ll now do the same thing we did for Sales, calculating the percent of running total.
Right click again and add a quick table calculation for Running Total. Right click again
and select Edit Table Calc. Click Specific Dimensions and check Product ID to make
this an addressing field, and perform a secondary calculation, of type Percent of Total.

![alt text](https://github.com/arpitran/Tableau-Learning/blob/master/How%20To/Workshop%20Images/repeat%20steps%20for%20product%20id.jpg)

Make sure Product ID is a sorted field

![alt text](https://github.com/arpitran/Tableau-Learning/blob/master/How%20To/Workshop%20Images/make%20sure%20product%20id%20is%20a%20sorted%20field.jpg)

Finally, change the mark type to line. This is the core of the Pareto chart.
Building a Pareto Chart – the bars
A true Pareto chart has both the line as well as a bar chart. To add the bar chart: bring a
new copy of sales to the Rows shelf, right click on this second copy of Sales and choose
Dual Axis. Change the mark type for Sum of Sales to a bar. We may want to resize the 
bars to be tiny. Right click on the right-hand Sales axis and select Move Marks to Back,
then again and Uncheck Show Header and we’ll edit our colors so the line is blue.

![alt text](https://github.com/arpitran/Tableau-Learning/blob/master/How%20To/Workshop%20Images/move%20marks%20to%20back%20uncheck%20show%20headers.jpg)

Building a Pareto Chart – the reference lines
Finally, we can add reference lines to illustrate the 80/20 rule. Click on the Analytics tab
and bring out a constant line to count distinct of Product ID. Set the value to 0.2. 

![alt text](https://github.com/arpitran/Tableau-Learning/blob/master/How%20To/Workshop%20Images/add%20a%20constant%20line.jpg)

Bring out another constant line to the Sum of Sales with the table calc, indicated by the delta
symbol. Set the value to 0.8. As we can see, in this data set, we need closer to 28% of our
product IDs to get 80% of our sales.

Summary of Steps
As a quick recap, to make a Pareto chart:
1. Use table calculations to compute the percent of total of the running total for both
the measure and the count distinct of the dimension
2. Bring a new copy of Sales out and make it a bar chart underneath the line
3. Add reference lines for 20% of the dimension (count distinct) and 80% of the
measure
