---
title: 'Creating An Interactive Gantt Chart Component With Vanilla JavaScript (Part 1)'
slug: interactive-gantt-chart-component-vanilla-javascript
author: anna-prenzel
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bcf1248-c58e-47f4-a94f-3cbac5c60b45/interactive-gantt-chart-component-vanillajs.jpg
date: 2021-08-18T08:00:00.000Z
summary: >-
  With a Gantt chart, you can visualize schedules and assign tasks. In this article, we will code a Gantt chart as a reusable Web component. We will focus on the architecture of the component, rendering the calendar with CSS Grid and managing the state of the draggable tasks with JavaScript Proxy Objects.
description: >-
  In this article, we will code a Gantt chart as a reusable Web component. We will focus on the architecture of the component, rendering the calendar with CSS Grid and managing the state of the draggable tasks with JavaScript Proxy Objects.
categories:
  - JavaScript
  - Frameworks
  - CSS
  - Tools
---

If you work with time data in your app, a graphical visualization as a calendar or Gantt chart is often very useful. At first glance, developing your own chart component seems quite complicated. Therefore, in this article, I will develop the foundation for a **Gantt chart component** whose appearance and functionality you can customize for any use case.

These are the **basic features of the Gantt chart** that I would like to implement:

- The user can choose between two views: year/month or month/day.
- The user can define the planning horizon by selecting a start date and an end date.
- The chart renders a given list of jobs that can be moved by drag and drop. The changes are reflected in the state of the objects.
- 
Below you can see the resulting Gantt chart in both views. In the monthly version, I have included three jobs as an example.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d1f6492-473b-4bff-b5fd-625f2b31251a/1-interactive-gantt-chart-component-vanillajs.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d1f6492-473b-4bff-b5fd-625f2b31251a/1-interactive-gantt-chart-component-vanillajs.jpg" width="800" height="166" sizes="100vw" caption="Gantt chart with the month view. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d1f6492-473b-4bff-b5fd-625f2b31251a/1-interactive-gantt-chart-component-vanillajs.jpg'>Large preview</a>)" alt="Gantt chart with the month view" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be156828-3af2-4885-a520-4c62b1c71356/2-interactive-gantt-chart-component-vanillajs.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be156828-3af2-4885-a520-4c62b1c71356/2-interactive-gantt-chart-component-vanillajs.PNG" width="800" height="158" sizes="100vw" caption="Gantt chart with the day view. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be156828-3af2-4885-a520-4c62b1c71356/2-interactive-gantt-chart-component-vanillajs.PNG'>Large preview</a>)" alt="Gantt chart with the day view" >}}

Below you can see the resulting Gantt chart in both views. In the monthly version, I have included three jobs as an example.

### Sample Files And Instructions For Running The Code

You can find the **full code snippets** of this article in the following files:

- [index.html](https://drive.google.com/file/d/1_sU8iuB6e8Dvp2wfeBFSlj_klW9Avmh9/view?usp=sharing)
- [index.js](https://drive.google.com/file/d/1qCTn3-2AV78frvkd_pASu0v-SYgLIy7U/view?usp=sharing)
- [VanillaGanttChart.js](https://drive.google.com/file/d/1KVKT7AA65wmF5l68MHPsKPCy31Kj4RVZ/view?usp=sharing)
- [YearMonthRenderer.js](https://drive.google.com/file/d/10N0EV_-5PO2FbupE3mn18xTWiRIKaKP3/view?usp=sharing)
- [DateTimeRenderer.js](https://drive.google.com/file/d/1k_TYNzg9NJmAcDI8YCGJ166SIqp4OTDs/view?usp=sharing).

Since the code contains JavaScript modules, you can only run the example from an **HTTP server** and not from the local file system. For testing on your local PC, I’d recommend the module [live-server](https://www.npmjs.com/package/live-server), which you can install via npm. 

Alternatively, you can [try out the example here directly in your browser](https://blaustern.eu/gantt-chart/) without installation.

{{% feature-panel %}}

## Basic Structure Of The Web Component

I decided to implement the Gantt chart as a web component. This allows us to create a **custom HTML element**, in my case `<gantt-chart></gantt-chart>`, which we can easily reuse anywhere on any HTML page.

You can find some basic information about developing web components in the [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/Web_Components). The following listing shows the structure of the component. It is inspired by the “counter” example from [Alligator.io](https://alligator.io/web-components/attributes-properties/).

The component defines a **template** containing the HTML code needed to display the Gantt chart. For the complete CSS specifications, please refer to the sample files. The specific selection fields for year, month or date cannot be defined here yet, as they depend on the selected level of the view.

The selection elements are projected in by one of the two **renderer classes** instead. The same applies to the rendering of the actual Gantt chart into the element with the ID `gantt-container`, which is also handled by the responsible renderer class.

The class `VanillaGanttChart` now describes the behavior of our new HTML element. In the constructor, we first define our rough template as the [shadow DOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM) of the element.

The component must be initialized with **two arrays**, `jobs`, and `resources`. The `jobs` array contains the tasks that are displayed in the chart as movable green bars. The `resources` array defines the individual rows in the chart where tasks can be assigned. In the screenshots above, for example, we have 4 resources labeled *Task 1* to *Task 4*. The resources can therefore represent the individual tasks, but also people, vehicles, and other physical resources, allowing for a variety of use cases.

Currently, the `YearMonthRenderer` is used as the **default renderer**. As soon as the user selects a different level, the renderer is changed in the `changeLevel` method: First, the renderer-specific DOM elements and listeners are deleted from the Shadow DOM using the `clear` method of the old renderer. Then the new renderer is initialized with the existing jobs and resources and the rendering is started.

<pre><code class="language-javascript">import {YearMonthRenderer} from './YearMonthRenderer.js';
import {DateTimeRenderer} from './DateTimeRenderer.js';

const template = document.createElement('template');

template.innerHTML = 
 `&lt;style&gt; … &lt;/style&gt;

  &lt;div id="gantt-settings"&gt;

    &lt;select name="select-level" id="select-level"&gt;
      &lt;option value="year-month"&gt;Month / Day&lt;/option&gt;
      &lt;option value="day"&gt;Day / Time&lt;/option&gt;
    &lt;/select&gt;

    &lt;fieldset id="select-from"&gt;
      &lt;legend&gt;From&lt;/legend&gt;
    &lt;/fieldset&gt;

    &lt;fieldset id="select-to"&gt;
      &lt;legend&gt;To&lt;/legend&gt;
    &lt;/fieldset&gt;
  &lt;/div&gt;

  &lt;div id="gantt-container"&gt;
  &lt;/div&gt;`;

export default class VanillaGanttChart extends HTMLElement {

    constructor() {
      super();
      this.attachShadow({ mode: 'open' });
      this.shadowRoot.appendChild(template.content.cloneNode(true));
      this.levelSelect = this.shadowRoot.querySelector('#select-level');
    }
 
    _resources = [];
    _jobs = [];
    _renderer;

    set resources(list){…}
    get resources(){…}
    set jobs(list){…}
    get jobs(){…}
    get level() {…}
    set level(newValue) {…} 
    get renderer(){…}
    set renderer(r){…}

    connectedCallback() {
      this.changeLevel = this.changeLevel.bind(this);

      this.levelSelect.addEventListener('change', this.changeLevel);
      this.level = "year-month";   

      this.renderer = new YearMonthRenderer(this.shadowRoot);
      this.renderer.dateFrom = new Date(2021,5,1);
      this.renderer.dateTo = new Date(2021,5,24);
      this.renderer.render();
    }

    disconnectedCallback() {  
      if(this.levelSelect)
        this.levelSelect.removeEventListener('change', this.changeLevel);
      if(this.renderer)
        this.renderer.clear();
    }

    changeLevel(){
      if(this.renderer)
        this.renderer.clear();

      var r;   

      if(this.level == "year-month"){
        r = new YearMonthRenderer(this.shadowRoot);    
      }else{
        r = new DateTimeRenderer(this.shadowRoot);
      }

      r.dateFrom = new Date(2021,5,1);
      r.dateTo = new Date(2021,5,24);
      r.resources = this.resources;
      r.jobs = this.jobs;
      r.render();
      this.renderer = r;
    }
  }
 
  window.customElements.define('gantt-chart', VanillaGanttChart);</code></pre>

Before we get deeper into the rendering process, I would like to give you an overview of the connections between the different scripts:

- **index.html** is your web page where you can use the tag `<gantt-chart></gantt-chart>`
- **index.js** is a script in which you initialize the instance of the web component that is associated with the Gantt chart used in index.html with the appropriate jobs and resources (of course you can also use multiple Gantt charts and thus multiple instances of the web component)
- The component **`VanillaGanttChart`** delegates rendering to the two renderer classes `YearMonthRenderer` and `DateTimeRenderer`.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f80bf86-6f3c-4e82-83c3-d944018be93a/3-interactive-gantt-chart-component-vanillajs.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f80bf86-6f3c-4e82-83c3-d944018be93a/3-interactive-gantt-chart-component-vanillajs.jpg" width="800" height="241" sizes="100vw" caption="Component architecture of our Gantt chart example. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f80bf86-6f3c-4e82-83c3-d944018be93a/3-interactive-gantt-chart-component-vanillajs.jpg'>Large preview</a>)" alt="Component architecture of our Gantt chart example" >}}

{{% ad-panel-leaderboard %}}

## Rendering Of The Gantt chart With JavaScript And CSS Grid

In the following, we discuss the **rendering process** using the `YearMonthRenderer` as an example. Please note that I have used a so-called [constructor function](https://www.javascripttutorial.net/javascript-constructor-function/) instead of the `class` keyword to define the class. This allows me to distinguish between public properties (`this.render` and `this.clear`) and private variables (defined with `var`).

The rendering of the chart is broken down into several sub-steps:

1. `initSettings`  
Rendering of the controls which are used to define the planning horizon.
2. `initGantt`  
Rendering of the Gantt chart, basically in four steps: 
  - `initFirstRow` (draws 1 row with month names)
  - `initSecondRow` (draws 1 row with days of the month)
  - `initGanttRows` (draws 1 row for each resource with grid cells for each day of the month)
  - `initJobs` (positions the draggable jobs in the chart)

<pre><code class="language-javascript">export function YearMonthRenderer(root){

    var shadowRoot = root;
    var names = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];    
 
    this.resources=[];
    this.jobs = [];
 
    this.dateFrom = new Date();
    this.dateTo = new Date();

    //select elements
    var monthSelectFrom;
    var yearSelectFrom;
    var monthSelectTo;
    var yearSelectTo;

    var getYearFrom = function() {…}
    var setYearFrom = function(newValue) {…}

    var getYearTo = function() {…}
    var setYearTo = function(newValue) {…}

    var getMonthFrom = function() {…}
    var setMonthFrom = function(newValue) {…}

    var getMonthTo = function() {…}
    var setMonthTo = function(newValue) {…}  

    this.render = function(){
      this.clear();
      initSettings();
      initGantt();
    }

    //remove select elements and listeners, clear gantt-container 
    this.clear = function(){…}

    //add HTML code for the settings area (select elements) to the shadow root, initialize associated DOM elements and assign them to the properties monthSelectFrom, monthSelectTo etc., initialize listeners for the select elements
    var initSettings = function(){…}

    //add HTML code for the gantt chart area to the shadow root, position draggable jobs in the chart
    var initGantt = function(){…}

    //used by initGantt: draw time axis of the chart, month names
    var initFirstRow = function(){…}

    //used by initGantt: draw time axis of the chart, days of month
    var initSecondRow = function(){…}

    //used by initGantt: draw the remaining grid of the chart
    var initGanttRows = function(){…}.bind(this);

    //used by initGantt: position draggable jobs in the chart cells
    var initJobs = function(){…}.bind(this);    

   //drop event listener for jobs
   var onJobDrop = function(ev){…}.bind(this);

   //helper functions, see example files
   ...
}</code></pre>

### Rendering The Grid

I recommend CSS Grid for drawing the diagram area because it makes it very easy to create **multi-column layouts** that adapt dynamically to the screen size. 

In the first step, we have to determine the **number of columns** of the grid. In doing so, we refer to the first row of the chart which (in the case of the `YearMonthRenderer`) represents the individual months. 

Consequently, we need:

- one column for the names of the resources, e.g. with a fixed width of 100px.
- one column for each month, of the same size and using the full space available.

This can be achieved with the setting `100px repeat(${n_months}, 1fr)` for the property `gridTemplateColumns` of the chart container. 

This is the initial part of the `initGantt` method:

<pre><code class="language-javascript">var container = shadowRoot.querySelector("#gantt-container");
container.innerHTML = "";

var first_month = new Date(getYearFrom(), getMonthFrom(), 1);
var last_month = new Date(getYearTo(), getMonthTo(), 1);
 
//monthDiff is defined as a helper function at the end of the file
var n_months =  monthDiff(first_month, last_month)+1;
 
container.style.gridTemplateColumns = `100px repeat(${n_months},1fr)`;</code></pre>

In the following picture you can see a chart for two months with `n_months=2`:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/054cd439-58bd-44cf-b54a-e56f647400bc/4-interactive-gantt-chart-component-vanillajs.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73076bcc-a5f7-4bdd-943a-66f37bcb8034/chart-2-months.png" width="763" height="247" sizes="100vw" caption="The chart for 2 months, set with <code>n_months=2</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/054cd439-58bd-44cf-b54a-e56f647400bc/4-interactive-gantt-chart-component-vanillajs.PNG'>Large preview</a>)" alt="" >}}

After we have defined the outer columns, we can start **filling the grid**. Let's stay with the example from the picture above. In the first row, I insert 3 `div`s with the classes `gantt-row-resource` and `gantt-row-period`. You can find them in the following snippet from the DOM inspector. 

In the second row, I use the same three `div`s to keep the vertical alignment. However, the month `div`s get child elements for the individual days of the month.

<pre class="language-markup"><code>&lt;div id="gantt-container"
  style="grid-template-columns: 100px repeat(2, 1fr);"&gt;
  &lt;div class="gantt-row-resource"&gt;&lt;/div&gt;
  &lt;div class="gantt-row-period"&gt;Jun 2021&lt;/div&gt;
  &lt;div class="gantt-row-period"&gt;Jul 2021&lt;/div&gt;
  &lt;div class="gantt-row-resource"&gt;&lt;/div&gt;
  &lt;div class="gantt-row-period"&gt;
    &lt;div class="gantt-row-period"&gt;1&lt;/div&gt;
    &lt;div class="gantt-row-period"&gt;2&lt;/div&gt;
    &lt;div class="gantt-row-period"&gt;3&lt;/div&gt;
    &lt;div class="gantt-row-period"&gt;4&lt;/div&gt;
    &lt;div class="gantt-row-period"&gt;5&lt;/div&gt;
    &lt;div class="gantt-row-period"&gt;6&lt;/div&gt;
    &lt;div class="gantt-row-period"&gt;7&lt;/div&gt;
    &lt;div class="gantt-row-period"&gt;8&lt;/div&gt;
    &lt;div class="gantt-row-period"&gt;9&lt;/div&gt;
    &lt;div class="gantt-row-period"&gt;10&lt;/div&gt;
  ...
  &lt;/div&gt;
  ...
&lt;/div&gt;
</code></pre>  

For the child elements to be arranged horizontally as well, we need the setting `display: grid` for the class `gantt-row-period`. In addition, we do not know exactly how many columns are required for the individual months (28, 30, or 31). Therefore, I use the setting `grid-auto-columns`. With the value `minmax(20px, 1fr);` I can ensure that a minimum width of 20px is maintained and that otherwise the available space is fully utilized:

<pre><code class="language-css">#gantt-container {
  display: grid;
}

.gantt-row-resource {
  background-color: whitesmoke;
  color: rgba(0, 0, 0, 0.726);
  border: 1px solid rgb(133, 129, 129);
  text-align: center;
}

.gantt-row-period {
  display: grid;
  grid-auto-flow: column;
  grid-auto-columns: minmax(20px, 1fr);
  background-color: whitesmoke;
  color: rgba(0, 0, 0, 0.726);
  border: 1px solid rgb(133, 129, 129);
  text-align: center;
}</code></pre>

The remaining rows are generated according to the second row, however as **empty cells**.

Here is the JavaScript code for generating the individual grid cells of the first row. The methods `initSecondRow` and `initGanttRows` have a similar structure.

<pre><code class="language-javascript">var initFirstRow = function(){

  if(checkElements()){
        var container = shadowRoot.querySelector("#gantt-container");

        var first_month = new Date(getYearFrom(), getMonthFrom(), 1);
        var last_month = new Date(getYearTo(), getMonthTo(), 1);
 
        var resource = document.createElement("div");
        resource.className = "gantt-row-resource";
        container.appendChild(resource);   
 
        var month = new Date(first_month);

        for(month; month &lt;= last_month; month.setMonth(month.getMonth()+1)){    
          var period = document.createElement("div");
          period.className = "gantt-row-period";
          period.innerHTML = names[month.getMonth()] + " " + month.getFullYear();
          container.appendChild(period);
        }
  }
}</code></pre>

### Rendering The Jobs

Now each `job` has to be drawn into the diagram at the **correct position**. For this I make use of the HTML data attributes: every grid cell in the main chart area is associated with the two attributes `data-resource` and `data-date` indicating the position on the horizontal and vertical axis of the chart (see function `initGanttRows` in the files `YearMonthRenderer.js` and `DateTimeRenderer.js`).

As an example, let's look at the **first four grid cells** in the first row of the chart (we are still using the same example as in the pictures above):

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8eaf9c3-f594-41e2-afa0-1a4ed3ee10a9/6-interactive-gantt-chart-component-vanillajs.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8eaf9c3-f594-41e2-afa0-1a4ed3ee10a9/6-interactive-gantt-chart-component-vanillajs.PNG" width="229" height="49" sizes="100vw" caption="Focusing on the first four grid cells in the first row of the chart. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8eaf9c3-f594-41e2-afa0-1a4ed3ee10a9/6-interactive-gantt-chart-component-vanillajs.PNG'>Large preview</a>)" alt="" >}}

In the DOM inspector you can see the values of the data attributes that I have assigned to the individual cells:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06e65da7-ef17-4f28-aa4b-dbba36acb02f/7-interactive-gantt-chart-component-vanillajs.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06e65da7-ef17-4f28-aa4b-dbba36acb02f/7-interactive-gantt-chart-component-vanillajs.PNG" width="800" height="83" sizes="100vw" caption="The values for the data attributes are assigned. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06e65da7-ef17-4f28-aa4b-dbba36acb02f/7-interactive-gantt-chart-component-vanillajs.PNG'>Large preview</a>)" alt="" >}}

Let's now see what this means for the function `initJobs`. With the help of the function `querySelector`, it is now quite easy to find the grid cell into which a job should be placed.

The next challenge is to determine the correct width for a `job` element. Depending on the selected view, each grid cell represents a **unit of one day** (level `month/day`) or one hour (level `day/time`). Since each job is the child element of a cell, the `job` duration of 1 unit (day or hour) corresponds to a width of `1*100%`, the duration of 2 units corresponds to a width of `2*100%`, and so on. This makes it possible to use the CSS `calc` function to **dynamically set the width of a `job` element**, as shown in the following listing.

<pre><code class="language-javascript">var initJobs = function(){

    this.jobs.forEach(job =&gt; {

        var date_string = formatDate(job.start);

        var ganttElement = shadowRoot.querySelector(`div[data-resource="${job.resource}"][data-date="${date_string}"]`);

        if(ganttElement){

          var jobElement = document.createElement("div");
          jobElement.className="job";
          jobElement.id = job.id;

          //helper function dayDiff - get difference between start and end in days
          var d = dayDiff(job.start, job.end);           
          
          //d --> number of grid cells covered by job + sum of borderWidths
          jobElement.style.width = "calc("+(d*100)+"% + "+ d+"px)";
          jobElement.draggable = "true";

          jobElement.ondragstart = function(ev){
              //the id is used to identify the job when it is dropped
              ev.dataTransfer.setData("job", ev.target.id); 
          };

          ganttElement.appendChild(jobElement);
        }
    });
  }.bind(this);</code></pre>

In order to make a `job` **draggable**, there are three steps required:

- Set the property `draggable` of the job element to `true` (see listing above).
- Define an event handler for the event `ondragstart` of the job element (see listing above).
- Define an event handler for the event `ondrop` for the grid cells of the Gantt chart, which are the possible drop targets of the job element (see function `initGanttRows` in the file `YearMonthRenderer.js`).

The event handler for the event `ondrop` is defined as follows:

<pre><code class="language-javascript">var onJobDrop = function(ev){
 
      // basic null checks
      if (checkElements()) {
 
        ev.preventDefault(); 
 
        // drop target = grid cell, where the job is about to be dropped
        var gantt_item = ev.target;
        
        // prevent that a job is appended to another job and not to a grid cell
        if (ev.target.classList.contains("job")) {
          gantt_item = ev.target.parentNode;
        }
        
        // identify the dragged job
        var data = ev.dataTransfer.getData("job");               
        var jobElement = shadowRoot.getElementById(data);  
        
        // drop the job
        gantt_item.appendChild(jobElement);
 
        // update the properties of the job object
        var job = this.jobs.find(j =&gt; j.id == data );
 
        var start = new Date(gantt_item.getAttribute("data-date"));
        var end = new Date(start);
        end.setDate(start.getDate()+dayDiff(job.start, job.end));
 
        job.start = start;
        job.end = end;
        job.resource = gantt_item.getAttribute("data-resource");
      }
    }.bind(this);</code></pre>
    
 All changes to the job data made by drag and drop are thus reflected in the list `jobs` of the Gantt chart component.

{{% ad-panel-leaderboard %}}

## Integrating The Gantt Chart Component In Your Application

You can use the tag `<gantt-chart></gantt-chart>` anywhere in the HTML files of your application (in my case in the file `index.html`) under the following conditions: 

- The script `VanillaGanttChart.js` must be integrated as a module so that the tag is interpreted correctly.
- You need a separate script in which the Gantt chart is initialized with `jobs` and `resources` (in my case the file `index.js`).

<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
 &lt;head&gt;
   &lt;meta charset="UTF-8"/&gt;
   &lt;title&gt;Gantt chart - Vanilla JS&lt;/title&gt;
   &lt;script type="module" src="VanillaGanttChart.js"&gt;&lt;/script&gt;   
 &lt;/head&gt;
    
 &lt;body&gt;
 
  &lt;gantt-chart id="g1"&gt;&lt;/gantt-chart&gt; 
 
  &lt;script type="module" src="index.js">&lt;/script&gt;
 &lt;/body&gt; 
&lt;/html&gt;</code></pre>

For example, in my case the file `index.js` looks as follows:

<pre><code class="language-javascript">import VanillaGanttChart from "./VanillaGanttChart.js";
 
var chart = document.querySelector("#g1");
 
chart.jobs = [
    {id: "j1", start: new Date("2021/6/1"), end: new Date("2021/6/4"), resource: 1},
    {id: "j2", start: new Date("2021/6/4"), end: new Date("2021/6/13"), resource: 2},
    {id: "j3", start: new Date("2021/6/13"), end: new Date("2021/6/21"), resource: 3},
];
 
chart.resources = [{id:1, name: "Task 1"}, {id:2, name: "Task 2"}, {id:3, name: "Task 3"}, {id:4, name: "Task 4"}];
</code></pre>

However, there is still one requirement open: when the user makes changes by dragging jobs in the Gantt chart, the respective changes in the property values of the jobs should be reflected in the list *outside* the component.

We can achieve this with the use of [JavaScript Proxy Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy): Each `job` is nested in a **proxy object**, which we provide with a so-called [validator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy#validation). It becomes active as soon as a property of the object is changed (function `set` of the validator) or retrieved (function `get` of the validator). In the set function of the validator, we can store code that is executed whenever the start time or the resource of a task is changed.

The following listing shows a different version of the file `index.js`. Now a list of proxy objects is assigned to the Gantt chart component instead of the original jobs. In the validator `set` I use a simple console output to show that I have been notified of a property change.

<pre><code class="language-javascript">import VanillaGanttChart from "./VanillaGanttChart.js";
 
var chart = document.querySelector("#g1");
 
var jobs = [
    {id: "j1", start: new Date("2021/6/1"), end: new Date("2021/6/4"), resource: 1},
    {id: "j2", start: new Date("2021/6/4"), end: new Date("2021/6/13"), resource: 2},
    {id: "j3", start: new Date("2021/6/13"), end: new Date("2021/6/21"), resource: 3},
];
var p_jobs = [];
 
chart.resources = [{id:1, name: "Task 1"}, {id:2, name: "Task 2"}, {id:3, name: "Task 3"}, {id:4, name: "Task 4"}];
 
jobs.forEach(job =&gt; {
 
    var validator = {
        set: function(obj, prop, value) {
 
          console.log("Job " + obj.id + ": " + prop + " was changed to " + value);
          console.log();
 
          obj[prop] = value;
          return true;
        },
 
        get: function(obj, prop){
 
            return obj[prop];
        }
    };
 
    var p_job = new Proxy(job, validator);
    p_jobs.push(p_job);
});
 
chart.jobs = p_jobs;</code></pre>

## Outlook

The Gantt chart is an example that shows how you can use the technologies of Web Components, CSS Grid, and JavaScript Proxy to develop a **custom HTML element** with a somewhat more complex graphical interface. You are welcome to develop the project further and/or use it in your own projects together with other JavaScript frameworks.

Again, you can find [all sample files and instructions](#sample-files-and-instructions-for-running-the-code) at the top of the article.

{{< signature "vf, yk, il" >}}
