---
title: Top 10 CSS Table Designs
slug: top-10-css-table-designs
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0281fa0f-2ead-4ad5-9be0-82da7315e854/csstables2.gif
date: 2008-08-13T18:53:04.000Z
author: rickchristie
description: >-
  **Tables** have got to be one of the most difficult objects to style in the
  Web, thanks to the cryptic markup, the amount of detail we have to take care
  of, and lack of browser compatibility. A lot of time could be wasted on a
  single table although it's just a simple one.
categories:
  - Coding
  - CSS
  - Tables
---

_This article was written back in 2008 when the concept of [responsive web design](/2018/02/media-queries-responsive-design-2018/) hasn't been created just yet. You may want to check our newest article on [Resonsive Table Design patterns](/2019/01/table-design-patterns-web/) to see what designs work well on all devices, and are accessible to screan reader users, as well_.

**Tables** have got to be one of the most difficult objects to style in the Web, thanks to the cryptic markup, the amount of detail we have to take care of, and lack of browser compatibility. A lot of time could be wasted on a single table although it's just a simple one. This is where this article comes in handy. It will show you ten most easily implemented CSS table designs so you can style your tables in a _zap!_

<div class="c-felix-the-cat">
<h4 class="h3">Designing The Perfect Feature Comparison Table</h4>
<p>Feature comparison tables can aid in decision-making and add meaning to an otherwise too technical product specification sheet. Here are some tips and tricks how to design the perfect one. <a href="https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/" class="btn btn—small btn--blue">Read a related article →</a></p>
</div>

## First things first

We start with a **valid xhtml 1.0 strict** markup. Here is an example of a valid table markup:

<pre><code class="language-markup">&lt;!-- Table markup--&gt;
&lt;table id=&quot;...&quot;&gt;

	&lt;!-- Table header --&gt;
		&lt;thead&gt;
			&lt;tr&gt;
				&lt;th scope=&quot;col&quot; id=&quot;...&quot;&gt;...&lt;/th&gt;
				...
			&lt;/tr&gt;
		&lt;/thead&gt;
    
	&lt;!-- Table footer --&gt;
		&lt;tfoot&gt;
	        &lt;tr&gt;
	              &lt;td&gt;...&lt;/td&gt;
	        &lt;/tr&gt;
		&lt;/tfoot&gt;

	&lt;!-- Table body --&gt;
		&lt;tbody&gt;
			&lt;tr&gt;
				&lt;td&gt;...&lt;/td&gt;
				...
			&lt;/tr&gt;
			...
		&lt;/tbody&gt;

&lt;/table&gt;</code></pre>

You can read more about xhtml table markup in [HTML Dog's Table Section](https://www.htmldog.com/guides/htmlbeginner/tables/ "External site"). I have tested the tables below in Mozilla Firefox 3, IE 6 and 7, Opera 9.x and Safari. Also note that I apply a light blue color scheme to all of these tables to give the article a consistent look.

{{% feature-panel %}}

Before we start, let's review the general rule of thumb for styling of tables:

*   **Tables love space**. Set the width of tables carefully, according to the content. If you don't know the perfect width, simply set the `width` of the `table` to `100%`. Tables look nicer when they have "overwidth", and when it comes to tables too much width is definitely better than too little width.
*   **Cells need some padding**. Sure, each table cell relates to each other. But it doesn't mean that we have to pull them too close, right? Define some space between the cells, crammed up table cells are so much harder to read.
*   **Treat tables the way you treat content**. Tables are read similarly to the way we read text — except it's harder and it takes more time to read a table. So be careful with the amount of contrast you are giving to your table. Use soft colors — it's easier for the eyes. Don't treat your table like it's a graphical decoration. Make sure that the style you apply to it makes the content more readable, not the other way around.

Now that we are all set up let's get going, shall we?

## 1\. Horizontal Minimalist

Horizontal tables are tables that are read rather horizontally than vertically. Each entity is represented by a row. You can style these types of tables with minimalist style. Simply set enough `padding` to the cells (`td` and `th`) and put a 2 pixel border underneath the header.

<table id="hor-minimalist-a" summary="Employee Pay Sheet">
    <thead>
    	<tr>
        	<th scope="col">Employee</th>
            <th scope="col">Salary</th>
            <th scope="col">Bonus</th>
            <th scope="col">Supervisor</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<td>Stephen C. Cox</td>
            <td>$300</td>
            <td>$50</td>
            <td>Bob</td>
        </tr>
        <tr>
        	<td>Josephin Tan</td>
            <td>$150</td>
            <td>-</td>
            <td>Annie</td>
        </tr>
        <tr>
        	<td>Joyce Ming</td>
            <td>$200</td>
            <td>$35</td>
            <td>Andy</td>
        </tr>
        <tr>
        	<td>James A. Pentel</td>
            <td>$175</td>
            <td>$25</td>
            <td>Annie</td>
        </tr>
    </tbody>
</table>

Because horizontal tables are supposed to be scanned _horizontally_, clearing the border of the table increases the efficiency of the table. The lack of border, however, makes this table design hard to read if it has too many rows. To counter it we simply add 1 pixel border underneath all `td` elements:

<table id="hor-minimalist-b" summary="Employee Pay Sheet">
    <thead>
    	<tr>
        	<th scope="col">Employee</th>
            <th scope="col">Salary</th>
            <th scope="col">Bonus</th>
            <th scope="col">Supervisor</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<td>Stephen C. Cox</td>
            <td>$300</td>
            <td>$50</td>
            <td>Bob</td>
        </tr>
        <tr>
        	<td>Josephin Tan</td>
            <td>$150</td>
            <td>-</td>
            <td>Annie</td>
        </tr>
        <tr>
        	<td>Joyce Ming</td>
            <td>$200</td>
            <td>$35</td>
            <td>Andy</td>
        </tr>
        <tr>
        	<td>James A. Pentel</td>
            <td>$175</td>
            <td>$25</td>
            <td>Annie</td>
        </tr>
    </tbody>
</table>

The `tr:hover` rules are very useful to aid people reading a minimally designed tables. When the mouse cursor hovers over a cell, the rest of the cells in the same row highlights immediately, making it easier to track things if your tables have multiple columns.

*   **Important!**
Carefully finetune the typography and the padding between the cells
*   **Pros**
Very easy to style, good for simple tables
*   **Cons**
`tr:hover` rules don't work in IE 6, table can be confusing if it has too many columns
*   **Play with**
Color scheme, typography, `tr:hover` effects

## 2\. Vertical Minimalist

Although rarely used, vertically oriented tables are useful for categorizing or comparing descriptions of objects, with each entity represented by a column. We can style it in minimalistic style by adding whitespace separators between columns.

<table id="ver-minimalist" summary="Most Favorite Movies">
    <thead>
    	<tr>
        	<th scope="col">Comedy</th>
            <th scope="col">Adventure</th>
            <th scope="col">Action</th>
            <th scope="col">Children</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<td>Scary Movie</td>
            <td>Indiana Jones</td>
            <td>The Punisher</td>
            <td>Wall-E</td>
        </tr>
        <tr>
        	<td>Epic Movie</td>
            <td>Star Wars</td>
            <td>Bad Boys</td>
            <td>Madagascar</td>
        </tr>
        <tr>
        	<td>Spartan</td>
            <td>LOTR</td>
            <td>Die Hard</td>
            <td>Finding Nemo</td>
        </tr>
        <tr>
        	<td>Dr. Dolittle</td>
            <td>The Mummy</td>
            <td>300</td>
            <td>A Bug's Life</td>
        </tr>
    </tbody>
</table>

Add large `border-left` and `border-right` with the same color as background. You can use transparent borders if you want, but IE 6 screws it all up. Since this table is supposed to be read from top to bottom (vertically), adding `tr:hover` does not help and instead makes it harder to read the data. There is perhaps a Javascript-based solution which enables you to highlight the whole column when a `mouseover` event occurs, but that's beyond the scope of this article.

*   **Important!**
Carefully finetune the typography and the padding between the cells, do not add `tr:hover` effect
*   **Pros**
Easy to style, good for simple tables
*   **Cons**
Can not be used if background is not a solid block of color, suitable only for some tables
*   **Play With**
Color scheme and typography

<style>
#leftcolumn dl{display:block;margin-left:20px;}#leftcolumn dt{font-size:120%;color:#999;margin:10px 0 0;padding:0;}#leftcolumn dt.imp strong{font-weight:normal;color:red;}#leftcolumn dd{margin:0;padding:0;}#hor-minimalist-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;background:#fff;width:480px;border-collapse:collapse;text-align:left;margin:20px;}#hor-minimalist-a th{font-size:14px;font-weight:normal;color:#039;border-bottom:2px solid #6678b1;padding:10px 8px;}#hor-minimalist-a td{color:#669;padding:9px 8px 0;}#hor-minimalist-a tbody tr:hover td{color:#009;}#hor-minimalist-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;background:#fff;width:480px;border-collapse:collapse;text-align:left;margin:20px;}#hor-minimalist-b th{font-size:14px;font-weight:normal;color:#039;border-bottom:2px solid #6678b1;padding:10px 8px;}#hor-minimalist-b td{border-bottom:1px solid #ccc;color:#669;padding:6px 8px;}#hor-minimalist-b tbody tr:hover td{color:#009;}#ver-minimalist{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:30px 30px 30px 15px;}#ver-minimalist th{font-weight:normal;font-size:14px;border-bottom:2px solid #6678b1;border-right:30px solid #fff;border-left:30px solid #fff;color:#039;padding:8px 2px;}#ver-minimalist td{border-right:30px solid #fff;border-left:30px solid #fff;color:#669;padding:12px 2px 0;}#box-table-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#box-table-a th{font-size:13px;font-weight:normal;background:#b9c9fe;border-top:4px solid #aabcfe;border-bottom:1px solid #fff;color:#039;padding:8px;}#box-table-a td{background:#e8edff;border-bottom:1px solid #fff;color:#669;border-top:1px solid transparent;padding:8px;}#box-table-a tr:hover td{background:#d0dafd;color:#339;}#box-table-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:center;border-collapse:collapse;border-top:7px solid #9baff1;border-bottom:7px solid #9baff1;margin:20px;}#box-table-b th{font-size:13px;font-weight:normal;background:#e8edff;border-right:1px solid #9baff1;border-left:1px solid #9baff1;color:#039;padding:8px;}#box-table-b td{background:#e8edff;border-right:1px solid #aabcfe;border-left:1px solid #aabcfe;color:#669;padding:8px;}#hor-zebra{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#hor-zebra th{font-size:14px;font-weight:normal;color:#039;padding:10px 8px;}#hor-zebra td{color:#669;padding:8px;}#hor-zebra .odd{background:#e8edff;}#ver-zebra{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:0 20px 20px 20px;}#ver-zebra th{font-size:14px;font-weight:normal;border-right:1px solid #fff;border-left:1px solid #fff;color:#039;padding:12px 15px;}#ver-zebra td{border-right:1px solid #fff;border-left:1px solid #fff;color:#669;padding:8px 15px;}.vzebra-odd{background:#eff2ff;}.vzebra-even{background:#e8edff;}#ver-zebra #vzebra-adventure,#ver-zebra #vzebra-children{background:#d0dafd;border-bottom:1px solid #c8d4fd;}#ver-zebra #vzebra-comedy,#ver-zebra #vzebra-action{background:#dce4ff;border-bottom:1px solid #d6dfff;}#one-column-emphasis{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#one-column-emphasis th{font-size:14px;font-weight:normal;color:#039;padding:12px 15px;}#one-column-emphasis td{color:#669;border-top:1px solid #e8edff;padding:10px 15px;}.oce-first{background:#d0dafd;border-right:10px solid transparent;border-left:10px solid transparent;}#one-column-emphasis tr:hover td{color:#339;background:#eff2ff;}#newspaper-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;border:1px solid #69c;margin:20px;}#newspaper-a th{font-weight:normal;font-size:14px;color:#039;border-bottom:1px dashed #69c;padding:12px 17px;}#newspaper-a td{color:#669;padding:7px 17px;}#newspaper-a tbody tr:hover td{color:#339;background:#d0dafd;}#newspaper-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;border:1px solid #69c;margin:20px;}#newspaper-b th{font-weight:normal;font-size:14px;color:#039;padding:15px 10px 10px;}#newspaper-b tbody{background:#e8edff;}#newspaper-b td{color:#669;border-top:1px dashed #fff;padding:10px;}#newspaper-b tbody tr:hover td{color:#339;background:#d0dafd;}#newspaper-c{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;border:1px solid #6cf;margin:20px;}#newspaper-c th{font-weight:normal;font-size:13px;color:#039;text-transform:uppercase;border-right:1px solid #0865c2;border-top:1px solid #0865c2;border-left:1px solid #0865c2;border-bottom:1px solid #fff;padding:20px;}#newspaper-c td{color:#669;border-right:1px dashed #6cf;padding:10px 20px;}#rounded-corner{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#rounded-corner thead th.rounded-company{background:#b9c9fe url("/images/express-css-table-design/table-images/left.png") left -1px no-repeat;}#rounded-corner thead th.rounded-q4{background:#b9c9fe url("/images/express-css-table-design/table-images/right.png") right -1px no-repeat;}#rounded-corner th{font-weight:normal;font-size:13px;color:#039;background:#b9c9fe;padding:8px;}#rounded-corner td{background:#e8edff;border-top:1px solid #fff;color:#669;padding:8px;}#rounded-corner tfoot td.rounded-foot-left{background:#e8edff url("/images/express-css-table-design/table-images/botleft.png") left bottom no-repeat;}#rounded-corner tfoot td.rounded-foot-right{background:#e8edff url("/images/express-css-table-design/table-images/botright.png") right bottom no-repeat;}#rounded-corner tbody tr:hover td{background:#d0dafd;}#background-image{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;background:url("/images/express-css-table-design/table-images/blurry.jpg") 330px 59px no-repeat;margin:20px;}#background-image th{font-weight:normal;font-size:14px;color:#339;padding:12px;}#background-image td{color:#669;border-top:1px solid #fff;padding:9px 12px;}#background-image tfoot td{font-size:11px;}#background-image tbody td{background:url("/images/express-css-table-design/table-images/back.png");}* html #background-image tbody td{filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src='table-images/back.png',sizingMethod='crop');background:none;}#background-image tbody tr:hover td{color:#339;background:none;}#gradient-style{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#gradient-style th{font-size:13px;font-weight:normal;background:#b9c9fe url("/images/express-css-table-design/table-images/gradhead.png") repeat-x;border-top:2px solid #d3ddff;border-bottom:1px solid #fff;color:#039;padding:8px;}#gradient-style td{border-bottom:1px solid #fff;color:#669;border-top:1px solid #fff;background:#e8edff url("/images/express-css-table-design/table-images/gradback.png") repeat-x;padding:8px;}#gradient-style tfoot tr td{background:#e8edff;font-size:12px;color:#99c;}#gradient-style tbody tr:hover td{background:#d0dafd url("/images/express-css-table-design/table-images/gradhover.png") repeat-x;color:#339;}#pattern-style-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;background:url("/images/express-css-table-design/table-images/pattern.png");margin:20px;}#pattern-style-a thead tr{background:url("/images/express-css-table-design/table-images/pattern-head.png");}#pattern-style-a th{font-size:13px;font-weight:normal;border-bottom:1px solid #fff;color:#039;padding:8px;}#pattern-style-a td{border-bottom:1px solid #fff;color:#669;border-top:1px solid transparent;padding:8px;}#pattern-style-a tbody tr:hover td{color:#339;background:#fff;}#pattern-style-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;background:url("/images/express-css-table-design/table-images/patternb.png");margin:20px;}#pattern-style-b thead tr{background:url("/images/express-css-table-design/table-images/patternb-head.png");}#pattern-style-b th{font-size:13px;font-weight:normal;border-bottom:1px solid #fff;color:#039;padding:8px;}#pattern-style-b td{border-bottom:1px solid #fff;color:#669;border-top:1px solid transparent;padding:8px;}#pattern-style-b tbody tr:hover td{color:#339;background:#cdcdee;}.dp-highlighter{font-family:"Consolas", "Courier New", Courier, mono, serif;font-size:12px;background-color:#E7E5DC;width:99%;overflow:auto;padding-top:1px;margin:18px 0!important;}.dp-highlighter ol,.dp-highlighter ol li,.dp-highlighter ol li span{border:none;margin:0;padding:0;}.dp-highlighter a,.dp-highlighter a:hover{background:none;border:none;margin:0;padding:0;}.dp-highlighter .bar{padding-left:45px;}.dp-highlighter.collapsed .bar,.dp-highlighter.nogutter .bar{padding-left:0;}.dp-highlighter ol{list-style:decimal;background-color:#fff;color:#5C5C5C;margin:0 0 1px 45px !important;padding:0;}.dp-highlighter.nogutter ol,.dp-highlighter.nogutter ol li{list-style:none!important;margin-left:0!important;}.dp-highlighter ol li,.dp-highlighter .columns div{list-style:decimal-leading-zero;list-style-position:outside!important;border-left:3px solid #6CE26C;background-color:#F8F8F8;color:#5C5C5C;line-height:14px;margin:0!important;padding:0 3px 0 10px !important;}.dp-highlighter.nogutter ol li,.dp-highlighter.nogutter .columns div{border:0;}.dp-highlighter .columns{background-color:#F8F8F8;color:gray;overflow:hidden;width:100%;}.dp-highlighter .columns div{padding-bottom:5px;}.dp-highlighter ol li.alt{background-color:#FFF;color:inherit;}.dp-highlighter ol li span{color:black;background-color:inherit;}.dp-highlighter.collapsed ol{margin:0;}.dp-highlighter.collapsed ol li{display:none;}.dp-highlighter.printing{border:none;}.dp-highlighter.printing .tools{display:none!important;}.dp-highlighter.printing li{display:list-item!important;}.dp-highlighter .tools{font:9px Verdana, Geneva, Arial, Helvetica, sans-serif;color:silver;background-color:#f8f8f8;border-left:3px solid #6CE26C;padding:3px 8px 10px 10px;}.dp-highlighter.nogutter .tools{border-left:0;}.dp-highlighter.collapsed .tools{border-bottom:0;}.dp-highlighter .tools a{font-size:9px;color:#a0a0a0;background-color:inherit;text-decoration:none;margin-right:10px;}.dp-highlighter .tools a:hover{color:red;background-color:inherit;text-decoration:underline;}.dp-about{background-color:#fff;color:#333;margin:0;padding:0;}.dp-about table{width:100%;height:100%;font-size:11px;font-family:Tahoma, Verdana, Arial, sans-serif!important;}.dp-about td{vertical-align:top;padding:10px;}.dp-about .copy{border-bottom:1px solid #ACA899;height:95%;}.dp-about .title{color:red;background-color:inherit;font-weight:bold;}.dp-about .para{margin:0 0 4px;}.dp-about .footer{background-color:#ECEADB;color:#333;border-top:1px solid #fff;text-align:right;}.dp-about .close{font-size:11px;font-family:Tahoma, Verdana, Arial, sans-serif!important;background-color:#ECEADB;color:#333;width:60px;height:22px;}.dp-highlighter .comment,.dp-highlighter .comments{color:#008200;background-color:inherit;}.dp-highlighter .string{color:blue;background-color:inherit;}.dp-highlighter .keyword{color:#069;font-weight:bold;background-color:inherit;}.dp-highlighter .preprocessor{color:gray;background-color:inherit;}
</style>

## 3\. Box

The most dependable of all styles, the box style works for all kinds of tables. Pick a good color scheme and then distribute `background-color` to all the cells. Don't forget to accentuate the differences of each cell by defining `border` as a separator. An example of a box style table is the following table:

<table id="box-table-a" summary="Employee Pay Sheet">
    <thead>
    	<tr>
        	<th scope="col">Employee</th>
            <th scope="col">Salary</th>
            <th scope="col">Bonus</th>
            <th scope="col">Supervisor</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<td>Stephen C. Cox</td>
            <td>$300</td>
            <td>$50</td>
            <td>Bob</td>
        </tr>
        <tr>
        	<td>Josephin Tan</td>
            <td>$150</td>
            <td>-</td>
            <td>Annie</td>
        </tr>
        <tr>
        	<td>Joyce Ming</td>
            <td>$200</td>
            <td>$35</td>
            <td>Andy</td>
        </tr>
        <tr>
        	<td>James A. Pentel</td>
            <td>$175</td>
            <td>$25</td>
            <td>Annie</td>
        </tr>
    </tbody>
</table>

<table id="box-table-b" summary="Most Favorit Movies">
    <thead>
    	<tr>
        	<th scope="col">Comedy</th>
            <th scope="col">Adventure</th>
            <th scope="col">Action</th>
            <th scope="col">Children</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<td>Scary Movie</td>
            <td>Indiana Jones</td>
            <td>The Punisher</td>
            <td>Wall-E</td>
        </tr>
        <tr>
        	<td>Epic Movie</td>
            <td>Star Wars</td>
            <td>Bad Boys</td>
            <td>Madagascar</td>
        </tr>
        <tr>
        	<td>Spartan</td>
            <td>LOTR</td>
            <td>Die Hard</td>
            <td>Finding Nemo</td>
        </tr>
        <tr>
        	<td>Dr. Dolittle</td>
            <td>The Mummy</td>
            <td>300</td>
            <td>A Bug's Life</td>
        </tr>
    </tbody>
</table>

This style is nowadays probably the most used style. The tricky part is actually trying to find the color scheme that matches with your site. If your site is heavy on graphics, it will be pretty hard to use this style.

*   **Important!**
Choose a color scheme that matches with your site
*   **Pros**
Easy to style, flexible for large or small tables
*   **Cons**
Choosing the perfect color scheme could be tricky
*   **Play with**
Colors and borders, use `dashed` or `dotted` to achieve cute effects, typography, icons

## 4\. Horizontal Zebra

Zebra-tables are pretty attractive and usable. The alternating background color can serve as a visual cue for people when scanning the table. To style a table as zebra, simply put a `class="odd"` to every odd ordered `tr` tag and define a style for it (e.g. using if ($count % 2) then _even class_ else _odd class_ in PHP).

<pre><code class="language-php">...

  &lt;tr class=&quot;odd&quot;&gt;
		   &lt;td&gt;...&lt;/td&gt;
		   ...
		&lt;/tr&gt;

		&lt;tr&gt;
		   &lt;td&gt;...&lt;/td&gt;
		   ...
		&lt;/tr&gt;

	...</code></pre>

<table id="hor-zebra" summary="Employee Pay Sheet">
    <thead>
    	<tr>
        	<th scope="col">Employee</th>
            <th scope="col">Salary</th>
            <th scope="col">Bonus</th>
            <th scope="col">Supervisor</th>
        </tr>
    </thead>
    <tbody>
    	<tr class="odd">
        	<td>Stephen C. Cox</td>
            <td>$300</td>
            <td>$50</td>
            <td>Bob</td>
        </tr>
        <tr>
        	<td>Josephin Tan</td>
            <td>$150</td>
            <td>-</td>
            <td>Annie</td>
        </tr>
        <tr class="odd">
        	<td>Joyce Ming</td>
            <td>$200</td>
            <td>$35</td>
            <td>Andy</td>
        </tr>
        <tr>
        	<td>James A. Pentel</td>
            <td>$175</td>
            <td>$25</td>
            <td>Annie</td>
        </tr>
    </tbody>
</table>

*   **Important!**
Do not put too much contrast on the zebra colors, you can blind your users
*   **Pros**
The zebra pattern can help people to scan the table
*   **Cons**
Adding `class="odd"` manually can be very tedious for large tables, many content management systems do not provide _even/odd_ features on a table loop, hence picking the color scheme may be tricky
*   **Play With**
Contrasting color, borders, typography, icons

## 5\. Vertical Zebra Style

Vertical zebra is easier to style than the horizontal one, as we can make use of `colgroup` and `col` elements to distribute column classes. However, the markup becomes a little bit heavier:

<pre><code class="language-markup tmp-xml">&lt;table&gt;

		&lt;!-- Colgroup --&gt;
	   &lt;colgroup&gt;
	      &lt;col class=&quot;vzebra-odd&quot;&gt; 
	      &lt;col class=&quot;vzebra-even&quot;&gt;
	      &lt;col class=&quot;vzebra-odd&quot;&gt;
	      &lt;col class=&quot;vzebra-even&quot;&gt;
	   &lt;/colgroup&gt;

		&lt;!-- Table header --&gt;
	   &lt;thead&gt;
	      &lt;tr&gt;
	         &lt;th scope=&quot;col&quot; id=&quot;vzebra-comedy&quot;&gt;Employee&lt;/th&gt;
	         ...
	      &lt;/tr&gt;
	   &lt;/thead&gt;

	   ...
&lt;/table&gt;</code></pre>

The `colgroup` element actually applies a style or class to the table, columnwise. Instead of tediously applying `class` for the first `td` or `th` element, we can use a more convenient `colgroup`-tag. For more information about `colgroup` visit [this page](https://www.htmldog.com/guides/htmladvanced/tables/ "External site, html dog's explanation").

<table id="ver-zebra" summary="Most Favorite Movies">

    	<col />
    	<col />
    	<col />
        <col />

    <thead>
    	<tr>
        	<th scope="col">Comedy</th>
            <th scope="col">Adventure</th>
            <th scope="col">Action</th>
            <th scope="col">Children</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<td>Scary Movie</td>
            <td>Indiana Jones</td>
            <td>The Punisher</td>
            <td>Wall-E</td>
        </tr>
        <tr>
        	<td>Epic Movie</td>
            <td>Star Wars</td>
            <td>Bad Boys</td>
            <td>Madagascar</td>
        </tr>
        <tr>
        	<td>Spartan</td>
            <td>LOTR</td>
            <td>Die Hard</td>
            <td>Finding Nemo</td>
        </tr>
        <tr>
        	<td>Dr. Dolittle</td>
            <td>The Mummy</td>
            <td>300</td>
            <td>A Bug's Life</td>
        </tr>
    </tbody>
</table>

Although perhaps more suitable for vertically-oriented table, this zebra-style can also be used for any other kind of tables.

*   **Important!**
Do not put too much contrast on the zebra colors, you can blind your viewer
*   **Pros**
Suitable for all types of tables
*   **Cons**
Choosing the color scheme could be tricky, need to add `colgroup` elements
*   **Play With**
Contrasting color, borders, `colgroup` and `col`, icons and typography

<style>
#leftcolumn dl{display:block;margin-left:20px;}#leftcolumn dt{font-size:120%;color:#999;margin:10px 0 0;padding:0;}#leftcolumn dt.imp strong{font-weight:normal;color:red;}#leftcolumn dd{margin:0;padding:0;}#hor-minimalist-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;background:#fff;width:480px;border-collapse:collapse;text-align:left;margin:20px;}#hor-minimalist-a th{font-size:14px;font-weight:normal;color:#039;border-bottom:2px solid #6678b1;padding:10px 8px;}#hor-minimalist-a td{color:#669;padding:9px 8px 0;}#hor-minimalist-a tbody tr:hover td{color:#009;}#hor-minimalist-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;background:#fff;width:480px;border-collapse:collapse;text-align:left;margin:20px;}#hor-minimalist-b th{font-size:14px;font-weight:normal;color:#039;border-bottom:2px solid #6678b1;padding:10px 8px;}#hor-minimalist-b td{border-bottom:1px solid #ccc;color:#669;padding:6px 8px;}#hor-minimalist-b tbody tr:hover td{color:#009;}#ver-minimalist{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:30px 30px 30px 15px;}#ver-minimalist th{font-weight:normal;font-size:14px;border-bottom:2px solid #6678b1;border-right:30px solid #fff;border-left:30px solid #fff;color:#039;padding:8px 2px;}#ver-minimalist td{border-right:30px solid #fff;border-left:30px solid #fff;color:#669;padding:12px 2px 0;}#box-table-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#box-table-a th{font-size:13px;font-weight:normal;background:#b9c9fe;border-top:4px solid #aabcfe;border-bottom:1px solid #fff;color:#039;padding:8px;}#box-table-a td{background:#e8edff;border-bottom:1px solid #fff;color:#669;border-top:1px solid transparent;padding:8px;}#box-table-a tr:hover td{background:#d0dafd;color:#339;}#box-table-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:center;border-collapse:collapse;border-top:7px solid #9baff1;border-bottom:7px solid #9baff1;margin:20px;}#box-table-b th{font-size:13px;font-weight:normal;background:#e8edff;border-right:1px solid #9baff1;border-left:1px solid #9baff1;color:#039;padding:8px;}#box-table-b td{background:#e8edff;border-right:1px solid #aabcfe;border-left:1px solid #aabcfe;color:#669;padding:8px;}#hor-zebra{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#hor-zebra th{font-size:14px;font-weight:normal;color:#039;padding:10px 8px;}#hor-zebra td{color:#669;padding:8px;}#hor-zebra .odd{background:#e8edff;}#ver-zebra{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:0 20px 20px 20px;}#ver-zebra th{font-size:14px;font-weight:normal;border-right:1px solid #fff;border-left:1px solid #fff;color:#039;padding:12px 15px;}#ver-zebra td{border-right:1px solid #fff;border-left:1px solid #fff;color:#669;padding:8px 15px;}.vzebra-odd{background:#eff2ff;}.vzebra-even{background:#e8edff;}#ver-zebra #vzebra-adventure,#ver-zebra #vzebra-children{background:#d0dafd;border-bottom:1px solid #c8d4fd;}#ver-zebra #vzebra-comedy,#ver-zebra #vzebra-action{background:#dce4ff;border-bottom:1px solid #d6dfff;}#one-column-emphasis{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#one-column-emphasis th{font-size:14px;font-weight:normal;color:#039;padding:12px 15px;}#one-column-emphasis td{color:#669;border-top:1px solid #e8edff;padding:10px 15px;}.oce-first{background:#d0dafd;border-right:10px solid transparent;border-left:10px solid transparent;}#one-column-emphasis tr:hover td{color:#339;background:#eff2ff;}#newspaper-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;border:1px solid #69c;margin:20px;}#newspaper-a th{font-weight:normal;font-size:14px;color:#039;border-bottom:1px dashed #69c;padding:12px 17px;}#newspaper-a td{color:#669;padding:7px 17px;}#newspaper-a tbody tr:hover td{color:#339;background:#d0dafd;}#newspaper-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;border:1px solid #69c;margin:20px;}#newspaper-b th{font-weight:normal;font-size:14px;color:#039;padding:15px 10px 10px;}#newspaper-b tbody{background:#e8edff;}#newspaper-b td{color:#669;border-top:1px dashed #fff;padding:10px;}#newspaper-b tbody tr:hover td{color:#339;background:#d0dafd;}#newspaper-c{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;border:1px solid #6cf;margin:20px;}#newspaper-c th{font-weight:normal;font-size:13px;color:#039;text-transform:uppercase;border-right:1px solid #0865c2;border-top:1px solid #0865c2;border-left:1px solid #0865c2;border-bottom:1px solid #fff;padding:20px;}#newspaper-c td{color:#669;border-right:1px dashed #6cf;padding:10px 20px;}#rounded-corner{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#rounded-corner thead th.rounded-company{background:#b9c9fe url("/images/express-css-table-design/table-images/left.png") left -1px no-repeat;}#rounded-corner thead th.rounded-q4{background:#b9c9fe url("/images/express-css-table-design/table-images/right.png") right -1px no-repeat;}#rounded-corner th{font-weight:normal;font-size:13px;color:#039;background:#b9c9fe;padding:8px;}#rounded-corner td{background:#e8edff;border-top:1px solid #fff;color:#669;padding:8px;}#rounded-corner tfoot td.rounded-foot-left{background:#e8edff url("/images/express-css-table-design/table-images/botleft.png") left bottom no-repeat;}#rounded-corner tfoot td.rounded-foot-right{background:#e8edff url("/images/express-css-table-design/table-images/botright.png") right bottom no-repeat;}#rounded-corner tbody tr:hover td{background:#d0dafd;}#background-image{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;background:url("/images/express-css-table-design/table-images/blurry.jpg") 330px 59px no-repeat;margin:20px;}#background-image th{font-weight:normal;font-size:14px;color:#339;padding:12px;}#background-image td{color:#669;border-top:1px solid #fff;padding:9px 12px;}#background-image tfoot td{font-size:11px;}#background-image tbody td{background:url("/images/express-css-table-design/table-images/back.png");}* html #background-image tbody td{filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src='table-images/back.png',sizingMethod='crop');background:none;}#background-image tbody tr:hover td{color:#339;background:none;}#gradient-style{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#gradient-style th{font-size:13px;font-weight:normal;background:#b9c9fe url("/images/express-css-table-design/table-images/gradhead.png") repeat-x;border-top:2px solid #d3ddff;border-bottom:1px solid #fff;color:#039;padding:8px;}#gradient-style td{border-bottom:1px solid #fff;color:#669;border-top:1px solid #fff;background:#e8edff url("/images/express-css-table-design/table-images/gradback.png") repeat-x;padding:8px;}#gradient-style tfoot tr td{background:#e8edff;font-size:12px;color:#99c;}#gradient-style tbody tr:hover td{background:#d0dafd url("/images/express-css-table-design/table-images/gradhover.png") repeat-x;color:#339;}#pattern-style-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;background:url("/images/express-css-table-design/table-images/pattern.png");margin:20px;}#pattern-style-a thead tr{background:url("/images/express-css-table-design/table-images/pattern-head.png");}#pattern-style-a th{font-size:13px;font-weight:normal;border-bottom:1px solid #fff;color:#039;padding:8px;}#pattern-style-a td{border-bottom:1px solid #fff;color:#669;border-top:1px solid transparent;padding:8px;}#pattern-style-a tbody tr:hover td{color:#339;background:#fff;}#pattern-style-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;background:url("/images/express-css-table-design/table-images/patternb.png");margin:20px;}#pattern-style-b thead tr{background:url("/images/express-css-table-design/table-images/patternb-head.png");}#pattern-style-b th{font-size:13px;font-weight:normal;border-bottom:1px solid #fff;color:#039;padding:8px;}#pattern-style-b td{border-bottom:1px solid #fff;color:#669;border-top:1px solid transparent;padding:8px;}#pattern-style-b tbody tr:hover td{color:#339;background:#cdcdee;}.dp-highlighter{font-family:"Consolas", "Courier New", Courier, mono, serif;font-size:12px;background-color:#E7E5DC;width:99%;overflow:auto;padding-top:1px;margin:18px 0!important;}.dp-highlighter ol,.dp-highlighter ol li,.dp-highlighter ol li span{border:none;margin:0;padding:0;}.dp-highlighter a,.dp-highlighter a:hover{background:none;border:none;margin:0;padding:0;}.dp-highlighter .bar{padding-left:45px;}.dp-highlighter.collapsed .bar,.dp-highlighter.nogutter .bar{padding-left:0;}.dp-highlighter ol{list-style:decimal;background-color:#fff;color:#5C5C5C;margin:0 0 1px 45px !important;padding:0;}.dp-highlighter.nogutter ol,.dp-highlighter.nogutter ol li{list-style:none!important;margin-left:0!important;}.dp-highlighter ol li,.dp-highlighter .columns div{list-style:decimal-leading-zero;list-style-position:outside!important;border-left:3px solid #6CE26C;background-color:#F8F8F8;color:#5C5C5C;line-height:14px;margin:0!important;padding:0 3px 0 10px !important;}.dp-highlighter.nogutter ol li,.dp-highlighter.nogutter .columns div{border:0;}.dp-highlighter .columns{background-color:#F8F8F8;color:gray;overflow:hidden;width:100%;}.dp-highlighter .columns div{padding-bottom:5px;}.dp-highlighter ol li.alt{background-color:#FFF;color:inherit;}.dp-highlighter ol li span{color:black;background-color:inherit;}.dp-highlighter.collapsed ol{margin:0;}.dp-highlighter.collapsed ol li{display:none;}.dp-highlighter.printing{border:none;}.dp-highlighter.printing .tools{display:none!important;}.dp-highlighter.printing li{display:list-item!important;}.dp-highlighter .tools{font:9px Verdana, Geneva, Arial, Helvetica, sans-serif;color:silver;background-color:#f8f8f8;border-left:3px solid #6CE26C;padding:3px 8px 10px 10px;}.dp-highlighter.nogutter .tools{border-left:0;}.dp-highlighter.collapsed .tools{border-bottom:0;}.dp-highlighter .tools a{font-size:9px;color:#a0a0a0;background-color:inherit;text-decoration:none;margin-right:10px;}.dp-highlighter .tools a:hover{color:red;background-color:inherit;text-decoration:underline;}.dp-about{background-color:#fff;color:#333;margin:0;padding:0;}.dp-about table{width:100%;height:100%;font-size:11px;font-family:Tahoma, Verdana, Arial, sans-serif!important;}.dp-about td{vertical-align:top;padding:10px;}.dp-about .copy{border-bottom:1px solid #ACA899;height:95%;}.dp-about .title{color:red;background-color:inherit;font-weight:bold;}.dp-about .para{margin:0 0 4px;}.dp-about .footer{background-color:#ECEADB;color:#333;border-top:1px solid #fff;text-align:right;}.dp-about .close{font-size:11px;font-family:Tahoma, Verdana, Arial, sans-serif!important;background-color:#ECEADB;color:#333;width:60px;height:22px;}.dp-highlighter .comment,.dp-highlighter .comments{color:#008200;background-color:inherit;}.dp-highlighter .string{color:blue;background-color:inherit;}.dp-highlighter .keyword{color:#069;font-weight:bold;background-color:inherit;}.dp-highlighter .preprocessor{color:gray;background-color:inherit;}
</style>

## 6\. One Column Emphasis

In some tables, some particular column may have a higher weight than the other columns. If that's the case, you can use `colgroup` and `col` to make that particular column stand out. In the example below, the first column serves as the starting point to read, so it is emphasized, just like we emphasize the first letter of the paragraph as drop caps:

<table id="one-column-emphasis" summary="2007 Major IT Companies' Profit">

    	<col />

    <thead>
    	<tr>
        	<th scope="col">Company</th>
            <th scope="col">Q1</th>
            <th scope="col">Q2</th>
            <th scope="col">Q3</th>
            <th scope="col">Q4</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<td>Microsoft</td>
            <td>20.3</td>
            <td>30.5</td>
            <td>23.5</td>
            <td>40.3</td>
        </tr>
        <tr>
        	<td>Google</td>
            <td>50.2</td>
            <td>40.63</td>
            <td>45.23</td>
            <td>39.3</td>
        </tr>
        <tr>
        	<td>Apple</td>
            <td>25.4</td>
            <td>30.2</td>
            <td>33.3</td>
            <td>36.7</td>
        </tr>
        <tr>
        	<td>IBM</td>
            <td>20.4</td>
            <td>15.6</td>
            <td>22.3</td>
            <td>29.3</td>
        </tr>
    </tbody>
</table>

You can also use one-column-emphasis-technique to highlight something important, say the column containing totals of an accounting table, or in a comparison table — for computer specification perhaps, the winning entity (column).

*   **Important!**
Be careful, don't overdo the emphasis or the column will _jump out_, distracting the effort to read the rest of the columns.
*   **Pros**
Very effective when used in certain kind of tables
*   **Cons**
The necessary `tr:hover` effect does not work in IE, suitable for certain types of tables only
*   **Play with**
Color scheme, typography, icons and `tr:hover` effects

## 7\. Newspaper

To achieve the so-called _newspaper effect_, apply `border` to `table` element and play with the cells inside. A quick, minimalistic newspaper style can look like this:

<table id="newspaper-a" summary="2007 Major IT Companies' Profit">
    <thead>
    	<tr>
        	<th scope="col">Company</th>
            <th scope="col">Q1</th>
            <th scope="col">Q2</th>
            <th scope="col">Q3</th>
            <th scope="col">Q4</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<td>Microsoft</td>
            <td>20.3</td>
            <td>30.5</td>
            <td>23.5</td>
            <td>40.3</td>
        </tr>
        <tr>
        	<td>Google</td>
            <td>50.2</td>
            <td>40.63</td>
            <td>45.23</td>
            <td>39.3</td>
        </tr>
        <tr>
        	<td>Apple</td>
            <td>25.4</td>
            <td>30.2</td>
            <td>33.3</td>
            <td>36.7</td>
        </tr>
        <tr>
        	<td>IBM</td>
            <td>20.4</td>
            <td>15.6</td>
            <td>22.3</td>
            <td>29.3</td>
        </tr>
    </tbody>
</table>

Simply play with color scheme, borders, padding, backgrounds, and `tr:hover` effects of the cells (`td` and `th`). Other alternatives are presented below:

<table id="newspaper-b" summary="2007 Major IT Companies' Profit">
    <thead>
    	<tr>
        	<th scope="col">Company</th>
            <th scope="col">Q1</th>
            <th scope="col">Q2</th>
            <th scope="col">Q3</th>
            <th scope="col">Q4</th>
        </tr>
    </thead>
        <tfoot>
    	<tr>
        	<td colspan="5"><em>The above data were fictional and made up, please do not sue me</em></td>
        </tr>
    </tfoot>
    <tbody>
    	<tr>
        	<td>Microsoft</td>
            <td>20.3</td>
            <td>30.5</td>
            <td>23.5</td>
            <td>40.3</td>
        </tr>
        <tr>
        	<td>Google</td>
            <td>50.2</td>
            <td>40.63</td>
            <td>45.23</td>

            <td>39.3</td>
        </tr>
        <tr>
        	<td>Apple</td>
            <td>25.4</td>
            <td>30.2</td>
            <td>33.3</td>
            <td>36.7</td>
        </tr>
        <tr>
        	<td>IBM</td>
            <td>20.4</td>
            <td>15.6</td>
            <td>22.3</td>
            <td>29.3</td>
        </tr>
    </tbody>
</table>

<table id="newspaper-c" summary="Personal Movie Rating">
    <thead>
    	<tr>
        	<th scope="col">Favorite</th>
            <th scope="col">Great</th>
            <th scope="col">Nice</th>
            <th scope="col">Bad</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<td>Passion of the Christ</td>
            <td>Bourne Ultimatum</td>
            <td>Shoot 'Em Up</td>
            <td>Ali</td>
        </tr>
        <tr>
        	<td>The Big Fish</td>
            <td>The Mummy</td>
            <td>Apocalypto</td>
            <td>Monster</td>
        </tr>
        <tr>
        	<td>Shawshank Redemption</td>
            <td>Cold Mountain</td>
            <td>Indiana Jones</td>
            <td>Dead or Alive</td>
        </tr>
        <tr>
        	<td>Greatest Story Ever Told</td>
            <td>I Am Legend</td>
            <td>Star Wars</td>
            <td>Saw 3</td>
        </tr>
    </tbody>
</table>

*   **Important!**
Be careful with `border-collapse`, do not lose the signature border around the table!
*   **Pros**
Gives a royal, authoritative aura to a table
*   **Cons**
Unsuitable for large tables (it loses it's charm on large tables)
*   **Play With**
 Typography, color scheme, background, border, padding, and `tr:hover` effects

## 8\. Rounded Corner

Rounded corners are slick and modern, and it's easy to apply it to a table, although you need to fire up Photoshop for this. Create images for all four corners of your table. Theoretically, we can make use of the nesting `tr` and `td`-elements to place the left and right corners of the table without adding additional markup. Unfortunately, IE 6 goes berserk and the table appears ugly, so the most stable way to do this is to put `ID` or `class` to all four corner cells of the table. Please consider the example below:

<table id="rounded-corner" summary="2007 Major IT Companies' Profit">
    <thead>
    	<tr>
        	<th scope="col" class="rounded-company">Company</th>
            <th scope="col" class="rounded-q1">Q1</th>
            <th scope="col" class="rounded-q2">Q2</th>
            <th scope="col" class="rounded-q3">Q3</th>
            <th scope="col" class="rounded-q4">Q4</th>
        </tr>
    </thead>
        <tfoot>
    	<tr>
        	<td colspan="4" class="rounded-foot-left"><em>The above data were fictional and made up, please do not sue me</em></td>
        	<td class="rounded-foot-right">&nbsp;</td>
        </tr>
    </tfoot>
    <tbody>
    	<tr>
        	<td>Microsoft</td>
            <td>20.3</td>
            <td>30.5</td>
            <td>23.5</td>
            <td>40.3</td>
        </tr>
        <tr>
        	<td>Google</td>
            <td>50.2</td>
            <td>40.63</td>
            <td>45.23</td>
            <td>39.3</td>
        </tr>
        <tr>
        	<td>Apple</td>
            <td>25.4</td>
            <td>30.2</td>
            <td>33.3</td>
            <td>36.7</td>
        </tr>
        <tr>
        	<td>IBM</td>
            <td>20.4</td>
            <td>15.6</td>
            <td>22.3</td>
            <td>29.3</td>
        </tr>
    </tbody>
</table>

*   **Pros**
Great if you want untraditional table, probably the only viable option you have if your website uses rounded corners heavily
*   **Cons**
Takes longer to style, requires images
*   **Play With**
Color scheme, corner variations, typography, `tr:hover` effects, icons

<style>
#leftcolumn dl{display:block;margin-left:20px;}#leftcolumn dt{font-size:120%;color:#999;margin:10px 0 0;padding:0;}#leftcolumn dt.imp strong{font-weight:normal;color:red;}#leftcolumn dd{margin:0;padding:0;}#hor-minimalist-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;background:#fff;width:480px;border-collapse:collapse;text-align:left;margin:20px;}#hor-minimalist-a th{font-size:14px;font-weight:normal;color:#039;border-bottom:2px solid #6678b1;padding:10px 8px;}#hor-minimalist-a td{color:#669;padding:9px 8px 0;}#hor-minimalist-a tbody tr:hover td{color:#009;}#hor-minimalist-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;background:#fff;width:480px;border-collapse:collapse;text-align:left;margin:20px;}#hor-minimalist-b th{font-size:14px;font-weight:normal;color:#039;border-bottom:2px solid #6678b1;padding:10px 8px;}#hor-minimalist-b td{border-bottom:1px solid #ccc;color:#669;padding:6px 8px;}#hor-minimalist-b tbody tr:hover td{color:#009;}#ver-minimalist{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:30px 30px 30px 15px;}#ver-minimalist th{font-weight:normal;font-size:14px;border-bottom:2px solid #6678b1;border-right:30px solid #fff;border-left:30px solid #fff;color:#039;padding:8px 2px;}#ver-minimalist td{border-right:30px solid #fff;border-left:30px solid #fff;color:#669;padding:12px 2px 0;}#box-table-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#box-table-a th{font-size:13px;font-weight:normal;background:#b9c9fe;border-top:4px solid #aabcfe;border-bottom:1px solid #fff;color:#039;padding:8px;}#box-table-a td{background:#e8edff;border-bottom:1px solid #fff;color:#669;border-top:1px solid transparent;padding:8px;}#box-table-a tr:hover td{background:#d0dafd;color:#339;}#box-table-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:center;border-collapse:collapse;border-top:7px solid #9baff1;border-bottom:7px solid #9baff1;margin:20px;}#box-table-b th{font-size:13px;font-weight:normal;background:#e8edff;border-right:1px solid #9baff1;border-left:1px solid #9baff1;color:#039;padding:8px;}#box-table-b td{background:#e8edff;border-right:1px solid #aabcfe;border-left:1px solid #aabcfe;color:#669;padding:8px;}#hor-zebra{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#hor-zebra th{font-size:14px;font-weight:normal;color:#039;padding:10px 8px;}#hor-zebra td{color:#669;padding:8px;}#hor-zebra .odd{background:#e8edff;}#ver-zebra{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:0 20px 20px 20px;}#ver-zebra th{font-size:14px;font-weight:normal;border-right:1px solid #fff;border-left:1px solid #fff;color:#039;padding:12px 15px;}#ver-zebra td{border-right:1px solid #fff;border-left:1px solid #fff;color:#669;padding:8px 15px;}.vzebra-odd{background:#eff2ff;}.vzebra-even{background:#e8edff;}#ver-zebra #vzebra-adventure,#ver-zebra #vzebra-children{background:#d0dafd;border-bottom:1px solid #c8d4fd;}#ver-zebra #vzebra-comedy,#ver-zebra #vzebra-action{background:#dce4ff;border-bottom:1px solid #d6dfff;}#one-column-emphasis{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#one-column-emphasis th{font-size:14px;font-weight:normal;color:#039;padding:12px 15px;}#one-column-emphasis td{color:#669;border-top:1px solid #e8edff;padding:10px 15px;}.oce-first{background:#d0dafd;border-right:10px solid transparent;border-left:10px solid transparent;}#one-column-emphasis tr:hover td{color:#339;background:#eff2ff;}#newspaper-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;border:1px solid #69c;margin:20px;}#newspaper-a th{font-weight:normal;font-size:14px;color:#039;border-bottom:1px dashed #69c;padding:12px 17px;}#newspaper-a td{color:#669;padding:7px 17px;}#newspaper-a tbody tr:hover td{color:#339;background:#d0dafd;}#newspaper-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;border:1px solid #69c;margin:20px;}#newspaper-b th{font-weight:normal;font-size:14px;color:#039;padding:15px 10px 10px;}#newspaper-b tbody{background:#e8edff;}#newspaper-b td{color:#669;border-top:1px dashed #fff;padding:10px;}#newspaper-b tbody tr:hover td{color:#339;background:#d0dafd;}#newspaper-c{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;border:1px solid #6cf;margin:20px;}#newspaper-c th{font-weight:normal;font-size:13px;color:#039;text-transform:uppercase;border-right:1px solid #0865c2;border-top:1px solid #0865c2;border-left:1px solid #0865c2;border-bottom:1px solid #fff;padding:20px;}#newspaper-c td{color:#669;border-right:1px dashed #6cf;padding:10px 20px;}#rounded-corner{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#rounded-corner thead th.rounded-company{background:#b9c9fe url("/images/express-css-table-design/table-images/left.png") left -1px no-repeat;}#rounded-corner thead th.rounded-q4{background:#b9c9fe url("/images/express-css-table-design/table-images/right.png") right -1px no-repeat;}#rounded-corner th{font-weight:normal;font-size:13px;color:#039;background:#b9c9fe;padding:8px;}#rounded-corner td{background:#e8edff;border-top:1px solid #fff;color:#669;padding:8px;}#rounded-corner tfoot td.rounded-foot-left{background:#e8edff url("/images/express-css-table-design/table-images/botleft.png") left bottom no-repeat;}#rounded-corner tfoot td.rounded-foot-right{background:#e8edff url("/images/express-css-table-design/table-images/botright.png") right bottom no-repeat;}#rounded-corner tbody tr:hover td{background:#d0dafd;}#background-image{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;background:url("/images/express-css-table-design/table-images/blurry.jpg") 330px 59px no-repeat;margin:20px;}#background-image th{font-weight:normal;font-size:14px;color:#339;padding:12px;}#background-image td{color:#669;border-top:1px solid #fff;padding:9px 12px;}#background-image tfoot td{font-size:11px;}#background-image tbody td{background:url("/images/express-css-table-design/table-images/back.png");}* html #background-image tbody td{filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src='table-images/back.png',sizingMethod='crop');background:none;}#background-image tbody tr:hover td{color:#339;background:none;}#gradient-style{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#gradient-style th{font-size:13px;font-weight:normal;background:#b9c9fe url("/images/express-css-table-design/table-images/gradhead.png") repeat-x;border-top:2px solid #d3ddff;border-bottom:1px solid #fff;color:#039;padding:8px;}#gradient-style td{border-bottom:1px solid #fff;color:#669;border-top:1px solid #fff;background:#e8edff url("/images/express-css-table-design/table-images/gradback.png") repeat-x;padding:8px;}#gradient-style tfoot tr td{background:#e8edff;font-size:12px;color:#99c;}#gradient-style tbody tr:hover td{background:#d0dafd url("/images/express-css-table-design/table-images/gradhover.png") repeat-x;color:#339;}#pattern-style-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;background:url("/images/express-css-table-design/table-images/pattern.png");margin:20px;}#pattern-style-a thead tr{background:url("/images/express-css-table-design/table-images/pattern-head.png");}#pattern-style-a th{font-size:13px;font-weight:normal;border-bottom:1px solid #fff;color:#039;padding:8px;}#pattern-style-a td{border-bottom:1px solid #fff;color:#669;border-top:1px solid transparent;padding:8px;}#pattern-style-a tbody tr:hover td{color:#339;background:#fff;}#pattern-style-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;background:url("/images/express-css-table-design/table-images/patternb.png");margin:20px;}#pattern-style-b thead tr{background:url("/images/express-css-table-design/table-images/patternb-head.png");}#pattern-style-b th{font-size:13px;font-weight:normal;border-bottom:1px solid #fff;color:#039;padding:8px;}#pattern-style-b td{border-bottom:1px solid #fff;color:#669;border-top:1px solid transparent;padding:8px;}#pattern-style-b tbody tr:hover td{color:#339;background:#cdcdee;}.dp-highlighter{font-family:"Consolas", "Courier New", Courier, mono, serif;font-size:12px;background-color:#E7E5DC;width:99%;overflow:auto;padding-top:1px;margin:18px 0!important;}.dp-highlighter ol,.dp-highlighter ol li,.dp-highlighter ol li span{border:none;margin:0;padding:0;}.dp-highlighter a,.dp-highlighter a:hover{background:none;border:none;margin:0;padding:0;}.dp-highlighter .bar{padding-left:45px;}.dp-highlighter.collapsed .bar,.dp-highlighter.nogutter .bar{padding-left:0;}.dp-highlighter ol{list-style:decimal;background-color:#fff;color:#5C5C5C;margin:0 0 1px 45px !important;padding:0;}.dp-highlighter.nogutter ol,.dp-highlighter.nogutter ol li{list-style:none!important;margin-left:0!important;}.dp-highlighter ol li,.dp-highlighter .columns div{list-style:decimal-leading-zero;list-style-position:outside!important;border-left:3px solid #6CE26C;background-color:#F8F8F8;color:#5C5C5C;line-height:14px;margin:0!important;padding:0 3px 0 10px !important;}.dp-highlighter.nogutter ol li,.dp-highlighter.nogutter .columns div{border:0;}.dp-highlighter .columns{background-color:#F8F8F8;color:gray;overflow:hidden;width:100%;}.dp-highlighter .columns div{padding-bottom:5px;}.dp-highlighter ol li.alt{background-color:#FFF;color:inherit;}.dp-highlighter ol li span{color:black;background-color:inherit;}.dp-highlighter.collapsed ol{margin:0;}.dp-highlighter.collapsed ol li{display:none;}.dp-highlighter.printing{border:none;}.dp-highlighter.printing .tools{display:none!important;}.dp-highlighter.printing li{display:list-item!important;}.dp-highlighter .tools{font:9px Verdana, Geneva, Arial, Helvetica, sans-serif;color:silver;background-color:#f8f8f8;border-left:3px solid #6CE26C;padding:3px 8px 10px 10px;}.dp-highlighter.nogutter .tools{border-left:0;}.dp-highlighter.collapsed .tools{border-bottom:0;}.dp-highlighter .tools a{font-size:9px;color:#a0a0a0;background-color:inherit;text-decoration:none;margin-right:10px;}.dp-highlighter .tools a:hover{color:red;background-color:inherit;text-decoration:underline;}.dp-about{background-color:#fff;color:#333;margin:0;padding:0;}.dp-about table{width:100%;height:100%;font-size:11px;font-family:Tahoma, Verdana, Arial, sans-serif!important;}.dp-about td{vertical-align:top;padding:10px;}.dp-about .copy{border-bottom:1px solid #ACA899;height:95%;}.dp-about .title{color:red;background-color:inherit;font-weight:bold;}.dp-about .para{margin:0 0 4px;}.dp-about .footer{background-color:#ECEADB;color:#333;border-top:1px solid #fff;text-align:right;}.dp-about .close{font-size:11px;font-family:Tahoma, Verdana, Arial, sans-serif!important;background-color:#ECEADB;color:#333;width:60px;height:22px;}.dp-highlighter .comment,.dp-highlighter .comments{color:#008200;background-color:inherit;}.dp-highlighter .string{color:blue;background-color:inherit;}.dp-highlighter .keyword{color:#069;font-weight:bold;background-color:inherit;}.dp-highlighter .preprocessor{color:gray;background-color:inherit;}
</style>

## 9\. Table Background

If you are looking for a quick and unique way to style your table, simply pick an attractive image or photo related to the subject of your table and set it to be the `background-image` of the `table`. You can add 50% grey png-image as `background-image` of the cells to improve readability, and that means that you need a CSS-hack to make it work in IE 6:

<pre><code class="language-css">* html table tbody td
{

		  /* IE CSS Filter Hack goes here*/

}</code></pre>

The table would look like this:

<table id="background-image" summary="Meeting Results">
    <thead>
    	<tr>
        	<th scope="col">Employee</th>
            <th scope="col">Division</th>
            <th scope="col">Suggestions</th>
        </tr>
    </thead>
    <tfoot>
    	<tr>
        	<td colspan="4">IE 6 users won't see the transparent background if the hack is not applied</td>
        </tr>
    </tfoot>
    <tbody>
    	<tr>
        	<td>Stephen C. Cox</td>
            <td>Marketing</td>
            <td>Make discount offers</td>
        </tr>
        <tr>
        	<td>Josephin Tan</td>
            <td>Advertising</td>
            <td>Give bonuses</td>
        </tr>
        <tr>
        	<td>Joyce Ming</td>
            <td>Marketing</td>
            <td>New designs</td>
        </tr>
        <tr>
        	<td>James A. Pentel</td>
            <td>Marketing</td>
            <td>Better Packaging</td>
        </tr>
    </tbody>
</table>

*   **Important!**
Make sure the image is relevant to the table's contents
*   **Pros**
Very easy to style, delivers unique look, if used correctly the image can serve as a symbol that gives outstanding impression on the viewer
*   **Cons**
Needs hack to get the background work in IE 6, needs images
*   **Play With**
Background images, transparent PNGs, typography, colors, icons

## 10\. Cell Background

You can apply `background-image` to the cells and achieve a consistent look. Say you have at least half an hour to spare and you want something that's not too bland. Start your Photoshop and make 1 pixel width gradients, and set them as `background-image` of all cells. You'll end up with a gradient style table:

<table id="gradient-style" summary="Meeting Results">
    <thead>
    	<tr>
        	<th scope="col">Employee</th>
            <th scope="col">Division</th>
            <th scope="col">Suggestions</th>
            <th scope="col">Rating</th>
        </tr>
    </thead>
    <tfoot>
    	<tr>
        	<td colspan="4">Give background color to the table cells to achieve seamless transition</td>
        </tr>
    </tfoot>
    <tbody>
    	<tr>
        	<td>Stephen C. Cox</td>
            <td>Marketing</td>
            <td>Make discount offers</td>
            <td>3/10</td>
        </tr>
        <tr>
        	<td>Josephin Tan</td>
            <td>Advertising</td>
            <td>Give bonuses</td>
        	<td>5/10</td>
        </tr>
        <tr>
        	<td>Joyce Ming</td>
            <td>Marketing</td>
            <td>New designs</td>
        	<td>8/10</td>
        </tr>
        <tr>
        	<td>James A. Pentel</td>
            <td>Marketing</td>
            <td>Better Packaging</td>
            <td>8/10</td>
        </tr>
    </tbody>
</table>

Similarly, pick a pattern and set it as `background-image` and you'll end up with a pattern-styled-table:

<table id="pattern-style-a" summary="Meeting Results">
   <thead>
    	<tr>
        	<th scope="col">Employee</th>
            <th scope="col">Salary</th>
            <th scope="col">Bonus</th>
            <th scope="col">Supervisor</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<td>Stephen C. Cox</td>
            <td>$300</td>
            <td>$50</td>
            <td>Bob</td>
        </tr>
        <tr>
        	<td>Josephin Tan</td>
            <td>$150</td>
            <td>-</td>
            <td>Annie</td>
        </tr>
        <tr>
        	<td>Joyce Ming</td>
            <td>$200</td>
            <td>$35</td>
            <td>Andy</td>
        </tr>
        <tr>
        	<td>James A. Pentel</td>
            <td>$175</td>
            <td>$25</td>
            <td>Annie</td>
        </tr>
    </tbody>
</table>

<table id="pattern-style-b" summary="Meeting Results">
    <thead>
    	<tr>
        	<th scope="col">Nation</th>
            <th scope="col">Capital</th>
            <th scope="col">Language</th>
            <th scope="col">Unique</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<td>Japan</td>
            <td>Tokyo</td>
            <td>Japanese</td>
            <td>Karate</td>
        </tr>
        <tr>
        	<td>South Korea</td>
            <td>Seoul</td>
            <td>Korean</td>
            <td>Ginseng</td>
        </tr>
        <tr>
        	<td>China</td>
            <td>Beijing</td>
            <td>Mandarin</td>
            <td>Kung-Fu</td>
        </tr>
        <tr>
        	<td>Indonesia</td>
            <td>Jakarta</td>
            <td>Indonesian</td>
            <td>Batik</td>
        </tr>
    </tbody>
</table>

*   **Important!**
Make sure the text stands out against the background
*   **Pros**
Easy to style, not too bland
*   **Cons**
Uses images, patterns and gradients might distract reading
*   **Play With**
Color scheme, patterns, typography, borders, backgrounds, gradients, icons

## Final Words

I know I barely scratched the surface with this article, so feel free to look a the page source code and copy the &lt;styles&gt; and the table markup from the and play around. Feel free to post your favourite table designs, especially if it's something I missed out. Over to you.

<style>
#leftcolumn dl{display:block;margin-left:20px;}#leftcolumn dt{font-size:120%;color:#999;margin:10px 0 0;padding:0;}#leftcolumn dt.imp strong{font-weight:normal;color:red;}#leftcolumn dd{margin:0;padding:0;}#hor-minimalist-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;background:#fff;width:480px;border-collapse:collapse;text-align:left;margin:20px;}#hor-minimalist-a th{font-size:14px;font-weight:normal;color:#039;border-bottom:2px solid #6678b1;padding:10px 8px;}#hor-minimalist-a td{color:#669;padding:9px 8px 0;}#hor-minimalist-a tbody tr:hover td{color:#009;}#hor-minimalist-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;background:#fff;width:480px;border-collapse:collapse;text-align:left;margin:20px;}#hor-minimalist-b th{font-size:14px;font-weight:normal;color:#039;border-bottom:2px solid #6678b1;padding:10px 8px;}#hor-minimalist-b td{border-bottom:1px solid #ccc;color:#669;padding:6px 8px;}#hor-minimalist-b tbody tr:hover td{color:#009;}#ver-minimalist{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:30px 30px 30px 15px;}#ver-minimalist th{font-weight:normal;font-size:14px;border-bottom:2px solid #6678b1;border-right:30px solid #fff;border-left:30px solid #fff;color:#039;padding:8px 2px;}#ver-minimalist td{border-right:30px solid #fff;border-left:30px solid #fff;color:#669;padding:12px 2px 0;}#box-table-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#box-table-a th{font-size:13px;font-weight:normal;background:#b9c9fe;border-top:4px solid #aabcfe;border-bottom:1px solid #fff;color:#039;padding:8px;}#box-table-a td{background:#e8edff;border-bottom:1px solid #fff;color:#669;border-top:1px solid transparent;padding:8px;}#box-table-a tr:hover td{background:#d0dafd;color:#339;}#box-table-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:center;border-collapse:collapse;border-top:7px solid #9baff1;border-bottom:7px solid #9baff1;margin:20px;}#box-table-b th{font-size:13px;font-weight:normal;background:#e8edff;border-right:1px solid #9baff1;border-left:1px solid #9baff1;color:#039;padding:8px;}#box-table-b td{background:#e8edff;border-right:1px solid #aabcfe;border-left:1px solid #aabcfe;color:#669;padding:8px;}#hor-zebra{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#hor-zebra th{font-size:14px;font-weight:normal;color:#039;padding:10px 8px;}#hor-zebra td{color:#669;padding:8px;}#hor-zebra .odd{background:#e8edff;}#ver-zebra{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:0 20px 20px 20px;}#ver-zebra th{font-size:14px;font-weight:normal;border-right:1px solid #fff;border-left:1px solid #fff;color:#039;padding:12px 15px;}#ver-zebra td{border-right:1px solid #fff;border-left:1px solid #fff;color:#669;padding:8px 15px;}.vzebra-odd{background:#eff2ff;}.vzebra-even{background:#e8edff;}#ver-zebra #vzebra-adventure,#ver-zebra #vzebra-children{background:#d0dafd;border-bottom:1px solid #c8d4fd;}#ver-zebra #vzebra-comedy,#ver-zebra #vzebra-action{background:#dce4ff;border-bottom:1px solid #d6dfff;}#one-column-emphasis{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#one-column-emphasis th{font-size:14px;font-weight:normal;color:#039;padding:12px 15px;}#one-column-emphasis td{color:#669;border-top:1px solid #e8edff;padding:10px 15px;}.oce-first{background:#d0dafd;border-right:10px solid transparent;border-left:10px solid transparent;}#one-column-emphasis tr:hover td{color:#339;background:#eff2ff;}#newspaper-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;border:1px solid #69c;margin:20px;}#newspaper-a th{font-weight:normal;font-size:14px;color:#039;border-bottom:1px dashed #69c;padding:12px 17px;}#newspaper-a td{color:#669;padding:7px 17px;}#newspaper-a tbody tr:hover td{color:#339;background:#d0dafd;}#newspaper-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;border:1px solid #69c;margin:20px;}#newspaper-b th{font-weight:normal;font-size:14px;color:#039;padding:15px 10px 10px;}#newspaper-b tbody{background:#e8edff;}#newspaper-b td{color:#669;border-top:1px dashed #fff;padding:10px;}#newspaper-b tbody tr:hover td{color:#339;background:#d0dafd;}#newspaper-c{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;border:1px solid #6cf;margin:20px;}#newspaper-c th{font-weight:normal;font-size:13px;color:#039;text-transform:uppercase;border-right:1px solid #0865c2;border-top:1px solid #0865c2;border-left:1px solid #0865c2;border-bottom:1px solid #fff;padding:20px;}#newspaper-c td{color:#669;border-right:1px dashed #6cf;padding:10px 20px;}#rounded-corner{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#rounded-corner thead th.rounded-company{background:#b9c9fe url("/images/express-css-table-design/table-images/left.png") left -1px no-repeat;}#rounded-corner thead th.rounded-q4{background:#b9c9fe url("/images/express-css-table-design/table-images/right.png") right -1px no-repeat;}#rounded-corner th{font-weight:normal;font-size:13px;color:#039;background:#b9c9fe;padding:8px;}#rounded-corner td{background:#e8edff;border-top:1px solid #fff;color:#669;padding:8px;}#rounded-corner tfoot td.rounded-foot-left{background:#e8edff url("/images/express-css-table-design/table-images/botleft.png") left bottom no-repeat;}#rounded-corner tfoot td.rounded-foot-right{background:#e8edff url("/images/express-css-table-design/table-images/botright.png") right bottom no-repeat;}#rounded-corner tbody tr:hover td{background:#d0dafd;}#background-image{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;background:url("/images/express-css-table-design/table-images/blurry.jpg") 330px 59px no-repeat;margin:20px;}#background-image th{font-weight:normal;font-size:14px;color:#339;padding:12px;}#background-image td{color:#669;border-top:1px solid #fff;padding:9px 12px;}#background-image tfoot td{font-size:11px;}#background-image tbody td{background:url("/images/express-css-table-design/table-images/back.png");}* html #background-image tbody td{filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src='table-images/back.png',sizingMethod='crop');background:none;}#background-image tbody tr:hover td{color:#339;background:none;}#gradient-style{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;margin:20px;}#gradient-style th{font-size:13px;font-weight:normal;background:#b9c9fe url("/images/express-css-table-design/table-images/gradhead.png") repeat-x;border-top:2px solid #d3ddff;border-bottom:1px solid #fff;color:#039;padding:8px;}#gradient-style td{border-bottom:1px solid #fff;color:#669;border-top:1px solid #fff;background:#e8edff url("/images/express-css-table-design/table-images/gradback.png") repeat-x;padding:8px;}#gradient-style tfoot tr td{background:#e8edff;font-size:12px;color:#99c;}#gradient-style tbody tr:hover td{background:#d0dafd url("/images/express-css-table-design/table-images/gradhover.png") repeat-x;color:#339;}#pattern-style-a{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;background:url("/images/express-css-table-design/table-images/pattern.png");margin:20px;}#pattern-style-a thead tr{background:url("/images/express-css-table-design/table-images/pattern-head.png");}#pattern-style-a th{font-size:13px;font-weight:normal;border-bottom:1px solid #fff;color:#039;padding:8px;}#pattern-style-a td{border-bottom:1px solid #fff;color:#669;border-top:1px solid transparent;padding:8px;}#pattern-style-a tbody tr:hover td{color:#339;background:#fff;}#pattern-style-b{font-family:"Lucida Sans Unicode", "Lucida Grande", Sans-Serif;font-size:12px;width:480px;text-align:left;border-collapse:collapse;background:url("/images/express-css-table-design/table-images/patternb.png");margin:20px;}#pattern-style-b thead tr{background:url("/images/express-css-table-design/table-images/patternb-head.png");}#pattern-style-b th{font-size:13px;font-weight:normal;border-bottom:1px solid #fff;color:#039;padding:8px;}#pattern-style-b td{border-bottom:1px solid #fff;color:#669;border-top:1px solid transparent;padding:8px;}#pattern-style-b tbody tr:hover td{color:#339;background:#cdcdee;}.dp-highlighter{font-family:"Consolas", "Courier New", Courier, mono, serif;font-size:12px;background-color:#E7E5DC;width:99%;overflow:auto;padding-top:1px;margin:18px 0!important;}.dp-highlighter ol,.dp-highlighter ol li,.dp-highlighter ol li span{border:none;margin:0;padding:0;}.dp-highlighter a,.dp-highlighter a:hover{background:none;border:none;margin:0;padding:0;}.dp-highlighter .bar{padding-left:45px;}.dp-highlighter.collapsed .bar,.dp-highlighter.nogutter .bar{padding-left:0;}.dp-highlighter ol{list-style:decimal;background-color:#fff;color:#5C5C5C;margin:0 0 1px 45px !important;padding:0;}.dp-highlighter.nogutter ol,.dp-highlighter.nogutter ol li{list-style:none!important;margin-left:0!important;}.dp-highlighter ol li,.dp-highlighter .columns div{list-style:decimal-leading-zero;list-style-position:outside!important;border-left:3px solid #6CE26C;background-color:#F8F8F8;color:#5C5C5C;line-height:14px;margin:0!important;padding:0 3px 0 10px !important;}.dp-highlighter.nogutter ol li,.dp-highlighter.nogutter .columns div{border:0;}.dp-highlighter .columns{background-color:#F8F8F8;color:gray;overflow:hidden;width:100%;}.dp-highlighter .columns div{padding-bottom:5px;}.dp-highlighter ol li.alt{background-color:#FFF;color:inherit;}.dp-highlighter ol li span{color:black;background-color:inherit;}.dp-highlighter.collapsed ol{margin:0;}.dp-highlighter.collapsed ol li{display:none;}.dp-highlighter.printing{border:none;}.dp-highlighter.printing .tools{display:none!important;}.dp-highlighter.printing li{display:list-item!important;}.dp-highlighter .tools{font:9px Verdana, Geneva, Arial, Helvetica, sans-serif;color:silver;background-color:#f8f8f8;border-left:3px solid #6CE26C;padding:3px 8px 10px 10px;}.dp-highlighter.nogutter .tools{border-left:0;}.dp-highlighter.collapsed .tools{border-bottom:0;}.dp-highlighter .tools a{font-size:9px;color:#a0a0a0;background-color:inherit;text-decoration:none;margin-right:10px;}.dp-highlighter .tools a:hover{color:red;background-color:inherit;text-decoration:underline;}.dp-about{background-color:#fff;color:#333;margin:0;padding:0;}.dp-about table{width:100%;height:100%;font-size:11px;font-family:Tahoma, Verdana, Arial, sans-serif!important;}.dp-about td{vertical-align:top;padding:10px;}.dp-about .copy{border-bottom:1px solid #ACA899;height:95%;}.dp-about .title{color:red;background-color:inherit;font-weight:bold;}.dp-about .para{margin:0 0 4px;}.dp-about .footer{background-color:#ECEADB;color:#333;border-top:1px solid #fff;text-align:right;}.dp-about .close{font-size:11px;font-family:Tahoma, Verdana, Arial, sans-serif!important;background-color:#ECEADB;color:#333;width:60px;height:22px;}.dp-highlighter .comment,.dp-highlighter .comments{color:#008200;background-color:inherit;}.dp-highlighter .string{color:blue;background-color:inherit;}.dp-highlighter .keyword{color:#069;font-weight:bold;background-color:inherit;}.dp-highlighter .preprocessor{color:gray;background-color:inherit;}
</style>