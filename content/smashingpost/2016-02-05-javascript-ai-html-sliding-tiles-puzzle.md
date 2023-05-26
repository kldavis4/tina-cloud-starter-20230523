---
title: JavaScript AI For An HTML Sliding Tiles Puzzle
slug: javascript-ai-html-sliding-tiles-puzzle
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2727b1d6-6b10-4bd4-8769-8c5bfa4b649b/sliding-tiles-puzzle-7-opt.jpg
date: 2016-02-05T02:17:51.000Z
author: arnaldoperezcastano
summary: >-
  Enter the amazing world of rational agents, supervised learning and unsupervised learning. Start developing algorithms that can solve daily life problems by simulating the thinking of the human mind. The purpose of AI should be that: providing a contribution to society and making our life easier and more sophisticated.
description: >-
  Enter the amazing world of rational agents, supervised learning and unsupervised learning. Start developing algorithms that can solve daily life problems by simulating the thinking of the human mind.
categories:
  - JavaScript
  - Games
  - HTML5
  - AI
---
Sam Loyd (1841–1911), American chess player and puzzle maker, created the <strong>sliding tiles puzzle</strong> in the 1870s. The puzzle is represented by an <em>m</em>×<em>n</em> grid, where <em>m</em> is number of columns and <em>n</em> is number of rows, and each cell can be any imaginable value (number, letter, image, and so on.)

The purpose of the puzzle is to <strong>rearrange the initial configuration of the tiles to match another configuration</strong> known as the <em>goal configuration</em>. The rearrangement task is achieved by swapping the empty tile with some other tile in all possible directions (up, down, left, and right).

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9ef7f5c-8f45-49cb-833b-8ce0561bb7b4/sliding-tiles-puzzle-1-opt.jpg" alt="Sliding Tiles Puzzle" /><br>
<figcaption>Sliding Tiles Puzzle.</figcaption></figure>

It is assumed that the empty tile cannot be moved out of the board: thus, if located in the first column, the empty tile cannot go left; and if located in the rightmost column, it cannot go right; the same applies for rows considering moves either up or down. The solution to the previous puzzle will be obtained in the following steps.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbe49296-2da8-4f1e-9b58-fb6c4a4895e2/sliding-tiles-puzzle-2-opt.jpg" alt="How it starts" /><br>
<figcaption>How it starts.</figcaption></figure>

...and finally:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a97e3ea3-cecd-42f5-b5f7-7a2b60fa8e13/sliding-tiles-puzzle-3-opt.jpg" alt="How it should end" /><br>
<figcaption>How it should end.</figcaption></figure>

Verify how the initial and goal configurations are now the same; this means we have completed the puzzle.

This article will be divided into two parts. First, we'll provide a brief description of <strong>how to create and develop a sliding tiles puzzle</strong> using HTML, CSS for the visual aspects, and JavaScript for moving (by means of animation) the tiles on the board. (We'll need this to illustrate the latter part of this article.)

Second, we'll <strong>develop an artificial intelligence by means of an A* search algorithm</strong> capable of finding a solution with the minimum number of moves to the goal configuration, thus providing an optimal solution. The various heuristics associated with the A* algorithm will help guide the search, and the cleverer the heuristic, the sooner the optimal solution will be found. Each of the heuristics described will be presented in order of cleverness; therefore, the last heuristic presented will be the most powerful.

{{% feature-panel %}}

## Layout

We'll start by creating the corresponding <em>sliding_tiles_puzzle.html</em> file which will hold the game; we'll also create the following empty files:

*   _styles.css_
*   _stpuzzle.js_

Moreover, it will be necessary to add <em>jquery.js</em> as we will use it to make our life easier and get much more elegant, legible code.

The header should end up looking like this:

<div class="break-out">

 <pre><code class="language-markup">&lt;head&gt;
   &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
   &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /&gt;
   &lt;link href="css/styles.css" rel="stylesheet" media="screen" type="text/css"&gt;

   &lt;title&gt;Sliding Tiles Puzzle&lt;/title&gt;
&lt;/head&gt;
</code></pre>
</div>

For efficiency, we'll add links to every script at the bottom of the page. This is a common practice, since pages are rendered in a top to bottom manner and we regularly want the page to load as quickly as possible; we leave the functional scripts to be loaded at the end, after all visual elements have been properly loaded.

<pre><code class="language-markup">      &lt;script type="text/javascript" src="js/jquery.js"&gt;&lt;/script&gt;
      &lt;script type="text/javascript" src="js/priority-queue.js"&gt;&lt;/script&gt;
      &lt;script type="text/javascript" src="js/hashtable.js"&gt;&lt;/script&gt;
      &lt;script type="text/javascript" src="js/hashset.js"&gt;&lt;/script&gt;
      &lt;script type="text/javascript" src="js/stpuzzle.js"&gt;&lt;/script&gt;
   &lt;/body&gt;
&lt;/html&gt;
</code></pre>

The <em>priority-queue.js</em>, <em>hashtable.js</em> and <em>hashset.js</em> will be used in the artificial intelligence component to provide efficiency to our rational agent; they respectively represent priority queues, hash tables and hash sets data structures.

Now we'll start creating the layout of the page. At first, our layout will look like this.

<pre><code class="language-markup">&lt;body&gt;	
   &lt;div class="container"&gt;

   &lt;/div&gt;
   &lt;div id="panel"&gt;
   &lt;/div&gt;
</code></pre>

The <code>container</code> class, located in the <em>styles.css</em> file, appears as in the following block of styles.

<pre><code class="language-css">/* 
Developed by Arnaldo Perez Castano
arnaldo.skywalker@gmail.com
*/

.container {
   width:1024px;
   margin-left: auto;
   margin-right: auto;
   min-height:380px;
}
</code></pre>

The panel is simply a log that we'l use for printing or showing the results associated with the artificial intelligence component. In this panel we'll be printing the optimal solution obtained by the AI.

<pre><code class="language-css">#panel {
   width:100%;
   background-color: rgb(180,180,180);
   min-height:1000px;
   color:white;
   font-weight: bold;
   padding:5px;
   font-family: Arial;
}
</code></pre>

Since we want the global container to be at the center of the page, we set a fixed width, and properties <code>margin-left</code> and <code>margin-right</code> to auto – this will set it right in the middle. Now we add the <code>grid-container</code> div which, as the name suggests, is basically the div that will immediately contain the grid representing the board.

<pre><code class="language-markup">&lt;div class="container"&gt;
   &lt;div class="grid-container"&gt;
      &lt;h2&gt; Initial Config &lt;/h2&gt;

   &lt;/div&gt;
&lt;/div&gt;
</code></pre>

The <code>grid-container</code> class and the selectors involving it are illustrated in the following blocks.

<pre><code class="language-css">.grid-container {
   float: left;
   width:210px;
   height:250px;
   text-align: center;
   width:50%;
}

.grid-container h2 {
   font-family: Tahoma;
}
</code></pre>

We are floating left the grid container since we will put two of these in the same line: one for each configuration (initial and goal). Finally, we add the grid div.

<pre><code class="language-markup">&lt;div class="grid-container"&gt;
   &lt;h2&gt; Initial Config &lt;/h2&gt;
   &lt;div class="grid start"&gt;
      &lt;div class="row"&gt; 
         &lt;div class="cell" data-pos="0,0"&gt;&lt;span&gt;6&lt;/span&gt;&lt;/div&gt;
         &lt;div class="cell" data-pos="0,1"&gt;&lt;span&gt;4&lt;/span&gt;&lt;/div&gt;
         &lt;div class="cell" data-pos="0,2"&gt;&lt;span&gt;7&lt;/span&gt;&lt;/div&gt;
      &lt;/div&gt;
      &lt;div class="row"&gt; 
         &lt;div class="cell" data-pos="1,0"&gt;&lt;span&gt;8&lt;/span&gt;&lt;/div&gt;
         &lt;div class="cell" data-pos="1,1"&gt;&lt;span&gt;5&lt;/span&gt;&lt;/div&gt;
         &lt;div class="cell" id="empty" data-pos="1,2"&gt;&lt;/div&gt;
      &lt;/div&gt;
      &lt;div class="row"&gt; 
         &lt;div class="cell" data-pos="2,0"&gt;&lt;span&gt;3&lt;/span&gt;&lt;/div&gt;
         &lt;div class="cell" data-pos="2,1"&gt;&lt;span&gt;2&lt;/span&gt;&lt;/div&gt;
         &lt;div class="cell" data-pos="2,2"&gt;&lt;span&gt;1&lt;/span&gt;&lt;/div&gt;
      &lt;/div&gt;
   &lt;/div&gt;
&lt;/div&gt;
</code></pre>

The sliding tiles puzzle grid consists of three rows, each with three cells; this basically makes up the entire grid. With the proposed layout we achieve a very intuitive manner of representing the grid. The grid contains three children; each child is a row (div element); a row contains three children; and each child represents a cell (also a div element).

For programming-related issues we add the <code>data-pos</code> attribute to each cell, to indicate the position of each cell on the board. The same goes for the <code>start</code> class. We need to differentiate the initial configuration from the goal configuration as the latter will not receive input from the user. The <code>start</code> class will help us accomplish that. The definition of the above classes is listed in the next lines.

<pre><code class="language-css">.grid {
   background-color: rgb(248,248,248);
   border: solid 5px rgb(249, 90, 0);
   width:210px;
   height:210px;
   margin-left: auto;
   margin-right: auto;
   border-radius: 3px;
   box-shadow: 5px 5px #d8d8d8, 5px 5px #d8d8d8;
   overflow: auto;
}

.row {
   height:33.3%;
}

.cell {
   width:32.3%;
   height:100%;
   float: left;
   text-align: center;
   font-size:150%;
   font-family: Arial;
   font-weight: bold;
   position:relative;
}

.cell:hover {
   background-color: rgb(221,221,221);
}

.cell span {
   display: block;
   transform: translateY(70%);
}
</code></pre>

The final result is a complete 3×3 grid with numbers 1 to 9.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6d3c527-b508-41b0-8bb9-d4e5d3ce5c36/sliding-tiles-puzzle-4-opt.jpg" alt="Final grid" /><br>
<figcaption>Final grid.</figcaption></figure>

To get the goal configuration into the page we just copy the grid div and all its contents and rename the <code>start</code> class to <code>goal</code>.

<pre><code class="language-markup">&lt;div class="grid-container"&gt;
   &lt;h2&gt; Goal Config &lt;/h2&gt;
   &lt;div class="grid goal"&gt;
      &lt;div class="row"&gt; 
         &lt;div class="cell"&gt;&lt;span&gt;1&lt;/span&gt;&lt;/div&gt;
         &lt;div class="cell"&gt;&lt;span&gt;2&lt;/span&gt;&lt;/div&gt;
         &lt;div class="cell"&gt;&lt;span&gt;3&lt;/span&gt;&lt;/div&gt;
      &lt;/div&gt;
      &lt;div class="row"&gt; 
         &lt;div class="cell"&gt;&lt;span&gt;4&lt;/span&gt;&lt;/div&gt;
         &lt;div class="cell"&gt;&lt;span&gt;5&lt;/span&gt;&lt;/div&gt;
         &lt;div class="cell"&gt;&lt;span&gt;6&lt;/span&gt;&lt;/div&gt;
      &lt;/div&gt;
      &lt;div class="row"&gt; 
         &lt;div class="cell"&gt;&lt;span&gt;7&lt;/span&gt;&lt;/div&gt;
         &lt;div class="cell"&gt;&lt;span&gt;8&lt;/span&gt;&lt;/div&gt;
         &lt;div class="cell"&gt;&lt;/div&gt;
      &lt;/div&gt;
   &lt;/div&gt;
&lt;/div&gt;
</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dad0b82a-7b05-489d-a144-4f4638ce2de4/sliding-tiles-puzzle-5-opt.jpg" alt="Start and Final grids" /><br>
<figcaption>Start and Final grids.</figcaption></figure>

To conclude, we add <b>Solve</b> and <b>Show Step</b> buttons to the first grid container.

<pre><code class="language-markup">&lt;button onclick="start()"&gt; Solve &lt;/button&gt;
&lt;button onclick="showSolution()"&gt; Show Step &lt;/button&gt;
</code></pre>

The first button will trigger the rational agent; in other words, the A* search algorithm. The second will visually show a step of the solution obtained by the first. Thus, by pressing the <b>Show Step</b> button <em>n</em> times where <em>n</em> is the length of the solution, we'll know how to solve the puzzle in the minimum number of steps.

Now that we have some visual competence let us start building some functional competence. We need to make the game work – basically, that translates into allowing the empty tile to move throughout the board. To complete this piece of development we'll be using JavaScript. The first lines of the <em>stpuzzle.js</em> file will look like this

<pre><code class="language-javascript">/* 
   Developed by Arnaldo Perez Castano
   arnaldo.skywalker@gmail.com
*/

var emptytilePosRow = 1;
var emptytilePosCol = 2;
var cellDisplacement = "69px";
</code></pre>

The <code>emptytilePosRow</code> and <code>emptytilePosCol</code> will tell us where the empty tile is at all times. It will be updated with each move made.

The <code>cellDisplacement</code> variable will indicate the displacement value to apply to a cell when an animation is being made. Note how the <code>cell</code> class has the <code>position</code> attribute set to relative. We want to freely move the cells on the board using the <code>top</code> and <code>right</code> properties on animations. The <code>cellDisplacement</code> value will indicate the new values of the <code>top</code> and <code>right</code> properties, thus moving the cells.

The function taking care of moves on the board starts like this:

<pre><code class="language-javascript">function moveTile() 
{
   // Gets the position of the current element
   var pos = $(this).attr('data-pos');
   var posRow = parseInt(pos.split(',')[0]);
   var posCol = parseInt(pos.split(',')[1]);
</code></pre>

Notice how we are already using jQuery to select all cells from the starting grid. Note also the use of the <code>start</code> class. We want to maintain the goal board as read-only, therefore we select all cells belonging to the start grid – and only to the start grid. Up next, we get the position of the cell being selected. Remember, the positions are stored as '<em>x</em>, <em>y</em>': we get the row and column indexes in the <code>posRow</code> and <code>posCol</code> variables.

The rest of the function is dedicated to executing the correct move.

<div class="break-out">

 <pre><code class="language-javascript">// Move Up
   if (posRow + 1 == emptytilePosRow &amp;&amp; posCol == emptytilePosCol) 
   {
      $(this).animate({
      'top' : "+=" + cellDisplacement //moves up
      });

      $('#empty').animate({
      'top' : "-=" + cellDisplacement //moves down
      });

      emptytilePosRow-=1;
      $(this).attr('data-pos',(posRow+1) + "," + posCol);
   }

   // Move Down
   if (posRow - 1 == emptytilePosRow &amp;&amp; posCol == emptytilePosCol) 
   {
      $(this).animate({
      'top' : "-=" + cellDisplacement //moves down
      });

      $('#empty').animate({
      'top' : "+=" + cellDisplacement //moves up
      });

      emptytilePosRow+=1;
      $(this).attr('data-pos',(posRow-1) + "," + posCol);
   }

   // Move Left
   if (posRow == emptytilePosRow &amp;&amp; posCol + 1 == emptytilePosCol) 
   {
      $(this).animate({
      'right' : "-=" + cellDisplacement //moves right
      });

      $('#empty').animate({
      'right' : "+=" + cellDisplacement //moves left
      });

      emptytilePosCol -= 1;
      $(this).attr('data-pos',posRow + "," + (posCol+1));
   }

   // Move Right
   if (posRow == emptytilePosRow &amp;&amp; posCol - 1 == emptytilePosCol) 
   {
      $(this).animate({
      'right' : "+=" + cellDisplacement //moves left
      });

      $('#empty').animate({
      'right' : "-=" + cellDisplacement //moves right
      });

      emptytilePosCol += 1;
      $(this).attr('data-pos',posRow + "," + (posCol-1));
   }

   // Update empty position
   $('#empty').attr('data-pos',emptytilePosRow + "," + emptytilePosCol);
}
</code></pre>
</div>

Each of the four <code>if</code> statements represents a different move for the empty tile. They share similarities as their main differences reside on the conditions, signs and updating of variables. The right move, for instance, begins by checking if the empty tile is to the left of the current cell by the condition: <code>posRow == emptytilePosRow</code> (the same as saying that they are in the same row) and <code>posCol - 1 == emptytilePosCol</code> (the same as saying that the empty tile is to the left of current cell).

If the condition is satisfied then, using JQuery's animation, we change the value of the <code>right</code> property to displace the current cell to the left and make the illusion of having swapped the elements. The <code>if</code> statement ends by updating the <code>emptytilePosCol</code> variable (adding 1) as it was moved to the right, and updating the cell position which was moved to the left (subtracting 1 from its column position). At the end, we update the position of the empty tile.

## Artificial Intelligence

The <a href="https://en.wikipedia.org/wiki/A*_search_algorithm">A* informed search</a> (Hart et al, 1968) represents the rational non-living agent that we'll be developing to solve the sliding tiles puzzle. A rational agent is an entity that, being part of some environment and subject to certain rules, is capable of perceiving in this environment and acting rationally to these perceptions. Rationality would be given by the appropriate decision making of the agent, considered appropriate if it's aimed towards maximizing some desired outcome. The artificial intelligence is the agent itself.

Humans are rational (most of the time) living agents as they belong to an environment (the universe) and we are subject to certain environmental rules (we cannot live under extremely cold temperatures, for example); we obtain perceptions from the environment (we feel cold) and we react rationally (again, most of the time) to these perceptions (we wear coats).

In the context of the sliding tiles puzzle, the environment is represented by the board, the rules or constraints by the possible directions in which one can move the empty tile (up, down, left, right), and by the fact that you execute a valid movement when you swap the empty tile with any of its adjacent tiles. A perception corresponds to the current state of the configuration and the rational reaction to this perception corresponds to the executed move. If it's rational, this move should be oriented toward getting a configuration that matches the goal configuration.

### What Will The A* Search Do?

The A* search, as the name suggests, is a search algorithm, its purpose to intelligently search the space state (set of all board configurations) and find a path from the initial configuration to the goal configuration. The intelligence of the search is given by how many states it visits: the fewer the number of states visited, the more intelligent it is and the sooner it will provide a solution. To navigate through the space state, we model the problem as a graph. In this manner, we consider that state B is a child of state A if B is obtained by moving the empty tile in some valid direction in A. In this sense, a node on the graph can have at most four children, one for each possible direction.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/028a3a09-2ece-4db0-a6cc-3788eb82c7e1/sliding-tiles-puzzle-7-opt-preview.jpg" alt="Expanded nodes in the A* Search" /><br>
<figcaption>Expanded nodes in the A* Search. (<a>View large version</a>)</figcaption></figure>

The A* search is informed as it uses environment knowledge to select the next step to continue the search. This knowledge is represented by a numeric value associated with every state (<em>s</em>) and known as <em>f(s)</em>, hence in general:

<em>f(s)</em> = <em>g(s)</em> + <em>h(s)</em>

where <em>g(s)</em> is the cost of reaching state <em>s</em> from the initial state, and <em>h(s)</em> is the estimated cost of reaching the goal state from the current state or configuration. This relation is depicted in the following figure.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/957bd18d-af05-499c-b24b-1bcc5c69bb5a/sliding-tiles-puzzle-8-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e914acff-7634-40b4-9d2d-97783a947715/sliding-tiles-puzzle-8-opt-preview.jpg" alt="Cost of moving from initial config to the final config" /></a><figcaption>Cost of moving from initial config to the final config. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/957bd18d-af05-499c-b24b-1bcc5c69bb5a/sliding-tiles-puzzle-8-opt.jpg">View large version</a>)</figcaption></figure>

To guide the search through the immense space state we use heuristics. A heuristic is the way by which we adhere our empirical and specific environment knowledge to the rational agent, in this case the A* search. The information provided by the heuristic is supposed to help find a feasible, short path to the goal configuration.

Since we are modeling the problem as a graph, the basic skeleton of the A* search corresponds to that of a breadth-first search (BFS), a classical graph search algorithm. The difference between the A* search and the BFS is that nodes or states in the A* search are associated with some value <em>f(s)</em>, and the node selected for the next iteration is the one with the minimum <em>f(s)</em>. In BFS, all nodes have the same value (1) so it is not really important which one comes first, just that they are selected in the order in which they were added to the queue (FIFO: first in, first out).

When developing a heuristic it's important to make sure it holds the admissibility criteria. A heuristic is considered admissible if it doesn't overestimate the minimum cost of reaching the goal configuration from the current configuration. If admissible, the A* search algorithm will always find an optimal solution.

As previously mentioned we are coding the artificial intelligence in JavaScript. Some may think this an unwise approach but we'll prove that JavaScript can offer all we need to obtain an efficient rational agent. We'll start by creating the <code>Node</code> object shown in the following code.

<pre><code class="language-javascript">function Node(value, state, emptyRow, emptyCol, depth) {
   this.value = value
   this.state = state
   this.emptyCol = emptyCol
   this.emptyRow = emptyRow
   this.depth = depth
   this.strRepresentation = ""
   this.path = ""

   // String representation of the state in CSV format
   for (var i = 0; i &lt; state.length; i++)
   {
      // We assume the state is a square
      if (state[i].length != state.length) {
         alert('Number of rows differs from number of columns')
         return false
      }

      for (var j = 0; j &lt; state[i].length; j++)
      	this.strRepresentation += state[i][j] + ",";
   }
   this.size = this.state.length
}
</code></pre>

A description of every variable is listed next.

*   `value`: represents the _f(s)_ value.
*   `state`: represents the state of the board as a two-dimensional array.
*   `emptyCol`: indicates the column in which the empty tile is located.
*   `emptyRow`: indicates the row in which the empty tile is located.
*   `depth`: indicates the number of moves executed from the initial configuration up to the configuration of this node, the _g(s)_ value.
*   `strRepresentation`: string representation of the board in CSV format. For the goal configuration the string representation would be "1,2,3,4,5,6,7,8,0,". The sliding tiles puzzle is a cyclic puzzle: from one configuration _s_ and after a sequence of moves we could get back to _s_, hence we'll store the representation of every expanded node to avoid these cycles. For this purpose we are using the HashSet.
*   `path`: stores every move in a string ("DLRU"), thus this string represents the sequence of moves made from the initial configuration up to the current node.
*   `size`: the size of the board. Notice that we are assuming the board has dimensions _n_, _m_ where _n_=_m_.

Now that we've presented the Node object let's illustrate the execution of the A* algorithm through an example. For this example we'll consider the <em>misplaced tiles heuristic</em>, probably the simplest, most common heuristic for this puzzle. The misplaced tiles heuristic returns the number of tiles that are misplaced; that is, in an incorrect position when compared to the goal configuration. It's admissible as the number returned does not overestimate the minimum number of moves required to get to the goal state. You have to move every misplaced tile once at least to be able to take them to their goal position; hence, it is admissible.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/501c1af8-890f-448f-bf06-9100dc258f03/sliding-tiles-puzzle-9-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccb4f74f-1a3a-4f4a-8fa4-55c9931a8bc9/sliding-tiles-puzzle-9-opt-preview.jpg" alt="A* Search" /></a><figcaption>A* Search. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/501c1af8-890f-448f-bf06-9100dc258f03/sliding-tiles-puzzle-9-opt.jpg">View large version</a>)</figcaption></figure>

To implement the A* algorithm we'll create an <code>AStar</code> object with the following schema:

<pre><code class="language-javascript">function AStar(initial, goal, empty) {
   this.initial = initial
   this.goal = goal
   this.empty = empty
   this.queue = new PriorityQueue({ comparator: function(a, b) { 
		if (a.value &gt; b.value)
			return 1
		if (a.value &lt; b.value)
			return -1
		return 0
	}});
	this.queue.queue(initial);
	this.visited = new HashSet();
}
</code></pre>

Notice how we are already using the data structures contained in the script files we added at the beginning. For the priority queue, we defined a comparison function that we'll need to sort the elements or nodes in ascending order. The visited HashSet will store the <code>strRepresentation</code> of our visited configurations. This way we avoid cycles.

To enhance the <code>AStar</code> object, we'll use prototypes to add methods and properties. A <code>prototype</code> is a method or property that becomes part of every new object created after the method or property has been related to the object at hand. For instance, the <code>execute</code> function will be available for every <code>AStar</code> object declared after this piece of code.

<pre><code class="language-javascript">AStar.prototype.execute = function () 
{
   // Add current state to visited list
   this.visited.add(this.initial.strRepresentation)

   while (this.queue.length &gt; 0) 
   {
      var current = this.queue.dequeue()

      if (current.strRepresentation == this.goal.strRepresentation) 
      	return current

      this.expandNode(current)
   }
}
</code></pre>

The <code>execute</code> skeleton resembles that of the BFS skeleton:

*   There's a loop that will end when the priority queue is empty.
*   The current variable will hold the node contained in the queue with minimum value.
*   If this node's state matches the goal state then we would have completed the task.
*   Otherwise we expand the current node. The expansion translates into moving the empty tile in all possible directions, hence generating new nodes that will be queued into the queue.

The statements block from the expansion method is presented in the following code:

<pre><code class="language-javascript">AStar.prototype.expandNode = function (node) 
{
   var temp = ’
   var newState = ’
   var col = node.emptyCol
   var row = node.emptyRow
   var newNode = ’

   // Up
   if (row &gt; 0)
   {
      newState = node.state.clone();
      temp = newState[row - 1][col]
      newState[row - 1][col] = this.empty
      newState[row][col] = temp
      newNode = new Node(0, newState, row - 1, col,  node.depth + 1)

      if (!this.visited.contains(newNode.strRepresentation))
      {
      newNode.value = newNode.depth + this.heuristic(newNode)
      newNode.path = node.path + "U"
      this.queue.queue(newNode)
      this.visited.add(newNode.strRepresentation)
      }
   }

   // Down
  if (row &lt; node.size - 1)
  {
      newState = node.state.clone();
      temp = newState[row + 1][col]
      newState[row + 1][col] = this.empty
      newState[row][col] = temp
      newNode = new Node(0, newState, row + 1, col, node.depth + 1)

      if (!this.visited.contains(newNode.strRepresentation))
      {
         newNode.value = newNode.depth + this.heuristic(newNode)
	 newNode.path = node.path + "D"
         this.queue.queue(newNode)
         this.visited.add(newNode.strRepresentation)
      }
   }

   // Left
   if (col &gt; 0)
   {
       newState = node.state.clone();
       temp = newState[row][col - 1]
       newState[row][col - 1] = this.empty
       newState[row][col] = temp
       newNode = new Node(0, newState, row, col - 1, node.depth + 1)

       if (!this.visited.contains(newNode.strRepresentation))
       {
         newNode.value = newNode.depth + this.heuristic(newNode)
	 newNode.path = node.path + "L"
         this.queue.queue(newNode)
         this.visited.add(newNode.strRepresentation)
       }
   }

   // Right
   if (col &lt; node.size - 1)
   {
      newState = node.state.clone();
      temp = newState[row][col + 1]
      newState[row][col + 1] = this.empty
      newState[row][col] = temp
      newNode = new Node(0, newState, row, col + 1, node.depth + 1)

      if (!this.visited.contains(newNode.strRepresentation))
      {
         newNode.value = newNode.depth + this.heuristic(newNode)
         newNode.path = node.path + "R"
         this.queue.queue(newNode)
         this.visited.add(newNode.strRepresentation)
      }
   }
}
</code></pre>

All of the <code>if</code> statements are very similar; each is devoted to one of the possible moves. First we check a condition to see if the move at hand happens to be possible. The right move, for example, will be possible only if the empty tile column is less than the size of the board. If the move is possible, we create a <code>newState</code> by cloning the current state (cloning becomes necessary as arrays are reference types). We swap the empty tile with the corresponding element, we create a <code>newNode</code>, and finally queue it if – and only if – the node's state is not in the visited HashSet. We also calculate the value of the node as explained earlier (<em>f</em> = <em>g</em> + <em>h</em>) and we add the corresponding direction to the <code>path</code> variable.

<pre><code class="language-javascript">Array.prototype.clone = function() 
{
   return JSON.parse(JSON.stringify(this))
}
</code></pre>

Last but not least the heuristic function

<pre><code class="language-javascript">AStar.prototype.heuristic = function (node)
{
   return this.manhattanDistance(node);
}
</code></pre>

From this point on we'll start presenting and comparing results provided by the A* when accompanied by different heuristics. We'll see how the heuristic turns out to be an essential component during the search and how its cleverness can drastically reduce the time complexity of the algorithm.

### Misplaced Tiles

Before we dive into the interesting field of heuristics, let's point out an important note when calculating any heuristic: we never take into account the empty tile. If we do, then we could be overestimating the real cost of the shortest path to the goal state, thereby making the heuristic non-admissible. To illustrate this note, consider the following node:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae53922a-6568-4912-9d8f-154f8aee5454/sliding-tiles-puzzle-10-opt.jpg" alt="sliding-tiles-puzzle-10-opt" /></figure>

If we take into account the empty tile, then <em>h</em>=2, an overestimation of the shortest path to the goal configuration, which could be obtained just by moving the empty tile down. Thus the length of the shortest path to the goal configuration is 1 and we are overestimating.

To test our heuristics we'll be using one of the worst configurations for this puzzle – it requires 31 moves to be completed.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99041a5c-60f3-4136-b328-cb6a45318ced/sliding-tiles-puzzle-11-opt.jpg" alt="sliding-tiles-puzzle-11-opt" /></figure>

The A* algorithm will be executed when the <b>Solve</b> button is pressed. The <code>onclick</code> event associated with this button will trigger the <code>start</code> function whose body is up next.

<div class="break-out">

 <pre><code class="language-javascript">function start() {
   var init = new Node(0, [[6,4,7],[8,5,0],[3,2,1]], 1, 2, 0)
   var goal = new Node(0, [[1,2,3],[4,5,6],[7,8,0]], 2, 2, 0)

   var astar = new AStar(init, goal, 0)
   // To measure time taken by the algorithm
   var startTime = new Date()
   // Execute AStar
   var result = astar.execute()
   // To measure time taken by the algorithm
   var endTime = new Date()
   alert('Completed in: ' + (endTime - startTime) + ' milliseconds')

   var panel = document.getElementById('panel')
   panel.innerHTML = 'Solution: ' + result.path + ' Total steps: ' + result.path.length + '
'
   solution = result.path
}
</code></pre>
</div>

Note that we are going to measure the time taken by the algorithm in milliseconds. This is how we'll compare the various heuristics developed. The code of the misplaced tiles heuristic is very simple.

<div class="break-out">

 <pre><code class="language-javascript">AStar.prototype.misplacedTiles = function (node) 
{
   var result = 0;

   for (var i = 0; i &lt; node.state.length; i++)
   {
      for (var j = 0; j &lt; node.state[i].length; j++)
      if (node.state[i][j] != this.goal.state[i][j] &amp;&amp; node.state[i][j] != this.empty)
      result++;
   }

   return result;
}
</code></pre>
</div>

The result is the following

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaf6846a-93d8-4af6-842c-6aa7d23fa578/sliding-tiles-puzzle-12-opt.jpg" alt="sliding-tiles-puzzle-12-opt" /></figure>

The algorithm takes around four seconds to find a solution: not bad, but with more sophisticated, intelligent heuristics we can do better.

### Manhattan Distance

The <em>Manhattan distance</em> or <em>block distance</em> is defined as the sum of the absolute difference of their corresponding coordinates; that is:

<em>MD</em> = |<em>x</em>1−<em>x</em>2| + |<em>y</em>1−<em>y</em>2|

considering points A=(<em>x</em>1, <em>y</em>1) and B=(<em>x</em>2, <em>y</em>2).

It is admissible since for each tile it returns the minimum number of steps that will be required to move that tile into its goal position.

<pre><code class="language-javascript">AStar.prototype.manhattanDistance = function (node) 
{
   var result = 0;

   for (var i = 0; i &lt; node.state.length; i++)
   {
      for (var j = 0; j &lt; node.state[i].length; j++)
      {
         var elem = node.state[i][j]
         var found = false
         for (var h = 0; h &lt; this.goal.state.length; h++)
         {
            for (var k = 0; k &lt; this.goal.state[h].length; k++)
            {
               if (this.goal.state[h][k] == elem)
               {
                  result += Math.abs(h - i) + Math.abs(j - k)
                  found = true
                  break
               }
            }
            if (found) break
         }
      }
   }
   return result
}
</code></pre>

The result after applying this heuristic is the following:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3ac061e-71ff-4eb3-8889-05760310d01f/sliding-tiles-puzzle-13-opt.jpg" alt="sliding-tiles-puzzle-13-opt" /></figure>

Now we have obtained a significant reduction in the time, down to less than one second. The Manhattan distance heuristic provides more accurate information on how far we are from the goal configuration, thus we complete the puzzle sooner.

### MD + Linear Conflict

Even though the Manhattan distance heuristic greatly improves the time complexity of the algorithm, there are some necessary moves that are being missed. The <em>linear conflict</em> heuristic provides information on these necessary moves. Two tiles <em>tj</em> and <em>tk</em> are said to be in a linear conflict if: <em>tj</em> and <em>tk</em> are in the same line; the goal positions of <em>tj</em> and <em>tk</em> are both in that line; <em>tj</em> is to the right of <em>tk</em>; and the goal position of <em>tj</em> is to the left of the goal position of <em>tk</em>.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e3a10cd-78d2-4896-a9e8-c3a8678494c8/sliding-tiles-puzzle-14-opt.jpg" alt="sliding-tiles-puzzle-14-opt" /></figure>

In the left board, tiles 3 and 1 are located in their corresponding row but in an incorrect order. To get them to their goal positions we must move one of them down and then up again; these moves are not considered in the Manhattan distance heuristic. Important note: a tile cannot appear related to more than one conflict as solving a conflict may involve the resolution of other conflicts in the same row or column. Therefore, if tile 1 is related to tile 3 in a conflict then it cannot be related to a conflict with tile 2 as this may become an overestimation of the shortest path to a goal state and could make our heuristic non-admissible. The methods implementing this heuristic are presented in the next code.

<div class="break-out">

 <pre><code class="language-javascript">AStar.prototype.linearConflicts = function (node)
{
   var result = 0
   var state = node.state

   // Row Conflicts
   for (var i = 0; i &lt; state.length; i++)
      result += this.findConflicts(state, i, 1)

   // Column Conflicts
   for (var i = 0; i &lt; state[0].length; i++)
      result += this.findConflicts(state, i, 0)

   return result
}

AStar.prototype.findConflicts = function (state, i, dimension)
{
   var result = 0;
   var tilesRelated = new Array();

   // Loop foreach pair of elements in the row/column
   for (var h = 0; h &lt; state.length - 1 &amp;&amp; !tilesRelated.contains(h); h++)
   {
      for (var k = h + 1; k &lt; state.length &amp;&amp; !tilesRelated.contains(h); k++)
      {
         var moves = dimension == 1 
            ? this.inConflict(i, state[i][h], state[i][k], h, k, dimension) 
            : this.inConflict(i, state[h][i], state[k][i], h, k, dimension);

         if (moves == 0) continue;
         result += 2
         tilesRelated.push([h, k ])
         break
      }
   }

   return result;
}

AStar.prototype.inConflict = function (index, a, b, indexA, indexB, dimension)
{
   var indexGoalA = -1
   var indexGoalB = -1

   for (var c = 0; c = 0 &amp;&amp; indexGoalB &gt;= 0) &amp;&amp; 
	       ((indexA  indexGoalB) ||
          (indexA &gt; indexB &amp;&amp; indexGoalA &lt; indexGoalB))
                     ? 2
                     : 0;
}
</code></pre>
</div>

Since the linear conflicts heuristic calculates moves that do not intersect with the moves associated with the Manhattan distance, we can join them together to get more accurate information.

<pre><code class="language-javascript">AStar.prototype.heuristic = function (node)
{
   return this.manhattanDistance(node) + this.manhattanDistance(node);
}
</code></pre>

The result after having added the linear conflicts heuristic is the following:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf9f006a-4957-49b7-8d83-1771453914f2/sliding-tiles-puzzle-15-opt.jpg" alt="sliding-tiles-puzzle-15-opt" /></figure>

By adding the linear conflicts heuristic we have obtained a significant improvement. If we want to know the solution we can see it printed on the gray panel below.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21da6d03-c3b6-4411-b1cc-d622b5e709f4/sliding-tiles-puzzle-16-opt.jpg" alt="sliding-tiles-puzzle-16-opt" /></figure>

By pressing the <b>Show Step</b> button we can see a step of the solution. After pressing this button 31 times we'll see the sequence of moves that solve the puzzle.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d318c35-80b8-4373-b1f5-4a3e7e9a7d48/sliding-tiles-puzzle-17-opt.jpg" alt="sliding-tiles-puzzle-17-opt" /></figure>

## Conclusion

In this article, we have described an artificial intelligence by means of an A* search algorithm for the sliding tiles puzzle. We have examined the result offered by different heuristics and we have been able to find an efficient agent for the problem at hand. Now you can compete with friends and create artificial intelligences for this and many other puzzles and games!

### <span class="rh">Further Reading</span> on SmashingMag:

*   [A Beginner’s Guide To Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)
*   [How To Develop A Chat Bot With Node.js](https://www.smashingmagazine.com/2016/10/how-to-develop-a-chat-bot-with-node-js/)
*   [How Artificial Intelligence Is Changing Design](https://www.smashingmagazine.com/2017/01/algorithm-driven-design-how-artificial-intelligence-changing-design/)

{{< signature "rb, ml, og, il" >}}
