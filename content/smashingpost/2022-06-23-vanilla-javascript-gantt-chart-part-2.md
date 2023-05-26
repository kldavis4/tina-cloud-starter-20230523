---
title: 'How To Create A Vanilla JavaScript Gantt Chart: Adding Task Editing Features (Part 2)'
slug: vanilla-javascript-gantt-chart-part-2
author: anna-prenzel
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3b4b9df-4f79-4eef-8ebc-2d1f86843d45/vanilla-javascript-gantt-chart-part-2.jpg
date: 2022-06-23T11:30:00.000Z
summary: >-
  In this article, we will enhance the Gantt Chart component with some interaction possibilities for editing the jobs. In doing so, we will continue to work with Vanilla JS and Web Components and look at some JavaScript libraries that can greatly simplify the effort of developing a fully functional Gantt Chart.
description: >-
  In this article, we will enhance the Gantt Chart component with some interaction possibilities for editing the jobs. In doing so, we will continue to work with Vanilla JS and Web Components and look at some JavaScript libraries that can greatly simplify the effort of developing a fully functional Gantt Chart.
categories:
  - JavaScript
  - Frameworks
  - Tools
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Bryntum
  link: https://www.bryntum.com?aw=smash-jun2022
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7154d16-70af-4a07-91f4-dfa5c21f21dc/bryntum.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.bryntum.com?aw=smash-jun2022">Bryntum</a> who are strong believers in the web as an application platform and provide advanced UI components and dev tools for over 5000 companies in 70+ countries. <em>Thank you!</em>
---

In [Part 1](https://www.smashingmagazine.com/2021/08/interactive-gantt-chart-component-vanilla-javascript/) of this article, we developed a web component for an interactive Gantt Chart. Now we will enhance the Gantt Chart component with some interaction possibilities for editing the jobs: the job bars are made resizable by mouse-dragging, and we also implement an editing dialogue that can be used to modify the start and end dates of a job. In doing so, we will continue to work with Vanilla JS and Web Components. In the end, we will look at some JavaScript libraries that can greatly simplify the effort of developing a fully functional Gantt Chart.

The following video shows what we are going to build in this article. First, we will add a drag handle on the right-hand side of each job that can be used for resizing the job bar (in the picture, it’s shown as a narrow gray vertical bar). In the next step, we will further extend the behavior of the jobs so that double-clicking on a job bar opens an editing dialogue.

{{< vimeo id="721411339" caption="The new interface of the Gantt Chart with job editing features" breakout="true" >}}

To follow the instructions in this article, you can use the files from the [previous article](https://www.smashingmagazine.com/2021/08/interactive-gantt-chart-component-vanilla-javascript/) as a starting point. The **source code of the finished solution** can be found in my [GitHub repository](https://github.com/aprenzel/gantt-chart-vanillajs).

Since the code contains JavaScript modules, you can only run the example from an **HTTP server** and not from the local file system. For testing on your local PC, I’d recommend the module [live-server](https://www.npmjs.com/package/live-server), which you can install via npm. 

Alternatively, you can [try out the example here directly in your browser](https://aprenzel.github.io/gantt-chart-vanillajs/) without installation.

## A Web Component For Jobs

Before we extend the functionality of jobs, we move the source code related to jobs into a separate component with the name `GanttJob`. 

The component contains setters and getters for a job object and for the selected zoom level of the Gantt Chart’s time axis (`year-month` or `day`). It renders a job as a simple `div` element `<div class="job"></div>`. The length of the job bar is calculated in the `render` function depending on the zoom level and the duration of the job.

Compared to Part 1 of this article, I have changed the styling of the jobs a bit.

**Note:** *Check some minor changes in the CSS style of the component `VanillaGanttChart`.*

<pre><code class="language-javascript">const template = document.createElement('template');
  template.innerHTML = 
   `&lt;style&gt;
       @import "./styles/GanttJob.css";
    &lt;/style&gt;
    &lt;div class="job"&gt;&lt;/div&gt;`;
  export default class GanttJob extends HTMLElement {
    constructor() {
      super();
      this.attachShadow({ mode: 'open' });
      this.shadowRoot.appendChild(template.content.cloneNode(true));
    }
    connectedCallback() {
        var jobElement = this.shadowRoot.querySelector(".job");
        jobElement.id = this.id;
        jobElement.draggable = true;
        this._render();
    }
    disconnectedCallback() { }
    update(){
      this._render();
    }
    _render(){
      var jobElement = this.shadowRoot.querySelector(".job");
      var d;
      if(this._level == "year-month"){
        d = this._dayDiff(this.job.start, this.job.end);
      }else{//_level = "day"
        d = this._hourDiff(this.job.start, this.job.end);
      }
      jobElement.style.width = `calc(${d*100}% + ${d}px)`;
    }
    _job;
    _level = "year-month";
    set job(newValue){
        this._job = newValue;
        this._render();
    } 
    get job(){
        return this._job;
    }
    set level(newValue)
      this._level = newValue;
    }
    get level(){
        return this._level;
    }
    
    //helper functions &#95;dayDiff, &#95;hourDiff; see example files
}
window.customElements.define('gantt-job', GanttJob);</code></pre>

In the class `YearMonthRenderer`, you only need to adapt the function `initJobs` for now. Instead of a simple `div` element, the custom element `gantt-job` is inserted into the Gantt grid for each job from the `jobs` array. It is initialized with the properties `id`, `job`, and `level`. Furthermore, there are no changes to the drag-and-drop implementation of the jobs within the Gantt grid.

The same changes are applied to the class `DateTimeRenderer`.

<div class="break-out">

<pre><code class="language-javascript">var initJobs = function(){
  this.jobs.forEach(job =&gt; {
      var date_string = formatDate(job.start);
      var ganttElement = shadowRoot.querySelector(`div[data-resource="${job.resource}"][data-date="${date_string}"]`);
      if(ganttElement){
        var jobElement = document.createElement("gantt-job");
        jobElement.id = job.id;
        jobElement.job = job;
        jobElement.level = "year-month";
        ganttElement.appendChild(jobElement);         
        jobElement.ondragstart = function(ev){
            ev.dataTransfer.setData("job", ev.target.id);           
        };
      }
  });
}.bind(this);</code></pre>
</div>

{{% feature-panel %}}
 
## Making Jobs Resizable

The user should be able to increase or decrease the duration of a job by dragging the right outer edge of a job bar. Furthermore, changing the duration should be possible only in steps corresponding to the size of the time segments in the currently active view. This means that if the level `year-month` is set, the duration can only be changed in steps of full days, and if the level `day` is set, the duration can only be changed in steps of full hours.

First, a drag handle is added to the right side of a job bar using CSS (see file `styles/GanttJob.css`).

<pre><code class="language-css">.job::after {
       content: '';
       background-color: #646965;
       position: absolute;
       right: 0;
       width: 4px;
       height: 100%;
       cursor: ew-resize;
}</code></pre>

To make a job resizable, the following strategy can be used:

1. Resizing starts when the user clicks on the drag handle of a job. It means we have to respond to the `mousedown` event in the Gantt chart.
2. From this point on, the job bar increases or decreases as the user moves the mouse to the left or right. This behavior can be controlled via the `mousemove` event.
3. The resizing is finished as soon as the user releases the mouse button again: once the `mouseup` event occurs.

It might be your first thought to add a `mousedown` listener to the job bar within the `GanttJob` component. However, depending on the number of jobs in the Gantt Chart, this could result in a huge number of listeners, which could affect the component’s performance. 

Therefore, in this case, I use the concept of [**event delegation**](https://javascript.info/event-delegation). Instead of installing a separate `mousedown` listener for each job, we install exactly one listener for the common parent element. In our case, this is the `div` element with the ID `gantt-container`, which contains the complete Gantt Chart.

You can add the following code to the file `YearMonthRenderer.js`:

<div class="break-out">

<pre><code class="language-javascript">var makeJobsResizable = function(){
    if(checkElements()){
      var container = shadowRoot.querySelector("#gantt-container");        
      container.addEventListener("mousedown", _handleMouseDown, false);
    }
 }.bind(this);


 var &#95;handleMouseDown = function(e){
    if(e.target.tagName == "GANTT-JOB"){
       this.selectedJobElement = e.target;
       if(this.selectedJobElement.isMouseOverDragHandle(e)){            
          this.selectedJob = this.jobs.find(j =&gt; j.id == e.target.id);          
          document.addEventListener("mousemove", &#95;handleMouseMove, false);
          document.addEventListener("mouseup", &#95;handleMouseUp, false);
          //use this to disable drag and drop behavior in resize mode
       e.preventDefault();
       }
    }
}.bind(this);
</code></pre>
</div>

The `mousedown` handler checks whether the user has clicked on a `GanttJob` element. If this is the case, it must still be checked whether the user has clicked on the drag handle. Only then the `mousemove` and `mouseup` listeners are installed for the duration of the resize operation.

In the file `GanttJob.js`, the function `isMouseOverDragHandle` is added:

<div class="break-out">

<pre><code class="language-javascript">isMouseOverDragHandle = function(e){
      var panel = this.shadowRoot.querySelector(".job");
      var current_width = parseInt(getComputedStyle(panel, '').width);
      if (e.offsetX &gt;= (current_width - this._HANDLE_SIZE)) {
        return true;
      }
      return false;
}.bind(this);
//should match the width setting of the drag handle in the file "GanttJob.css" _HANDLE_SIZE = 4;</code></pre>
</div>

The remaining handler functions are now added to the file `YearMonthRenderer.js`. 

In the handler `_handleMouseMove`, we first need to check which section of the Gantt Chart the mouse cursor is currently over. The corresponding `gantt-item` tells us the new end date of the job through the attribute `data-date`. By calling the `update` function of the selected `GanttJob` element, we update the length of the job bar. 

As you can see in the `render` function of the `GanttJob` component, the length is modified only in steps corresponding to the size of the time sections of the Gantt Chart.

In the handler `_handleMouseUp`, the selection of the job is cleared, and the `mousemove` listener is removed.

<div class="break-out">

<pre><code class="language-javascript">var _handleMouseMove = function(ev){            
      var gantt_item = getGanttElementFromPosition(ev.x, ev.y);
      if(this.selectedJob && this.selectedJobElement){
        this.selectedJob.end = new Date(gantt_item.getAttribute("data-date"));
        this.selectedJobElement.update();
      }
 }.bind(this);
 var _handleMouseUp = function(){
      this.selectedJob = null;
      this.selectedJobElement = null;
      document.removeEventListener("mousemove", _handleMouseMove, false);     
 }.bind(this);


 var getGanttElementFromPosition = function(x, y){
    //elementsFromPoint: returns an array of all elements at the coordinates x,y
    var items = shadowRoot.elementsFromPoint(x, y);
    
   //Possibly the mouse pointer is just above the drag handle or above the job bar. Therefore we have to iterate through the array until we arrive at the gantt_item lying behind of it
    var gantt_item = items.find(item =&gt; 
                    item.classList.contains("gantt-row-item"));
    return gantt_item;
 }  
 this.selectedJob = null;
 this.selectedJobElement = null;
</code></pre>
</div>

In the last step, we call the function `makeJobsResizable` at the end of the function `initJobs`. We also use the existing function `clear` in the file `YearMonthRenderer.js` to remove the `mousedown` and `mouseup` listeners (see sample files).

<pre><code class="language-javascript">//see file “YearMonthRenderer.js” in the example files of this article 
var initJobs = function(){
  …
  makeJobsResizable();

}.bind(this);</code></pre>

All the steps shown above are also applied to the file `DateTimeRenderer.js`.

{{% ad-panel-leaderboard %}}

## Making Jobs Editable

A job’s start and end dates should also be modifiable via an edit dialog. For this purpose, we first develop our own web component for the dialog with the name `GanttJobDialog`.

The following properties are assigned to the dialog from outside:

- `job` for the job object to be edited;
- `level` for the current zoom level of the timeline (`year-month` or `day`);
- `xPos` and `yPos` for the `x` and `y` coordinates of the position of the upper left corner of the dialog, relative to the position of the associated job bar.

In the `render` function, the appropriate form elements for adjusting the start and end dates are generated depending on the zoom level. Inputs of type `date` are used when the level is set to `year-month`, and inputs of type `datetime-local` are used when the level is `day`. Furthermore, the values of the inputs are initialized with the current data of the job.

The handler for the <kbd>save</kbd> button of the dialog has the following responsibilities:

- the new start and end dates are read from the input fields and assigned to the job object;
- a **`CustomEvent`** with the event name `save` is triggered to notify the caller of the dialog (here the `GanttJob` component) that the job data has been changed;
- the dialog is made invisible.

The handler for the dialog’s <kbd>cancel</kbd> button fires a **`CustomEvent`** with the event name `cancel` to notify the dialog’s caller that no data has been changed.

<div class="break-out">

<pre><code class="language-javascript">const template = document.createElement('template');
  template.innerHTML = 
   `&lt;style&gt;
       @import "./styles/GanttJob.css";
    &lt;/style&gt;
    &lt;dialog&gt;
        &lt;h4 id="job_title"&gt;Edit Task&lt;/h4&gt;
        &lt;form action="#"&gt;
        &lt;p&gt;
            &lt;label for="start"&gt;Start&lt;/label&gt;
            &lt;input id="start_input" name="start"&gt;
        &lt;/p&gt;
        &lt;p&gt;
            &lt;label for="start"&gt;End&lt;/label&gt;
            &lt;input id="end_input" name="start"&gt;
        &lt;/p&gt;
        &lt;p&gt;
            &lt;input type="button" id="cancel_button" value="Cancel"&gt;
            &lt;input type="button" id="save_button" value="Save"&gt;
        &lt;/p&gt;
        &lt;/form&gt;  
    &lt;/dialog&gt;`;
  export default class GanttJobDialog extends HTMLElement {
    constructor() {
      super();
      this.attachShadow({ mode: 'open' });
      this.shadowRoot.appendChild(template.content.cloneNode(true));
    }
    _job;
    _xPos;
    _yPos;
    _level = "year-month";
    connectedCallback() 
        this._render();   
    }
    disconnectedCallback() {
      this.shadowRoot.querySelector("#cancel_button").removeEventListener("click", this._handleCancel);
      this.shadowRoot.querySelector("#save_button").removeEventListener("click", this._handleSave);
      document.removeEventListener("click", this._handleClickOutside);
    }   
    _render(){
        var dialogElement = this.shadowRoot.querySelector("dialog");
        dialogElement.style.left = this._xPos+"px";
        dialogElement.style.top = this._yPos+"px";
        if(this.level == "year-month"){
           this.shadowRoot.querySelector("#start_input").type = "date";
           this.shadowRoot.querySelector("#end_input").type = "date"; 
           this.shadowRoot.querySelector("#start_input").value = `${this.job.start.getFullYear()}-${this.zeroPad(this.job.start.getMonth()+1)}-${this.zeroPad(this.job.start.getDate())}`;
           this.shadowRoot.querySelector("#end_input").value = `${this.job.end.getFullYear()}-${this.zeroPad(this.job.end.getMonth()+1)}-${this.zeroPad(this.job.end.getDate())}`;
        }else{
           this.shadowRoot.querySelector("#start_input").type = "datetime-local";
           this.shadowRoot.querySelector("#end_input").type = "datetime-local";
           this.shadowRoot.querySelector("#start_input").value = `${this.job.start.getFullYear()}-${this.zeroPad(this.job.start.getMonth()+1)}-${this.zeroPad(this.job.start.getDate())}T${this.zeroPad(this.job.start.getHours())}:00`;
           this.shadowRoot.querySelector("#end_input").value = `${this.job.end.getFullYear()}-${this.zeroPad(this.job.end.getMonth()+1)}-${this.zeroPad(this.job.end.getDate())}T${this.zeroPad(this.job.end.getHours())}:00`;
        }
        this.shadowRoot.querySelector("#cancel_button").addEventListener("click", this._handleCancel);
        this.shadowRoot.querySelector("#save_button").addEventListener("click", this._handleSave);
        document.addEventListener("click", this._handleClickOutside);
    }
    _handleCancel = function(e){
        var dialogElement = this.shadowRoot.querySelector("dialog");
        this.dispatchEvent(new CustomEvent("cancel"));
        dialogElement.style.visibility = "hidden";
    }.bind(this);


    _handleSave = function(e){
        var dialogElement = this.shadowRoot.querySelector("dialog");
        this.job.start = new Date(this.shadowRoot.querySelector("#start_input").value);
        this.job.end = new Date(this.shadowRoot.querySelector("#end_input").value);
        this.dispatchEvent(new CustomEvent("save"));
        dialogElement.style.visibility = "hidden";
    }.bind(this);


    //when clicking outside the dialog, the dialog should be canceled as well
    _handleClickOutside = function(e){
        var dialogElement = this.shadowRoot.querySelector("dialog");
        //we need to check whether the click was triggered inside or outside the dialog
        var items = this.shadowRoot.elementsFromPoint(e.offsetX, e.offsetY);
        var close = true;
        items.forEach(item =&gt; {
            if(item.tagName == “DIALOG”){
                close = false;
                return;
            }
        });
        if(close){
            this.dispatchEvent(new CustomEvent("cancel"));
            dialogElement.style.visibility = "hidden";
        }
    }.bind(this);


    set job(newValue){
        this._job = newValue;
        this._render();
    }
    get job(){
        return this._job;
    }
    set xPos(newValue){
        this._xPos = newValue;
        this._render();
    }
    set yPos(newValue){
        this._yPos = newValue;
        this._render();
    }
    set level(newValue){
       this._level = newValue;
    }
    get level(){
       return this._level;
    }
    zeroPad(n){return n&lt;10 ? "0"+n : n;}
}
window.customElements.define('gantt-job-dialog', GanttJobDialog);
</code></pre>
</div>

The edit dialog is to be opened by double-clicking on a job bar. Therefore, we need a listener for the `dblclick` event, which we again attach to the surrounding `gantt-container` according to the principle of event delegation (the listener is removed in the function `clear`; see example files). 

For this purpose, we add the function `makeJobsEditable` in the file `YearMonthRenderer.js`:

<pre><code class="language-javascript">var makeJobsEditable = function(){
  if(checkElements()){
    var container = shadowRoot.querySelector("#gantt-container");
    container.addEventListener("dblclick", _handleDblClick, false);
  }
}.bind(this);

var _handleDblClick = function(e){
  if(e.target.tagName == "GANTT-JOB"){
    var jobElement = e.target;
    jobElement._handleDblClick();
  }
}</code></pre>

The actual processing of the event takes place in the `GanttJob` component. Here, an instance of the `GanttJobDialog` component is initialized and inserted into the DOM as a child element of the job bar.

At this point, we also implement the handlers for the `CustomEvents` `save` and `cancel` triggered by the dialog. Both handlers remove the dialog from the DOM. The `save` handler additionally triggers an update of the length of the job bar and, in turn, forwards a `CustomEvent` `editjob` to the associated renderer (`YearMonthRenderer` or `DateTimeRenderer`).

<div class="break-out">

<pre><code class="language-javascript">&#95;handleDblClick = function(e){
    var panel = this.shadowRoot.querySelector(".job");
    //As long as the dialog is open, the z-index of the job bar is temporarily increased. This ensures that the dialog is not overlapped by other job bars.
    panel.style.zIndex = 101;
    var dialogElement = document.createElement("gantt-job-dialog");
    dialogElement.job = this.job;
    dialogElement.xPos = 0;
    dialogElement.yPos = 40;
    dialogElement.level = this.level;
    panel.appendChild(dialogElement);
    dialogElement.addEventListener("cancel", () =&gt; {
      panel.style.zIndex = 100;
      dialogElement.remove();
    });
    dialogElement.addEventListener("save", () =&gt; {
      this.update();
      panel.style.zIndex = 100;
      dialogElement.remove();
      this.dispatchEvent(new CustomEvent("editjob"));
    });
}.bind(this);</code></pre>
</div>

Back in the file `YearMonthRenderer.js`, we have to extend the function `initJobs` once again. First, a handler for the event `editjob` is defined to ensure that the job is re-inserted at the correct position in the Gantt Chart in case of a changed start time. Secondly, a call to `makeJobsEditable` is placed at the end of the function.

<div class="break-out">

<pre><code class="language-javascript">var initJobs = function{

   ... 
   jobElement.ondragstart = function(ev){
        ev.dataTransfer.setData("job", ev.target.id);           
   };
   jobElement.addEventListener("editjob", (ev) =>{
        var date_string = formatDate(job.start);
        var gantt_item = shadowRoot.querySelector(&#96;div[data-resource="${job.resource}"][data-date="${date_string}"]&#96;);
        gantt_item.appendChild(jobElement);          
    });
    ... 
    makeJobsResizable();
    makeJobsEditable();
}</code></pre>
</div>

All the steps shown are also applied to the file `DateTimeRenderer.js`.

{{% ad-panel-leaderboard %}}
  
## Special Libraries For Gantt Charts And Scheduling

With the code enhancements presented in this second part of the article, the Gantt Chart has become a little more interactive and user-friendly. Nevertheless, there are still a few things left open. For example, when dropping a job, the left side of the job bar (which means the start time) jumps to the `gantt` cell that was just below the mouse pointer. Instead, the job should be **positioned exactly in the cell to which the left side of the bar points** regardless of the position of the mouse pointer on the job bar.

Above that, we need a few more refinements that make the interaction with the Gantt Chart even smoother, such as a **flexible adjustment of the chart to the screen size** or a **flexible positioning of the editing dialogs** depending on the available space.

The present chart component can be configured both as a Gantt Chart and a resource scheduler. If used as a Gantt Chart, some rules still have to be implemented. For example, in this case, **a job may not be moved from one row to the next**. In addition, more Gantt Chart specific configuration options are needed, such as **sequence dependencies** between jobs or a **hierarchical organization of tasks into subtasks**.

Users will likely expect even more features in a professional Gantt Chart for production use:

- **reordering of rows in the WBS tree of tasks and subtasks;**
- **filtering, sorting, inline cell editing;**
- **tracking data changes;**
- **Zooming into different views with different time granularity** (days vs months vs years);
- **dependencies between tasks;**
- **non-working time;**
- **tooltips**
- .. and more.

So, if you want further to develop your own Gantt Chart or scheduling component, those are some feature ideas to consider.

However, if you are looking for a Gantt chart solution that you can easily integrate into your web app, it might be worth taking a look at existing third-party JavaScript Gantt libraries. Such libraries contain pre-built, sophisticated components that will save you the massive effort of developing and maintaining your own Gantt widget.

Let’s take a look at three examples of professional Gantt chart libraries.

### JavaScript Gantt Chart By Syncfusion

The handling of Gantt Chart libraries is usually very comfortable. Often a single JavaScript file is sufficient to configure the chart according to your preferences and fill it with data. 

For example, let’s look at the [`index.js`](https://drive.google.com/file/d/1R87U4dR-7NVdxdssLKrdD566p9fGLxCv/view?usp=sharing) file of our project in this article where we initialize our Gantt Chart with the required data of our jobs and resources. Our component `VanillaGanttChart` is simply imported at the beginning of the file. This is how it works with ready-made libraries: after importing the required scripts and modules, you can immediately start entering your data into the Gantt Chart or configuring the Gantt Chart according to your wishes.

Let’s check out the [JavaScript Gantt Chart by Syncfusion](https://www.syncfusion.com/javascript-ui-controls/js-gantt-chart). This is a commercial tool “to display and manage hierarchical tasks with timeline details.”

In the “getting started” section of the [tool’s documentation](https://ej2.syncfusion.com/javascript/documentation/gantt/es5-getting-started/#dialog-editing), you will learn how to initialize a simple Gantt Chart with a few basic options (e.g., options for task editing, filtering, sorting, and defining task relationships). A first simple Gantt Chart could look like this with Syncfusion:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c84083c-2c30-45c6-ad3e-41ad88e136d7/2-vanilla-javascript-gantt-chart-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c84083c-2c30-45c6-ad3e-41ad88e136d7/2-vanilla-javascript-gantt-chart-part-2.png" width="800" height="339" sizes="100vw" caption="Simple Gantt Chart built with the JavaScript Gantt control by Syncfusion. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c84083c-2c30-45c6-ad3e-41ad88e136d7/2-vanilla-javascript-gantt-chart-part-2.png'>Large preview</a>)" alt="Simple Gantt Chart built with the JavaScript Gantt control by Syncfusion" >}}

Building on this, the functionality of the chart can be extended further.

### JavaScript Gantt Chart By Bryntum

Another example that is worth considering is the [Bryntum Gantt](https://www.bryntum.com/products/gantt?aw=smash-jun2022) library, “a super-fast and fully customizable Gantt chart suite.” 

After downloading [a free trial of the library](https://www.bryntum.com/download?aw=smash-jun2022), you will get a build folder with CSS and JavaScript files for creating interactive Gantt charts. You can integrate these files into your web app and then immediately configure your individual chart. A simple [getting started guide](https://www.bryntum.com/docs/gantt/guide/Gantt/getting_started?aw=smash-jun2022) provides a quick introduction to the component. For example, a basic chart could look like this with the Bryntum Gantt library:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d73c5155-481b-4767-9126-cc0317fd61c1/6-vanilla-javascript-gantt-chart-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d73c5155-481b-4767-9126-cc0317fd61c1/6-vanilla-javascript-gantt-chart-part-2.png" width="800" height="407" sizes="100vw" caption="Simple Gantt Chart built with Bryntum Gantt. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d73c5155-481b-4767-9126-cc0317fd61c1/6-vanilla-javascript-gantt-chart-part-2.png'>Large preview</a>)" alt="Simple Gantt Chart built with Bryntum Gantt" >}}

You will learn a lot about the numerous customization options in the [full Bryntum Gantt documentation](https://www.bryntum.com/docs/gantt?aw=smash-jun2022). You will also explore how the tool can be integrated with popular frameworks like Angular, React, Vue, and many more or how to organize the loading and saving of data (CRUD data management). 

The [examples section](https://bryntum.com/examples/gantt?aw=smash-jun2022) provides a visual overview of the various features of Bryntum Gantt.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0a6ccbf-3695-47ac-a606-8b76d0e2fe7a/7-vanilla-javascript-gantt-chart-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0a6ccbf-3695-47ac-a606-8b76d0e2fe7a/7-vanilla-javascript-gantt-chart-part-2.png" width="800" height="228" sizes="100vw" caption="An extract from the <a href='https://www.bryntum.com/products/scheduler-pro?aw=smash-jun2022'>showcase of interactive examples</a> of Bryntum Gantt Charts (you can browse through more than 50 examples). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0a6ccbf-3695-47ac-a606-8b76d0e2fe7a/7-vanilla-javascript-gantt-chart-part-2.png'>Large preview</a>)" alt="An extract from the showcase of interactive examples of Bryntum Gantt Charts" >}}

They also offer [Bryntum Scheduler](https://www.bryntum.com/products/scheduler-pro?aw=smash-jun2022) &mdash; a library for resource planning.

### JavaScript Gantt Chart By Webix

With [Webix Gantt](https://webix.com/gantt/), another commercial Gantt library with rich functionality is available. The uncomplicated steps for installing, creating, and configuring a Gantt chart are [documented in detail](https://docs.webix.com/gantt__installing.html).

You can try out the tool in a [full-screen interactive demo](https://webix.com/demos/gantt/):

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17c80535-2cdc-45bb-92b2-83c0e0f09537/8-vanilla-javascript-gantt-chart-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17c80535-2cdc-45bb-92b2-83c0e0f09537/8-vanilla-javascript-gantt-chart-part-2.png" width="800" height="427" sizes="100vw" caption="Simple Gantt Chart built with Webix Gantt. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17c80535-2cdc-45bb-92b2-83c0e0f09537/8-vanilla-javascript-gantt-chart-part-2.png'>Large preview</a>)" alt="Simple Gantt Chart built with Webix Gantt" >}}

## Conclusion

Gantt Charts are a valuable visualization for project management, planning, and task organization. There are many ways to integrate Gantt Charts into a web application. In the last two articles, we built an interactive Gantt Chart from scratch, and in doing so, we learned a lot about CSS grids, Web Components, and JavaScript events. If you have more complex requirements, it is worth looking at the commercial JS libraries, which are often very powerful.
  
{{< signature "yk, il" >}}
