---
title: 'A Guide To Command-Line Data Manipulation'
slug: guide-command-line-data-manipulation-cli-miller
author: alvin-bryan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9865d051-a600-4de7-a961-8b39a9226757/guide-command-line-data-manipulation-cli-miller.jpg
date: 2022-12-27T11:00:00.000Z
summary: >-
  No more random scripts in Python and JavaScript to transform CSV or JSON data. In this article, Alvin Bryan shows you how to use [Miller](https://miller.readthedocs.io/en/latest/), a small and powerful CLI tool, to do all your data processing.
description: >-
  No more random scripts in Python and JavaScript to transform CSV or JSON data. In this article, Alvin Bryan shows you how to use Miller, a small and powerful CLI tool, to do all your data processing.
categories:
  - Guides
  - Tools
  - Techniques
---

Allow me to preface this article by saying that I’m not a terminal person. I don’t use Vim. I find `sed`, `grep`, and `awk` convoluted and counter-intuitive. I prefer seeing my files in a nice UI. Despite all that, I got into the habit of reaching for **command-line interfaces (CLIs)** when I had small, dedicated tasks to complete. Why? I’ll explain all of that below. In this article, you’ll also learn how to use a CLI tool named [Miller](https://miller.readthedocs.io/en/latest/) to manipulate data from CSV, TSV and/or JSON files.

## Why Use The Command Line?

Everything that I’m showing here can be done with regular code. You can load the file, parse the CSV data, and then transform it using regular JavaScript, Python, or any other language. But there are a few reasons why I reach out for command-line interfaces (CLIs) whenever I need to transform data:

- **Easier to read.**  
It is faster (for me) to write a script in JavaScript or Python for my usual data processing. But, a script can be confusing to come back to. In my experience, **command-line manipulations are harder to write initially but easier to read afterward**.
- **Easier to reproduce.**  
Thanks to package managers like Homebrew, CLIs are much easier to install than they used to be. No need to figure out the correct version of Node.js or Python, the package manager takes care of that for you.
- **Ages well.**  
Compared to modern programming languages, CLIs are old. They change a lot more slowly than languages and frameworks.

## What Is Miller?

The main reason I love Miller is that it’s a standalone tool. There are many great tools for data manipulation, but every other tool I found was part of a specific ecosystem. The tools written in Python required knowing how to use `pip` and virtual environments; for those written in Rust, it was `cargo`, and so on.

On top of that, it’s fast. The data files are streamed, not held in memory, which means that you can **perform operations on large files without freezing your computer**.

As a bonus, Miller is actively maintained, [John Kerl](https://github.com/johnkerl/) really keeps on top of PRs and issues. As a developer, I always get a satisfying feeling when I see a neat and maintained open-source project with great documentation.

## Installation

- Linux: `apt-get install miller` or [Homebrew](https://docs.brew.sh/linux).
- macOS: `brew install miller` using Homebrew.
- Windows: `choco install miller` using [Chocolatey](https://chocolatey.org/).

That’s it, and you should now have the `mlr` command available in your terminal.

Run `mlr help topics` to see if it worked. This will give you instructions to navigate the built-in documentation. You shouldn’t need it, though; that’s what this tutorial is for!

{{% feature-panel %}} 

## How `mlr` Works

Miller commands work the following way:

<pre><code class="language-bash">mlr [input/output file formats] [verbs] [file]
</code></pre>

**Example**: `mlr --csv filter '$color != "red"' example.csv`

Let’s deconstruct:

- `--csv` specifies the input file format. It’s a CSV file.
- `filter` is what we’re doing on the file, called a “verb” in the documentation. In this case, we’re filtering every row that doesn’t have the field `color` set to `"red"`. There are many other verbs like `sort` and `cut` that we’ll explore later.
- `example.csv` is the file that we’re manipulating.

## Operations Overview

We can use those *verbs* to run specific operations on your data. There’s a lot we can do. Let’s explore.

### Data

I’ll be using a dataset of [*IMDb ratings for American TV dramas*](https://github.com/TheEconomist/graphic-detail-data/tree/master/data/2018-11-24_tv-ratings) created by The Economist. You can download it [here](https://raw.githubusercontent.com/smashingmagazine/command-line-data-manipulation/main/tv_ratings.csv) or find it in the [repo](https://github.com/smashingmagazine/command-line-data-manipulation) for this article.

**Note**: *For the sake of brevity, I’ve renamed the file from `mlr --csv head ./IMDb_Economist_tv_ratings.csv` to `tv_ratings.csv`.*

Above, I mentioned that every command contains a specific operation or verb. Let’s learn our first one, called `head`. What it does is show you the beginning of the file (the “head”) rather than print the entire file in the console.

You can run the following command:

<pre><code class="language-bash">`mlr --csv head ./tv&#95;ratings.csv`
</code></pre>

And this is the output you’ll see:

<div class="break-out">

<pre><code class="language-bash">titleId,seasonNumber,title,date,av_rating,share,genres
tt2879552,1,11.22.63,2016-03-10,8.489,0.51,"Drama,Mystery,Sci-Fi"
tt3148266,1,12 Monkeys,2015-02-27,8.3407,0.46,"Adventure,Drama,Mystery"
tt3148266,2,12 Monkeys,2016-05-30,8.8196,0.25,"Adventure,Drama,Mystery"
tt3148266,3,12 Monkeys,2017-05-19,9.0369,0.19,"Adventure,Drama,Mystery"
tt3148266,4,12 Monkeys,2018-06-26,9.1363,0.38,"Adventure,Drama,Mystery"
tt1837492,1,13 Reasons Why,2017-03-31,8.437,2.38,"Drama,Mystery"
tt1837492,2,13 Reasons Why,2018-05-18,7.5089,2.19,"Drama,Mystery"
tt0285331,1,24,2002-02-16,8.5641,6.67,"Action,Crime,Drama"
tt0285331,2,24,2003-02-09,8.7028,7.13,"Action,Crime,Drama"
tt0285331,3,24,2004-02-09,8.7173,5.88,"Action,Crime,Drama"
</code></pre>
</div>

This is a bit hard to read, so let’s make it easier on the eye by adding `--opprint`.

<pre><code class="language-bash">mlr --csv --opprint head ./tv&#95;ratings.csv
</code></pre>

The resulting output will be the following:

<div class="break-out">

<pre><code class="language-bash">titleId   seasonNumber title            date          av_rating   share   genres
tt2879552      1       11.22.63         2016-03-10    8.489       0.51    Drama,Mystery,Sci-Fi
tt3148266      1       12 Monkeys       2015-02-27    8.3407      0.46    Adventure,Drama,Mystery
tt3148266      2       12 Monkeys       2016-05-30    8.8196      0.25    Adventure,Drama,Mystery
tt3148266      3       12 Monkeys       2017-05-19    9.0369      0.19    Adventure,Drama,Mystery
tt3148266      4       12 Monkeys       2018-06-26    9.1363      0.38    Adventure,Drama,Mystery
tt1837492      1       13 Reasons Why   2017-03-31    8.437       2.38    Drama,Mystery
tt1837492      2       13 Reasons Why   2018-05-18    7.5089      2.19    Drama,Mystery
tt0285331      1       24               2002-02-16    8.5641      6.67    Action,Crime,Drama
tt0285331      2       24               2003-02-09    8.7028      7.13    Action,Crime,Drama
tt0285331      3       24               2004-02-09    8.7173      5.88    Action,Crime,Drama
</code></pre>
</div>

Much better, isn’t it?

**Note**: *Rather than typing `--csv --opprint` every time, we can use the `--c2p` option, which is a shortcut.*

### Chaining

That’s where the fun begins. Rather than run multiple commands, we can chain the verbs together by using the `then` keyword.

### Remove columns

You can see that there’s a `titleId` column that isn’t very useful. Let’s get rid of it using the `cut` verb.

<pre><code class="language-bash">mlr --c2p cut -x -f titleId then head ./tv&#95;ratings.csv
</code></pre>

It gives you the following output:

<div class="break-out">

<pre><code class="language-bash">seasonNumber  title            date         av_rating   share    genres
     1      11.22.63          2016-03-10    8.489       0.51     Drama,Mystery,Sci-Fi
     1      12 Monkeys        2015-02-27    8.3407      0.46     Adventure,Drama,Mystery
     2      12 Monkeys        2016-05-30    8.8196      0.25     Adventure,Drama,Mystery
     3      12 Monkeys        2017-05-19    9.0369      0.19     Adventure,Drama,Mystery
     4      12 Monkeys        2018-06-26    9.1363      0.38     Adventure,Drama,Mystery
     1      13 Reasons Why    2017-03-31    8.437       2.38     Drama,Mystery
     2      13 Reasons Why    2018-05-18    7.5089      2.19     Drama,Mystery
     1      24                2002-02-16    8.5641      6.67     Action,Crime,Drama
     2      24                2003-02-09    8.7028      7.13     Action,Crime,Drama
     3      24                2004-02-09    8.7173      5.88     Action,Crime,Drama
</code></pre>
</div>

<blockquote><strong>Fun Fact</strong><br /><br />This is how I first learned about Miller! I was playing with a CSV dataset for <a href="https://details.town/">https://details.town/</a> that had a useless column, and I looked up “how to remove a column from CSV command line.” I discovered Miller, loved it, and then pitched an article to Smashing magazine. Now here we are!</blockquote>

### Filter

This is the verb that I first showed earlier. We can remove all the rows that don’t match a specific expression, letting us clean our data with only a few characters.

If we only want the rating of the first seasons of every series in the dataset, this is how you do it:

<pre><code class="language-bash">mlr --c2p filter '$seasonNumber == 1' then head ./tv&#95;ratings.csv
</code></pre>

### Sorting

We can sort our data based on a specific column like it would be in a UI like Excel or macOS Numbers. Here’s how you would sort your data based on the series with the highest rating:

<pre><code class="language-bash">mlr --c2p sort -nr av&#95;rating then head ./tv&#95;ratings.csv
</code></pre>

The resulting output will be the following:

<pre class="break-out"><code class="language-bash">titleId   seasonNumber title                         date         av_rating  share   genres
tt0098887      1       Parenthood                    1990-11-13   9.6824     1.68    Comedy,Drama
tt0106028      6       Homicide: Life on the Street  1997-12-05   9.6        0.13    Crime,Drama,Mystery
tt0108968      5       Touched by an Angel           1998-11-15   9.6        0.08    Drama,Family,Fantasy
tt0903747      5       Breaking Bad                  2013-02-20   9.554      18.95   Crime,Drama,Thriller
tt0944947      6       Game of Thrones               2016-05-25   9.4943     15.18   Action,Adventure,Drama
tt3398228      5       BoJack Horseman               2018-09-14   9.4738     0.45    Animation,Comedy,Drama
tt0103352      3       Are You Afraid of the Dark?   1994-02-23   9.4349     2.6     Drama,Family,Fantasy
tt0944947      4       Game of Thrones               2014-05-09   9.4282     11.07   Action,Adventure,Drama
tt0976014      4       Greek                         2011-03-07   9.4        0.01    Comedy,Drama
tt0090466      4       L.A. Law                      1990-04-05   9.4        0.1     Drama
</code></pre>

We can see that *Parenthood*, from 1990, has the highest rating on IMDb &mdash; who knew!

### Saving Our Operations

By default, Miller only prints your processed data to the console. If we want to save it to another CSV file, we can use the `>` operator.

If we wanted to save our sorted data to a new CSV file, this is what the command would look like:

<pre><code class="language-bash">mlr --csv sort -nr av&#95;rating ./tv&#95;ratings.csv &gt; sorted.csv
</code></pre>

### Convert CSV To JSON

Most of the time, you don’t use CSV data directly in your application. You convert it to a format that is easier to read or doesn’t require additional dependencies, like JSON.

Miller gives you the `--c2j` option to convert your data from CSV to JSON. Here’s how to do this for our sorted data:

<pre><code class="language-bash">mlr --c2j sort -nr av_rating ./tv_ratings.csv > sorted.json
</code></pre>

{{% ad-panel-leaderboard %}}

## Case study: Top 5 Athletes With Highest Number Of Medals In Rio 2016

Let’s apply everything we learned above to a real-world use case. Let’s say that you have a detailed dataset of every athlete who participated in the 2016 Olympic games in Rio, and you want to know who the 5 with the highest number of medals are.

First, [download the athlete data as a CSV](https://raw.githubusercontent.com/flother/rio2016/master/athletes.csv), then save it in a file named `athletes.csv`.

Let’s open up the following file:

<pre><code class="language-bash">mlr --c2p head ./athletes.csv
</code></pre>

The resulting output will be something like the following:

<div class="break-out">

<pre><code class="language-bash">id        name                nationality sex    date_of_birth height weight sport      gold silver bronze info
736041664 A Jesus Garcia      ESP         male   1969-10-17    1.72    64     athletics    0    0      0      -
532037425 A Lam Shin          KOR         female 1986-09-23    1.68    56     fencing      0    0      0      -
435962603 Aaron Brown         CAN         male   1992-05-27    1.98    79     athletics    0    0      1      -
521041435 Aaron Cook          MDA         male   1991-01-02    1.83    80     taekwondo    0    0      0      -
33922579  Aaron Gate          NZL         male   1990-11-26    1.81    71     cycling      0    0      0      -
173071782 Aaron Royle         AUS         male   1990-01-26    1.80    67     triathlon    0    0      0      -
266237702 Aaron Russell       USA         male   1993-06-04    2.05    98     volleyball   0    0      1      -
382571888 Aaron Younger       AUS         male   1991-09-25    1.93    100    aquatics     0    0      0      -
87689776  Aauri Lorena Bokesa ESP         female 1988-12-14    1.80    62     athletics    0    0      0      -
</code></pre>
</div>

### Optional: Clean Up The File

The CSV file has a few fields we don’t need. Let’s clean it up by removing the `info` , `id` , `weight`, and `date_of_birth` columns.

<pre><code class="language-bash">mlr --csv -I cut -x -f id,info,weight,date&#95;of&#95;birth athletes.csv
</code></pre>

Now we can move to our original problem: we want to find who won the highest number of medals. We have how many of *each medal* (bronze, silver, and gold) the athletes won, but not the total number of medals per athlete.

Let’s compute a new value called `medals` which corresponds to this total number (bronze, silver, and gold added together).

<pre><code class="language-bash">mlr --c2p put '$medals=$bronze+$silver+$gold' then head ./athletes.csv
</code></pre>

It gives you the following output:

<div class="break-out">

<pre><code class="language-bash">name                 nationality   sex      height  sport        gold silver bronze medals
A Jesus Garcia       ESP           male     1.72    athletics      0    0      0      0
A Lam Shin           KOR           female   1.68    fencing        0    0      0      0
Aaron Brown          CAN           male     1.98    athletics      0    0      1      1
Aaron Cook           MDA           male     1.83    taekwondo      0    0      0      0
Aaron Gate           NZL           male     1.81    cycling        0    0      0      0
Aaron Royle          AUS           male     1.80    triathlon      0    0      0      0
Aaron Russell        USA           male     2.05    volleyball     0    0      1      1
Aaron Younger        AUS           male     1.93    aquatics       0    0      0      0
Aauri Lorena Bokesa  ESP           female   1.80    athletics      0    0      0      0
Ababel Yeshaneh      ETH           female   1.65    athletics      0    0      0      0
</code></pre>
</div>

Sort by the highest number of medals by adding a `sort`.

<pre><code class="language-bash">mlr --c2p put '$medals=$bronze+$silver+$gold' \
	then sort -nr medals \
	then head ./athletes.csv
</code></pre>

Respectively, the resulting output will be the following:

<div class="break-out">

<pre><code class="language-bash">name              nationality  sex     height  sport       gold silver bronze medals
Michael Phelps    USA          male    1.94    aquatics      5    1      0      6
Katie Ledecky     USA          female  1.83    aquatics      4    1      0      5
Simone Biles      USA          female  1.45    gymnastics    4    0      1      5
Emma McKeon       AUS          female  1.80    aquatics      1    2      1      4
Katinka Hosszu    HUN          female  1.75    aquatics      3    1      0      4
Madeline Dirado   USA          female  1.76    aquatics      2    1      1      4
Nathan Adrian     USA          male    1.99    aquatics      2    0      2      4
Penny Oleksiak    CAN          female  1.86    aquatics      1    1      2      4
Simone Manuel     USA          female  1.78    aquatics      2    2      0      4
Alexandra Raisman USA          female  1.58    gymnastics    1    2      0      3
</code></pre>
</div>

Restrict to the top 5 by adding `-n 5` to your `head` operation.

<pre><code class="language-bash">mlr --c2p put '$medals=$bronze+$silver+$gold' \
	then sort -nr medals \
	then head -n 5 ./athletes.csv
</code></pre>

You will end up with the following file:

<div class="break-out">

<pre><code class="language-bash">name             nationality  sex      height  sport        gold silver bronze medals
Michael Phelps   USA          male     1.94    aquatics       5     1      0      6
Katie Ledecky    USA          female   1.83    aquatics       4     1      0      5
Simone Biles     USA          female   1.45    gymnastics     4     0      1      5
Emma McKeon      AUS          female   1.80    aquatics       1     2      1      4
Katinka Hosszu   HUN          female   1.75    aquatics       3     1      0      4
</code></pre>
</div>

As a final step, let’s convert this into a JSON file with the `--c2j` option. 

Here is our final command:

<pre><code class="language-bash">mlr --c2j put '$medals=$bronze+$silver+$gold' \
	then sort -nr medals \
	then head -n 5 ./athletes.csv &gt; top5.json
</code></pre>

With a single command, we've computed new data, sorted the result, truncated it, and converted it to JSON.

<pre><code class="language-javascript">[
  {
    "name": "Michael Phelps",
    "nationality": "USA",
    "sex": "male",
    "height": 1.94,
    "weight": 90,
    "sport": "aquatics",
    "gold": 5,
    "silver": 1,
    "bronze": 0,
    "medals": 6
  }
  // Other entries omitted for brevity.
]
</code></pre>

**Bonus:** If you wanted to show the top 5 women, you could add a `filter`.

<div class="break-out">

<pre><code class="language-bash">mlr --c2p put '$medals=$bronze+$silver+$gold' then sort -nr medals then filter '$sex == "female"' then head -n 5 ./athletes.csv
</code></pre>
</div>

Respectively, you would end up with the following output:

<div class="break-out">

<pre><code class="language-bash">name              nationality   sex       height   sport        gold silver bronze medals
Katie Ledecky     USA           female    1.83     aquatics       4    1      0      5
Simone Biles      USA           female    1.45     gymnastics     4    0      1      5
Emma McKeon       AUS           female    1.80     aquatics       1    2      1      4
Katinka Hosszu    HUN           female    1.75     aquatics       3    1      0      4
Madeline Dirado   USA           female    1.76     aquatics       2    1      1      4
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## Conclusion

I hope this article showed you how versatile [Miller](https://miller.readthedocs.io/en/latest/) is and gave you a taste of the power of command-line tools. Feel free to scourge the internet for the best CLI next time you find yourself writing yet another random script.

### Resources

- [Miller](https://miller.readthedocs.io/en/latest/)
- Dataset of [IMDb ratings for American TV dramas](https://raw.githubusercontent.com/TheEconomist/graphic-detail-data/master/data/2018-11-24_tv-ratings/IMDb_Economist_tv_ratings.csv)

### Further Reading on Smashing Magazine

- [Powerful Terminal And Command-Line (CLI) Tools For Modern Web Development](https://www.smashingmagazine.com/2021/11/powerful-terminal-commandline-tools-modern-web-development/)
- [How Should Designers Learn To Code? The Terminal And Text Editors (Part 1)](https://www.smashingmagazine.com/2020/03/designers-code-terminal-text-editors-part-1/)
- [How To Develop An Interactive Command Line Application Using Node.js](https://www.smashingmagazine.com/2017/03/interactive-command-line-application-node-js/)
- [A Deep Dive Into Serverless UI With TypeScript](https://www.smashingmagazine.com/2021/11/deep-dive-into-serverless-ui-typescript/)

{{< signature "yk, il" >}}
