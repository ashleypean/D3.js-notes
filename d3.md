# Notes for D3.js Course on Educative.io

## D3 Selections 
  * The ```select()``` and the ```selectAll()``` methods are used by the D3 library to select DOM elements on the page and manipulate them
    * The ```select()``` method will return the first instance of an element that you are searching for. <span style="color:red">If the element does not exist on the page it will return an empty selection </span> 

    #### Example 
    ###### HTML
    ~~~ 
    <html>
    <head>
	    <script src="https://d3js.org/d3.v6.min.js" />
    </head>

    <body>
      <div>hello world</div>
    </body>
    </html>
    ~~~

    ###### JavaScript 
    ~~~
    var s = d3.select('div').text();
    console.log(s)  //'hello world'
    ~~~

    * The ```selectAll()``` method will select multiple instances of an HTML tag and apply manipulations to all of them. <span style="color:red">If the element does not exist on the page it will return an empty selection </span> 

    #### Example 
    ###### HTML  
    ~~~
    <html>
    <head>
    <script src="https://d3js.org/d3.v6.min.js" />
    </head>

    <body>
    <div>Welcome to Educative</div>
      <div>Introduction to D3.js</div>
    </body>
    </html>
    ~~~

    ###### JavaScript 
    ~~~
    d3.selectAll('div').style("color","green");
    ~~~

    ###### Output 
    @import "images/Screen Shot 2021-02-12 at 6.41.27 PM.png"

## Manipulating DOM Elements
 * ```text()``` method
    * Used to add or modify text inside of a DOM element

    #### Example
    ###### HTML 
    ~~~
    <html>
      <head>
      <script src="https://d3js.org/d3.v6.min.js" />
      </head>

      <body>
      <div></div>
      </body>
    </html>
    ~~~

    ###### JavaScript 
    ~~~
    d3.select('div').text("I am adding text");
    ~~~

    ###### Output 
    @import "images/Screen Shot 2021-02-12 at 6.47.28 PM.png"

  * ```append()``` method
    * Used to add a new HTML DOM element to the page 

    #### Example
    ###### HTML 
    ~~~
    <html>
      <head>
      <script src="https://d3js.org/d3.v6.min.js" />
      </head>

      <body>
      <div>Introduction to Visualization using D3.js</div>
      </body>
    </html>
    ~~~

    ###### JavaScript 
    ~~~
    d3.select("body").append("div").text("Appending new div tag")
    ~~~

    ###### Output 
    @import "images/Screen Shot 2021-02-12 at 6.50.20 PM.png"

  * ```remove()``` method 
    * Used to remove and HTML DOM element from the page 

  * ```style()``` method
    * Allows us to add styling to an HTML DOM element 

    #### Example
    ###### HTML 
    ~~~
    <html>
      <head>
      <script src="https://d3js.org/d3.v6.min.js" />
      </head>

      <body>
      <div>Showing effect of the style method</div>
      </body>
    </html>
    ~~~

    ###### JavaScript 
    ~~~
    d3.select("div").style("color","blue").style("font-size","30px")
    ~~~

    ###### Output 
    @import "images/Screen Shot 2021-02-12 at 7.20.31 PM.png"

  * ```attr()``` method
    * Allows us to manipulate any HTML attribute of a dom element 

    #### Example
    ###### HTML 
    ~~~
    <html>
      <head>
      <script src="https://d3js.org/d3.v6.min.js" />
      </head>

      <body>
      <div>Showing effect of the attr method</div>
      </body>
    </html>
    ~~~   

    ###### JavaScript 
    ~~~
    //Change class attribute of element to 'error'
    d3.select("div").attr("class","error"); 
    ~~~

## Data Joins/Binding 
  * Data joining allows us to bind the data we wish to show in our visualization in an array 
  * Array of data + HTML/SVG element = Data Join
  
  *```datum()```
    * Joins a single data point with a single D3 selection 

  #### Example  
  ###### JavaScript
  ~~~~
    d3.select("body")
    .select("p") //Select the 'p' element in HTML DOM
    .datum(["10"]) //Bind the number 10 to the element  
    .text(function(d) { return d; }); //The parameter 'd' is now available as the value(s) we passed in the datum() method
  ~~~~
  Prints '10' to the screen 
  @import "images/Screen Shot 2021-02-12 at 7.34.45 PM.png"

  * ```data()```
    * Used to associate a set of/multiple data points with an HTML DOM element 

  #### Example  
  ###### JavaScript
  ~~~~
    d3.select("body")
    .selectAll("p") //Select all 'p' elements in HTML DOM
    .datum([10, 20, 30]) //Bind the numbers 10, 20, and 30 to the elements  
    .text(function(d) { return d; }); //The parameter 'd' is now available as the value(s) we passed in the datum() method
  ~~~~

  @import "images/Screen Shot 2021-02-12 at 7.37.30 PM.png"

  *```enter()```
    * Used when the number of HTML elements we are selecting is less than the number of elements in the data array. This method will take the amount of elements we already have on the page and add more in order to display the data to the screen  

  #### Example  
  ###### HTML
  ~~~
  <html>
  <head>
	<script src="https://d3js.org/d3.v6.min.js"></script>
  </head>

  <body>
    <p></p>
    <p></p>
    <p></p>
  </body>
  </html>
  ~~~

  ###### JavaScript 
  ~~~
  d3.select("body").selectAll("p")
  .data([10, 20, 30, 50, 70])
  .text(function(d) { return d; })
  .enter() //Enter method will create a new HTML dom node for each extra element in the data
  .append("p") //Create a new 'p' element for each new entry and add it to the page
  .text(function(d) { return d; });
  ~~~

  ###### Output 
  @import "images/Screen Shot 2021-02-12 at 7.42.41 PM.png"

  # Scales
  * Scales are functions that take a data point and convert it to a position, length, and color

  ## Linear Scales 
  * Linear scales signify a continuous input to output relationship
  * Linear scales can be signified by the function: $y = mx + b$, where x = input and y = output
  * Input is also signified with the ```domain()``` function, while output is signified by the ```range()``` function 

  #### Example 
  ##### JavaScript 
  ~~~
  var cgpaconv = d3.scaleLinear()
  .domain([0, 10])
  .range([0, 4]);

  console.log(cgpaconv(5)) // 2
  ~~~

  ## Logarithmic Scales 
  * Logarithmic scales signify a continuous logarithmic transformation in the input to output relationship
  $y = mlog(x) + b$
  * <span style="color:red">Since log(0) is equal to $infinity$, make sure that the domain of a logarithmic function always includes zero.</span> If we pass a negative value as the domain, it will return ```NAN```

  #### Example 
  ###### JavaScript 

$log2(N)$
  ~~~
  var b_step = d3.scaleLog()
    .domain([1, 1048576])
    .range([0, 20])
    .base(2)
  ~~~

## Clamp Function 
  * The clamp function allows us to clamp/attach our domain to a given range. So if we are given an input outside of our domain, the output will still be within our range  
  * Clamp has a Boolean value of ```false``` by default. Setting it to ```true``` forces all of your ouputs to show within the provided range, even if the input is outside of the scope of the domain.

  #### Examples 
  Out of Range 
  ~~~
  var cgpaconv = d3.scaleLinear()
    .domain([0, 10])
    .range([0, 4]);

  console.log(cgpaconv(12)); // 4.8
  ~~~

  In Range 
  ~~~
  var cgpaconv = d3.scaleLinear()
    .domain([0, 10])
    .range([0, 4])
    .clamp(true);

  console.log(cgpaconv(12)); // 4
  ~~~

## scaleQuantize 
  * Used when the input is continuous and the output is discrete $y = mx + c$

  #### Example 
  ~~~
  var qscale = d3.scaleQuantize()
    .domain([0, 100])
    .range(['Neon Carrot', 'Caribbean Green', 'Spring Green', 'Iris Blue']);

  console.log(qscale(5)); // 'Neon Carrot'
  ~~~

  In this example, our domain (0 - 100) is continuous. There is a clear progression of increasing values for our input number. Our range however, is discrete (there is no clear progression/order) between the different output options. 

  @import "images/Screen Shot 2021-02-12 at 10.32.49 PM.png"

  #### invert Extent 
  * Function that returns the portion of ```input``` for the corresponding value of the given ```range``` in the ```scaleQuantize``` function 
    ##### Example
    ###### JavaScript 
    ~~~
    var qscale = d3.scaleQuantize()
      .domain([0, 100])
      .range(['Neon Carrot', 'Caribbean Green', 'Spring Green', 'Iris Blue']);

    console.log(qscale.invertExtent('Neon Carrot')) //[0: 0, 1: 25]
    console.log(qscale.invertExtent('Caribbean Green')) // [0: 25, 1: 50]
    console.log(qscale.invertExtent('Spring Green')) // [0: 50, 1: 75]
    console.log(qscale.invertExtent('Iris Blue')) // [0: 75, 1: 100]
    ~~~ 

    
## Scale Ordinal 
  * The ```scaleOrdinal()``` function maps discrete input to discrete output
    * If ```domain.length = range.length```, mapping is one-to-one
    * If ```domain.length > range.length```, mapping will repeat itself 
    * If ```domain.length < range.length```, mapping will continue on a scale of one-to-one and all the extra elements in the range will be discarded 

    #### Example 
    ###### JavaScript 
    ~~~
    var grade_conv = d3.scaleOrdinal()
      .domain(['A','A-','B','B-','C'])
      .range([10,9,8,7,6]);

    console.log(grade_conv("A")) // 10
    console.log(grade_conv("B")) // 8
    ~~~
  
  * If we get an unexpected/undesired input, we can invoke the ```unknown()``` function to display an error 

    #### Example 
    ###### JavaScript 
    ~~~
    var grade_conv = d3.scaleOrdinal()
      .domain(['A','A-','B','B-','C'])
      .range([10,9,8,7,6]);
      .unknown('Not a grade')

    console.log(grade_conv("Y")) // 'Not a grade'
    ~~~

## Scale Band 
  * The ```scaleBand()``` method maps discrete ```input``` to ```bands``` of output (super helpful w/ bar charts)

    #### Example 
    ###### JavaScript 
    ~~~
    var grade_conv = d3.scaleBand()
      .domain(['X','Y','Z'])
      .range([0,300]);

    console.log(grade_conv("X")) // 0
    console.log(grade_conv("Z")) // 200
    ~~~    
  
    @import "images/Screen Shot 2021-02-12 at 10.57.41 PM.png"

  * You can also use the ```bandwidth()``` method to find the width/size of bands for data points 

    #### Example 
    ###### JavaScript 
    ~~~
    var grade_conv = d3.scaleBand()
      .domain(['X','Y','Z'])
      .range([0,300])

    console.log(grade_conv.bandwidth())  //100
    ~~~    

## SVG
  * SVG, or scalable vector graphics, is a markup language used to draw 2 dimensional graphics on a webpage
  ~~~
  <body>
     <svg>content</svg>
  </body>
  ~~~ 
  * SVG's consist of graphical (elements that render content) and non-graphical elements (elements that style/manage existing content), including: 
    * Lines ```<line />```
    * Rectangles ```<rect />```
    * Circles ```<circle />```
    * Paths ```<path />```
    * Text ```<text />```

    #### Example 
    ###### Without D3
    ~~~
    <html>
    <head>
    </head>
    <body>
      <svg height="200" width= "200" style="border: solid 8px red">
        <line x1 = "50" y1 = "30" 
                  x2 = "150" y2 = "100" style = "stroke: black;
                  stroke-width:2px"/>
        </svg>   
    </body>
    </html>
    ~~~

    ###### With D3
    ~~~
    var svg = d3.select("body") //create Svg element
      .append("svg")
      .attr("height",200 )
      .attr("width", 200)
      .style("border", "solid 8px red");

    svg.append("line")
      .attr("x1", 50)
      .attr("y1", 30)
      .attr("x2", 150)
      .attr("y2", 100)
      .attr("stroke", "black")
      .attr("stroke-width","2px");
    ~~~

    @import "images/Screen Shot 2021-02-13 at 9.33.46 AM.png"

  ### Transformations 
  * Transformations allow use to tranform one or more SVG element with the following values: 
    * Translate
      * Allows us to move elements on the page along the x- and y-axis
      ##### Example 
      ~~~
      var svg = d3.select("body") //create Svg element
      .append("svg")
      .attr("height",320 )
      .attr("width", 400)
      .style("border", "solid 8px red");

      svg.append("rect") //Draw rectangle
        .attr("x", 50)
        .attr("y", 50)
        .attr("height", 100)
        .attr("width", 150)
        .attr("fill", "#00A5E3")
        .transition() // line 13 and 14 will be explain in detail in next lesson
        .duration(3000)
        .attr("transform","translate(150,150)");
      ~~~
      @import "images/Screen Shot 2021-02-14 at 4.14.29 PM.png"
    * Rotate
      * Allows us to turn images around 360°
      ##### Example 
      ~~~
      var svg = d3.select("body") //create Svg element
        .append("svg")
        .attr("height",370 )
        .attr("width", 370)
        .style("border", "solid 8px red");

      svg.append("rect") //Draw rectangle
        .attr("x", 200)
        .attr("y", 50)
        .attr("height", 100)
        .attr("width", 150)
        .attr("fill", "#00A5E3")
        .transition() // line 13 and 14 will be explain in detail in next lesson
        .duration(3000)
        .attr("transform","rotate(50)")
      ~~~
      @import "images/Screen Shot 2021-02-14 at 4.16.29 PM.png"
    * Scale 
      * Allows us to upsize or downsize an SVG image 

      ##### Example
      ~~~
      var svg = d3.select("body") //create Svg element
        .append("svg")
        .attr("height",400 )
        .attr("width", 400)
        .style("border", "solid 8px red");
      svg.append("circle") //Drawing circle
        .attr("cx", 100)
        .attr("cy", 100)
        .attr("r", 50)
        .attr("fill", "#FF96C5")
        .transition() // line 13 and 14 will be explain in detail in next lesson
        .duration(3000)
        .attr("transform","scale(2)")
      ~~~
      @import "images/Screen Shot 2021-02-14 at 4.17.57 PM.png"
    * Skew 
      * Allows us to specify which angle an SVG element will be skewed along 
      * Options to skew an image are: ```skewX()``` and ```skewY()```

      ##### Example 
      ~~~
      var svg = d3.select("body") //create Svg element
        .append("svg")
        .attr("height",300 )
        .attr("width", 400)
        .style("border", "solid 8px red");

      svg.append("rect") //Draw rectangle
        .attr("x", 50)
        .attr("y", 50)
        .attr("height", 150)
        .attr("width", 170)
        .attr("fill", "#00A5E3")
        .transition() // line 13 and 14 will be explain in detail in next lesson
        .duration(3000)
        .attr("transform","skewX(30)")
      ~~~
       @import "images/Screen Shot 2021-02-14 at 4.20.54 PM.png"

  ## Transition 
  * Transitions give us the ability to animate our SVG elements from one state to another 
  ##### Syntax 
  ~~~
  .transition()
  .delay(500)
  ~~~

# Chart Design Principles

  ## Five-second rule 
  * Charts should answer the important question about your data within 5 seconds. If it takes longer than that, there is a problem with the chart's design 

  ## Selecting the right chart 
  * Line charts display trends and can be used to display continuous data over time.
  * Bar charts are used to compare data between different groups over time.
  * Pie charts are used to show proportions of the whole data and is more intuitive when used for percentages.
  * Scatter charts are used to show the relationship between data.
  * Treemaps are used to display hierarchical data.

  ## Color Selection 
  * NO MORE than 6 - 7 colors in one layout 
  * Don't use <span style="color:red">red</span> for positive values and <span style="color:green">green</span> for negative values
  * There should be a significant contrast between two colors (i.e. don't use green and light green for two different data points)

  ## Axis 
  * D3.js provides four function to draw axis scales: 
    * Bottom horizontal: ```d3.axisBottom()``` 
    * Top horizontal: ```d3.axisTop()```
    * Left vertical: ```d3.axisLeft()```
    * Right vertical ```d3.axisRight()```
    @import "images/IMG_A5DA28993C70-1.jpeg"
  ~~~
  var svg = d3.select("body") //create Svg element
    .append("svg")
    .attr("height",250)
    .attr("width", 350)
    .style("border", "solid 1px red")

  var data = [
      { X:0, Y: 0 },
      { X: 10, Y: 100 },
      { X: 50, Y: 200 },
      { X: 80, Y: 400 },
      { X:100, Y:150}];

  var xscale = d3.scaleLinear()
                .domain(d3.extent(data, d=>d.X)) //Take the min and max values from the data
                .range([0,300]); //Set the range to 300px wide 

  svg.append('g')
    .call(d3.axisBottom(xscale))
  ~~~

  @import "images/Screen Shot 2021-02-15 at 1.47.21 PM.png"

  ## Labels 
  * Provide text-based information to describe the axes of a chart 
  * D3 does not natively provide a label component, but you can create one dynamically using basic JavaScript 

  ~~~ 
  var svg = d3.select("body") //create Svg element
    .append("svg")
    .attr("height",500)
    .attr("width", 700)
    .style("border", "solid 1px red")

  var data = [
      { day:0, stock_value: 0 },
      { day:5, stock_value: 100 },
      { day:10, stock_value: 200 },
      { day:15, stock_value: 400 },
      { day:20, stock_value:150 }];

   // drawing  x scale
  var xscale = d3.scaleLinear()                        
                .domain(d3.extent(data, d=>d.day))
                .range([0,500]);

  // drawing  y scale
  var yscale= d3.scaleLinear()                         
              .domain(d3.extent(data,d=>d.stock_value))
              .range([400,0])    

  // drawing  x-axis
  svg.append('g')                                      
    .call(d3.axisBottom(xscale))
    .attr("transform","translate(150,420)")

  // drawing y-axis
  svg.append('g')                                     
    .call(d3.axisLeft(yscale))
    .attr("transform","translate(150,20)") 

  // labelling x-axis
  svg.append("text")                                  
      .text("day")          
      .attr("transform","translate(390,470)");

  // labelling y-axis
  svg.append("text")                                 
      .text("stock_value")
      .attr('transform', "translate(100,270) rotate(-90)");  
  ~~~  

  @import "images/Screen Shot 2021-02-15 at 2.04.01 PM.png"

  ## Margins 
  * Margins tell the D3 framework where our visual data ends. Without it, our margin would exist on the boundary of the SVG component 

  ~~~
    // defining a margin object with a property for each side
    var margin = {top: 20, right: 20, bottom: 60, left: 60}; 
    
    // overall height and width of the chart
    var width = 400 - margin.left - margin.right; 
    var height = 400 - margin.top - margin.bottom; 

    var svg = d3.select("body") //create Svg element
      .append("svg")
      .attr('width', width + margin.right + margin.left)   
      .attr('height', height + margin.top + margin.bottom) 
      .style("border", "solid 1px red")
      
    var data = [
      { X:0, Y: 0 },
      { X: 10, Y: 100 },
      { X: 250, Y: 200 },
      { X: 300, Y: 400 },
      { X:350, Y:150}
    ];

    //drawing xscale
    var xscale = d3.scaleLinear()                        
                  .domain(d3.extent(data, d=>d.X))
                  .range([0,width]);

    // drawing  y scale              
    var yscale= d3.scaleLinear()                         
                  .domain(d3.extent(data,d=>d.Y))
                  .range([height,0]);

    //defining chart
    var chart=svg.append('g')                           
      .attr('transform', 'translate(' + margin.left + ',' + margin.top + ')')
      .attr('width', width)
      .attr('height', height);

    chart.append('g')
      .call(d3.axisBottom(xscale))
      .attr('transform', 'translate(0,' + height + ')');

    chart.append('g')
      .call(d3.axisLeft(yscale));
  ~~~
  @import "images/Screen Shot 2021-02-15 at 2.52.57 PM.png"

  ## Paths 
  * A path is a combination of lines that are oftentimes used to 
  * A path has a few attributes available to it to define how it looks: 
    * ```d``` - an attribute that **defines** the path to be drawn 
    * ```M``` - command that defines the **starting point** of a path 
    * ```L``` - command that defines other lines to be drawn on the path 
  ~~~
  var svg = d3.select("body") 
    .append("svg")
    .attr("height",500 )
    .attr("width", 500)
    .style("border", "solid 8px red")

  //Draw path
  svg.append("path") 
    .attr("d","M 10 10 L 200 200 L 300 20 L 400 450")
    .attr("stroke","blue")
    .attr("fill","none")
    .attr("stroke-width","2px")
  ~~~
    

  @import "images/Screen Shot 2021-02-15 at 3.11.48 PM.png"

  ## Line Generator 
  * A line generator takes an ```(x,y)``` coordinate as input 

  ~~~
  var svg = d3.select("body") //create Svg element
    .append("svg")
    .attr("height",500)
    .attr("width", 500)
    .style("border", "solid 8px red")

  var data = [
    { X:10,Y:100},
    { X:250,Y:200},
    { X:300,Y:400},
    { X:400,Y:150}
    ];

  var generator = d3.line()
    .x(function (d) { return d.X; })
    .y(function (d) { return d.Y; });
  svg.append('path')
    .datum(data)
    .attr("d", generator)
    .attr("fill","none")
    .attr("stroke","blue")
    .attr("stroke-width","2px");
  ~~~

  ## Line Chart
  * A line chart can be built with the help of the **line generator** and **scale time** functions
  ~~~
  var margin = {top: 20, right: 20, bottom: 60, left: 80},
      width = 700 - margin.left - margin.right,
      height = 700 - margin.top - margin.bottom;

  var svg = d3.select("body") //create Svg element
    .append("svg")
    .attr('width', width + margin.right + margin.left)
    .attr('height', height + margin.top + margin.bottom)
    .style("border", "solid 1px red")

  var data = [
    {  date:"2020/01/01 00:00:00", patients: 600 },
    {  date:"2020/02/01 00:00:00", patients: 500 },
    {  date:"2020/03/01 00:00:00", patients: 400 },
    {  date:"2020/04/01 00:00:00", patients: 500 },
    {  date:"2020/05/01 00:00:00", patients: 300 },
    {  date:"2020/06/01 00:00:00", patients: 100 },
    {  date:"2020/07/01 00:00:00", patients: 50  },
    {  date:"2020/08/01 00:00:00", patients: 500 },
    {  date:"2020/09/01 00:00:00", patients: 550 },
    {  date:"2020/10/01 00:00:00", patients: 550 },
  ];

  data = data.map(d => ({
    date: new Date(d.date),
    patients: d.patients
  }))        

  var xscale = d3.scaleTime()
    .domain(d3.extent(data, d=>d.date))
    .range([0,width]);

  var yscale= d3.scaleLinear()                       
    .domain([0,600])
    .range([height,0]
    )                   
  var chart=svg.append('g')
    .attr('transform', 'translate(' + margin.left + ',' + margin.top + ')')
    .attr('width', width)
    .attr('height', height)

  chart.append('g')
    .call(d3.axisBottom(xscale).tickFormat(d3.timeFormat("%b")))
    .attr('transform', 'translate(0,' + height + ')')

  chart.append('g')
    .call(d3.axisLeft(yscale))

  svg.append("text")                                  // labelling x-axis
    .text("Month")          
    .attr("transform","translate(350,680)");

  svg.append("text")                                 // labelling y-axis
    .text("Number of patients")
    .attr('transform', "translate(40,400) rotate(-90)");   

  var generator = d3.line()
    .x(function (d) { return xscale(d.date); })
    .y(function (d) { return yscale(d.patients); });      

  chart.append('path')
    .datum(data)
    .attr("d", generator)
    .attr("fill","none")
    .attr("stroke","blue");
  ~~~

  @import "images/Screen Shot 2021-02-19 at 11.21.46 PM.png"


  ## Arcs
  * Arcs are curved structures in D3 that make up pie charts. They are made up of three attributes: 
    * ```innerRadius()``` - specifies the inner radious for the arc. If set to zero the arc will resemble a pie instead of a donut
    * ```outerRadius()``` - specifies the outer radius of the arc
    * ```startAngle()``` - specifies the start angle for the radius (in radians)
    * ```endAgle()``` - specifies the end angle for the arc (in radians)

  ```Radian = Degree * PI/180```

    ~~~~
    var margin = {top: 20, right: 20, bottom: 60, left: 80},
      width = 600 - margin.left - margin.right,
      height = 600 - margin.top - margin.bottom;

    var svg = d3.select("body") //create Svg element
      .append("svg")
      .attr('width', width + margin.right + margin.left)
      .attr('height', height + margin.top + margin.bottom)
      .style("border", "solid 1px red")
             
    var chart=svg.append('g')
      .attr('transform', 'translate(' + margin.left + ',' + margin.top + ')')
      .attr('width', width)
      .attr('height', height)

    var arc = d3.arc()                  // simple arc
      .innerRadius(0)
      .outerRadius(70)
      .startAngle(45 * (Math.PI/180)) //converting from degs to radians
      .endAngle(3) //angle in radians

    var d_arc=d3.arc()                  // donut arc
      .innerRadius(40)               
      .outerRadius(70)
      .startAngle(0) 
      .endAngle(4) //angle in radians

    chart.append("path")
      .attr("d", arc)
      .attr("transform", "translate(200,200)")  
      .attr("fill","#00A5E3")  // setting the color      

    chart.append("path")
      .attr("d", d_arc)
      .attr("transform", "translate(200,400)")  
      .attr("fill","#FF96C5")   // setting the color

    chart.append("text")
      .text("Simple arc")
      .attr("transform", "translate(200,300)") 

    chart.append("text")
      .text("Donut arc")
      .attr("transform", "translate(200,500)")                        
    ~~~
    @import "images/Screen Shot 2021-02-20 at 12.17.40 AM.png"

## Angle Generator 
  * In order to draw arcs, we need the ```startAngle()``` and ```endAngle()```. In real-life data, we don’t have angle information associated with our data. Angle generators provide an intermediate API b/w the data and the arc generator to draw pie/donut charts 
    @import "images/Screen Shot 2021-02-20 at 12.24.26 AM.png"
    ~~~
    var margin = {top: 20, right: 20, bottom: 60, left: 80},
        width = 500 - margin.left - margin.right,
        height = 500 - margin.top - margin.bottom;

    var data = [
      {language:  "Python", value: 30},
      {language:  "Java", value: 20},
      {language:  "C/C++", value: 15},
      {language:  "Javascript", value: 35},
      {language:  "PHP", value: 15},];

    colors=["#00A5E3","#FF96C5","#00CDAC","#FFA23A","#74737A"]  

    var svg = d3.select("body") //create Svg element
      .append("svg")
      .attr('width', width + margin.right + margin.left)
      .attr('height', height + margin.top + margin.bottom)
      .style("border", "solid 1px red")
      .attr("transform","translate(200,0)");     

    var chart=svg.append('g')
      .attr('transform', 'translate(' + margin.left + ',' + margin.top + ')')
      .attr('width', width)
      .attr('height', height)

    var pie=d3.pie() 
      .value(d => d.value)

    var color_scale=d3.scaleOrdinal()
      .domain(data.map(d=>d.language))
      .range(colors)

    let arc=d3.arc()
      .outerRadius(150)
      .innerRadius(0)

    var p_chart=chart.selectAll("pie")
      .data(pie(data))
      .enter()
      .append("g")
      .attr('transform', 'translate(170,230)') 

    p_chart.append("path")
      .attr("d",arc) 
      .attr("fill",d=>{
        return color_scale(d.data.language);
      })     

    p_chart.append("text")
      .text(function(d){ return d.data.language})
      .attr("transform", function(d) { return "translate(" + arc.centroid(d) + ")";  }) 
      .style("text-anchor", "middle")  
    ~~~
    @import "images/Screen Shot 2021-02-20 at 12.28.35 AM.png"

  ## Area Chart 
  * Area charts represent quantitative data over a period of time. It's similar to a line chart, except the area between the x- and y-axis are shaded in w/ a contrasting color
  * Area charts are built using the ```d3.area()``` API 
    ~~~~
    var margin = {top: 20, right: 20, bottom: 60, left: 80},
      width = 700 - margin.left - margin.right,
      height = 700 - margin.top - margin.bottom;

    var svg = d3.select("body") //create Svg element
      .append("svg")
      .attr('width', width + margin.right + margin.left)
      .attr('height', height + margin.top + margin.bottom)
      .style("border", "solid 1px red")
      .attr("transform","translate(100,0)"); 

    var data = [
      {  date:"2020/01/01 00:00:00", patients: 600 },
      {  date:"2020/02/01 00:00:00", patients: 500 },
      {  date:"2020/03/01 00:00:00", patients: 400 },
      {  date:"2020/04/01 00:00:00", patients: 500 },
      {  date:"2020/05/01 00:00:00", patients: 300 },
      {  date:"2020/06/01 00:00:00", patients: 100 },
      {  date:"2020/07/01 00:00:00", patients: 50  },
      {  date:"2020/08/01 00:00:00", patients: 500 },
      {  date:"2020/09/01 00:00:00", patients: 550 },
      {  date:"2020/10/01 00:00:00", patients: 550 },
    ];

    data=data.map(d => ({
      date: new Date(d.date),
      patients: d.patients
      }))        

    var xscale = d3.scaleTime()
      .domain(d3.extent(data, d=>d.date))
      .range([0,width]);

    var yscale= d3.scaleLinear()                         // drawing  y scale
      .domain([0,600])
      .range([height,0])      

    var chart=svg.append('g')
      .attr('transform', 'translate(' + margin.left + ',' + margin.top + ')')
      .attr('width', width)
      .attr('height', height)

    chart.append('g')
      .call(d3.axisBottom(xscale).tickFormat(d3.timeFormat("%b")))
      .attr('transform', 'translate(0,' + height + ')')

    chart.append('g')
      .call(d3.axisLeft(yscale))

    svg.append("text")                                  // labelling x-axis
      .text("Month")          
      .attr("transform","translate(350,680)");

    svg.append("text")                                 // labelling y-axis
      .text("Number of patients")
      .attr('transform', "translate(40,400) rotate(-90)");   

    var area_generator = d3.area()
      .x(function (d) { return xscale(d.date); })
      .y0(height)
      .y1(function (d) { return yscale(d.patients); });      

    chart.append('path')
      .datum(data)
      .attr("d", area_generator)
      .attr('fill','#00A5E3')
    ~~~~
    @import "images/Screen Shot 2021-02-20 at 12.48.35 AM.png"

  ## Stacked Area Chart
  * Stacked area charts are used to represent different values over time. They are used for showing trends over time among related attributes. If there are multiple related attributes, they are stacked on top of each other  
  * D3 provides a stack generator API with ```d3.stack()``` 
  ~~~
  var margin = {top: 20, right: 150, bottom: 60, left: 80},
    width = 950 - margin.left - margin.right,
    height = 700 - margin.top - margin.bottom;

  var svg = d3.select("body") //create Svg element
    .append("svg")
    .attr('width', width + margin.right + margin.left)
    .attr('height', height + margin.top + margin.bottom)
    .style("border", "solid 1px red");;

  var data = [
    {  date:"2020/01/01 00:00:00", flu_patients: 100, malaria_patients:100, dengue_patients: 10 },
    {  date:"2020/02/01 00:00:00", flu_patients: 200, malaria_patients:200,  dengue_patients: 30},
    {  date:"2020/03/01 00:00:00", flu_patients: 50, malaria_patients:150,  dengue_patients: 80},
    {  date:"2020/05/01 00:00:00", flu_patients: 70, malaria_patients:250,  dengue_patients: 90},
    {  date:"2020/06/01 00:00:00", flu_patients: 100, malaria_patients:300,  dengue_patients: 100},
    {  date:"2020/07/01 00:00:00", flu_patients: 150,  malaria_patients:150,   dengue_patients: 120},
    {  date:"2020/08/01 00:00:00", flu_patients: 200,malaria_patients:140,  dengue_patients: 70},
    {  date:"2020/09/01 00:00:00", flu_patients: 300,malaria_patients:80, dengue_patients: 60},
    {  date:"2020/10/01 00:00:00", flu_patients: 250, malaria_patients:70, dengue_patients: 50},
  ];   

  data=data.map(d => ({
    date: new Date(d.date),
    flu_patients: d.flu_patients,
    malaria_patients: d.malaria_patients,
    dengue_patients: d.dengue_patients
  }))  
    
  var stack=d3.stack().keys(["flu_patients", "malaria_patients", "dengue_patients"]);

  var colors=["#00A5E3", "#FF96C5", "#00CDAC"]; 
  var s_data=stack(data);    

  var xscale = d3.scaleTime()
    .domain(d3.extent(data, d=>d.date))
    .range([0,width]);

  // drawing  y scale
  var yscale= d3.scaleLinear()
    .domain([0,d3.max(s_data[s_data.length-1],function(d){ return d[1]})])                        
    .range([height,0])     

  var chart=svg.append('g')
    .attr('transform', 'translate(' + margin.left + ',' + margin.top + ')')
    .attr('width', width)
    .attr('height', height)  

  var area_generator = d3.area()
    .x(function (d) { return xscale(d.data.date); })
    .y0(function (d) { return yscale(d[0]);})
    .y1(function (d) { return yscale(d[1]); }); 

  var p_chart=chart.selectAll("area")
    .data(s_data)
    .enter()
    .append("g")

  p_chart.append("path")
    .attr("fill",function(d,i){ return colors[i]})
    .attr("d",area_generator) 

  chart.append('g')
    .call(d3.axisBottom(xscale).tickFormat(d3.timeFormat("%b")))
    .attr('transform', 'translate(0,' + height + ')')

  chart.append('g')
    .call(d3.axisLeft(yscale))

  // labelling x-axis  
  svg.append("text")      
    .text("Month")          
    .attr("transform","translate(350,680)");

  // labelling y-axis
  svg.append("text")         
      .text("Number of patients")
      .attr('transform', "translate(40,400) rotate(-90)"); 

  //Draw rectangle
  chart.append("rect") 
    .attr("x", 740)
    .attr("y", 50)
    .attr("height", 10)
    .attr("width", 15)
    .attr("fill", "#00A5E3")

  // labelling x-axis
  chart.append("text")            
    .text("Flu_patients")          
    .attr("transform","translate(760,60)");

  chart.append("rect") //Draw rectangle
    .attr("x", 740)
    .attr("y", 70)
    .attr("height", 10)
    .attr("width", 15)
    .attr("fill", "#FF96C5")

  // labelling x-axis
  chart.append("text")           
    .text("Malaria_patients")          
    .attr("transform","translate(760,80)");

  //Draw rectangle
  chart.append("rect") 
    .attr("x", 740)
    .attr("y", 90)
    .attr("height", 10)
    .attr("width", 15)
    .attr("fill", "#00CDAC")

  // labelling x-axis  
  chart.append("text")            
    .text("Dengue_patients")          
    .attr("transform","translate(760,100)");
  ~~~
  @import "images/Screen Shot 2021-02-20 at 1.35.30 AM.png"

  ## Bar Chart 
  * Bar charts/graphs are used to represent categorical data w/ rectangular bars of varyin heights
    ~~~
    var margin = {top: 20, right: 150, bottom: 60, left: 80},
      width = 700 - margin.left - margin.right,
      height = 600 - margin.top - margin.bottom;

    //create Svg element
    var svg = d3.select("body") 
      .append("svg")
      .attr('width', width + margin.right + margin.left)
      .attr('height', height + margin.top + margin.bottom)
      .style("border", "solid 1px red")

    var data = [
      { grade: "A", num_students: 8},
      { grade: "A-", num_students: 12},
      { grade: "B+", num_students: 20},
      { grade: "B", num_students: 25},
      { grade: "B-", num_students: 20},
      { grade: "C+", num_students: 10},
      { grade: "F", num_students: 5 },
    ]                  

    var x = d3.scaleBand()
      .domain(data.map(d => d.grade))
      .range([0, width])
      .padding(0.2);

    var y = d3.scaleLinear()
      .domain([0,d3.max(data,d=> d.num_students)])
      .range([height, 0]);    

    var chart=svg.append('g')
      .attr('transform', 'translate(' + margin.left + ',' + margin.top + ')')
      .attr('width', width)
      .attr('height', height)  

    chart.append('g')
      .call(d3.axisLeft(y))

    chart.append('g')
      .call(d3.axisBottom(x))
      .attr('transform', 'translate(0,' + height + ')')

    chart.selectAll('rect')
      .data(data)
      .enter()
      .append('rect')
      .attr('width', x.bandwidth)
      .attr('height', d => height - y(d.num_students))
      .attr('x', d => x(d.grade))
      .attr('y', d => y(d.num_students))
      .attr('fill','#00A5E3');

    // labelling x-axis 
    svg.append("text")                                  
      .text("Grades")          
      .attr("transform","translate(250,570)");

    // labelling y-axis
    svg.append("text")                                 
      .text("Num_students")
      .attr('transform', "translate(50,270) rotate(-90)");  
    ~~~

  ## Nodes and Links
  * Nodes represent singular pieces of data, while links are display the relationships between that data 
  * In order to generate the links between nodes, we need to have access to the node's position data
    * D3 provides a ```d3.forceSimulation()``` API to force positioning between elements 
      * ```forceManyBody()``` - all elements repel one another 
      * ```forceCenter()``` - elements are attracted to the center of gravity
  ~~~
    var margin = {top: 20, right: 150, bottom: 60, left: 80},
      width =300 - margin.left - margin.right,
      height =300 - margin.top - margin.bottom;
    var data={
      "nodes": [
        {"id": "Alex"},
        {"id": "Brandon"},
        {"id": "Camilieo"},
        {"id": "Grace"},
        {"id": "Sarah"},
      ],
      "links": [
        {"source": "Alex", "target": "Camilieo"},
        {"source": "Grace", "target": "Camilieo"},
        {"source": "Sarah", "target": "Alex"},
        {"source": "Alex", "target": "Grace"},
        {"source": "Camilieo", "target": "Brandon"} 
      ]
    }
    var simulation = d3.forceSimulation(data.nodes)
      .force("link",d3.forceLink(data.links).id(function(d) {return d.id;}))
      .force("charge", d3.forceManyBody().strength(-300))
      .force("center", d3.forceCenter(width + 70 , height/2))
      .on("tick", ticked);

    var svg = d3.select("body") //create Svg element
        .append("svg")
        .attr('width', width + margin.right + margin.left)
        .attr('height', height + margin.top + margin.bottom)
        .style("border", "solid 1px red")

    var link = svg.append("g")
      .selectAll("line")
      .data(data.links)
      .enter()
      .append("line")
      .attr("stroke-width",7)
      .style('stroke','#FF96C5');

    var node = svg.append("g")
      .selectAll("circle")
      .data(data.nodes)
      .enter()
      .append("circle")
      .attr("r", 10)
      .attr("fill","#00A5E3")

    function ticked() {
      link.attr("x1", function(d) {return d.source.x;})
        .attr("y1", function(d) {return d.source.y;})
        .attr("x2", function(d) {return d.target.x;})
        .attr("y2", function(d) {return d.target.y;});

      node.attr("cx", function(d) {return d.x;})
        .attr("cy", function(d) {return d.y;});
    } 
  ~~~

  ## Treemap 
  * A treemap is a form of a hierarchical data that is displayed as a set of nested rectangles 
  ~~~
  var margin = {top: 20, right: 150, bottom: 60, left: 80},
    width =400 - margin.left - margin.right,
    height =400 - margin.top - margin.bottom

  var data={
    name:"world",
    children:
    [   
      {   
        name:"Asia",
        children:[{ name:"China", population:250 },{ name:"India", population:150 }]
      },
      {
        name:"Europe",
        children: [{ name:"UK", population:68 },{ name:"France", population:65 }]
      },
      {   
        name:"North america",
        children:[{ name:"USA", population:120 },{ name:"Canada", population:50 }]
      }
    ]
  }

  var scale=d3.scaleOrdinal(["#00A5E3","#FF96C5","#00CDAC"])

  //create Svg element
  var svg = d3.select("body") 
    .append("svg")
    .attr('width', width + margin.right + margin.left)
    .attr('height', height + margin.top + margin.bottom)
    .style("border", "solid 1px red")

  var treemap = d3.treemap()
    .size([400,400])
    .paddingInner(2)

  var c_data = d3.hierarchy(data)

  c_data.sum(d => d.population)

  let cell = svg.selectAll('tree')
    .data(treemap(c_data).leaves())
    .enter()
    .append('g')
    .attr("transform",d => 'translate('+[d.x0, d.y0]+')')

  cell.append('rect')
    .attr("width",d=> d.x1 - d.x0)
    .attr("height",d=> d.y1 - d.y0)
    .attr("fill",d => scale(d.parent.data.name))

  cell.append('text')
    .text(d => d.data.name)
    .attr("alignment-baseline", "hanging")
  ~~~

  @import "images/Screen Shot 2021-02-20 at 2.37.11 AM.png"

  ## Data Interactivity
  * You can make the graphs interactive by enablin **event listeners** that call functions every time the user interacts with the visualization
    * ```mouseover``` -  Cursor is moved onto the element that has the listener attached.
    * ```mouseout``` -  Cursor is moved off the element that has the listener attached.
    * ```wheel``` -  Wheel button of a mouse is rotated in any direction.
    * ```keydown``` -  Any key is pressed

  ## Tooltips 
  * Tooltips are interactive data cards that show up when the user hovers over a piece of data

    ~~~~
    var margin = {top: 20, right: 150, bottom: 60, left: 80},
        width =250 - margin.left - margin.right,
        height =250 - margin.top - margin.bottom;
    var data={
      "nodes": [
        {id: "Alex"},
        {id: "Brandon"},
        {id: "Camilieo"},
        {id: "Grace"},
        {id: "Sarah"},
      ],
      "links": [
        {"source": "Alex", "target": "Camilieo"},
        {"source": "Grace", "target": "Camilieo"},
        {"source": "Sarah", "target": "Alex"},
        {"source": "Alex", "target": "Grace"},
        {"source": "Camilieo", "target": "Brandon"} 
      ]
    }
    var tooltip = d3.select("body")
      .append("div")
      .style("position", "absolute")
      .style("visibility", "hidden")
      .style("color", "white")
      .style("background-color", "black")
      .style("padding", "8px")
      .text("tooltip");

    var simulation = d3.forceSimulation(data.nodes)
      .force("link",d3.forceLink(data.links).id(function(d) {return d.id;}))
      .force("charge", d3.forceManyBody().strength(-300))
      .force("center", d3.forceCenter(width + 100 , height ))
      .on("tick", ticked)      

    //create Svg element             
    var svg = d3.select("body") 
      .append("svg")
      .attr('width', width + margin.right + margin.left)
      .attr('height', height + margin.top + margin.bottom)
      .style("border", "solid 1px red");   

    var link = svg.append("g")
      .selectAll("line")
      .data(data.links)
      .enter()
      .append("line")
      .attr("stroke-width",7)
      .style('stroke','#FF96C5');

    var node = svg.append("g")
      .selectAll("circle")
      .data(data.nodes)
      .enter()
      .append("circle")
      .attr("r", 10)
      .attr("fill","#00A5E3")
      .on("mouseover", function(d) {
        tooltip.text(d.id);
        tooltip.style("visibility", "visible");
      })
      .on("mouseout", function(){
        return tooltip.style("visibility", "hidden");}); 
              
    function ticked() {
      link.attr("x1", function(d) {return d.source.x;})
        .attr("y1", function(d) {return d.source.y;})
        .attr("x2", function(d) {return d.target.x;})
        .attr("y2", function(d) {return d.target.y;});
      node.attr("cx", function(d) {return d.x;})
        .attr("cy", function(d) {return d.y;});
    } 
    ~~~~
    @import "images/Screen Shot 2021-02-20 at 2.43.58 AM.png"

.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.