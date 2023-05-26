---
title: 'Quantitative Data Tools For UX Designers'
slug: quantitative-data-tools-uxdesigners
author: adonis-raul-raduca
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44c71f33-a2e3-4224-b573-f6dcc51e775f/quantitative-data-tools-uxdesigners.png
date: 2019-12-19T11:30:00.000Z
summary: >-
  Data analysis, tools and workflow are very helpful to UX designers in a data-driven world, especially for those working on visualizations or data products.
description: >-
  Data analysis, tools and workflow are very helpful for UX designers in a data-driven world, especially for those working on visualizations or data products.
categories:
  - Design
  - UX
  - Data Visualization
---
Many UX designers are somewhat afraid of data, believing it requires deep knowledge of statistics and math. Although that may be true for advanced data science, it is not true for the basic research data analysis required by most UX designers. Since we live in an increasingly data-driven world, basic data literacy is useful for almost <em>any</em> professional &mdash; not just UX designers.

Aaron Gitlin, interaction designer at Google, argues that many designers are not yet data-driven:

<blockquote>“While many businesses promote themselves as being data-driven, most designers are driven by instinct, collaboration, and qualitative research methods.” <br /><br />&mdash; Aaron Gitlin, “<a href="https://uxdesign.cc/becoming-a-data-aware-designer-1d7614ebc3ed">Becoming A Data-Aware Designer</a>”</blockquote>

With this article, I’d like to give UX designers the knowledge and tools to incorporate data into their daily routines.

## But First, Some Data Concepts

In this article I will talk about structured data, meaning data that can be represented in a table, with rows and columns. Unstructured data, being a subject in itself, is more difficult to analyze, as Devin Pickell (content marketing specialist at G2 Crowd, writing about data and analytics) pointed out in his article “[Structured vs Unstructured Data – What's the Difference?](https://learn.g2.com/structured-vs-unstructured-data).” If the structured data can be represented in a table form, the main concepts are:

### Dataset

The entire set of data we intend to analyze. This could be, for example, an Excel table. Another popular format for storing datasets is the comma-separated value file (CSV). CSV files are simple text files used to store table-like information. Each CSV row corresponds to a row in the table, and each CSV row has values separated (naturally) by commas, which correspond to table cells.

### Data Point

A single row from a dataset table is a data point. In that way, a dataset is a collection of data points.

### Data Variable

A single value from a data-point row represents a data variable &mdash; put simply, a table cell. We can have two types of data variables: qualitative variables, and quantitative variables. Qualitative variables (also known as categorical variables) have a discrete set of values, such as `color = red/green/blue`. Quantitative variables have numerical values, such as `height = 167`. A quantitative variable, unlike a qualitative one, can take any value.

{{% feature-panel %}}

## Creating Our Data Project

Now we know the basics, it’s time to get our hands dirty and create our first data project. The scope of the project is to analyze a dataset by going through the entire data flow of importing, processing and plotting data. First, we will choose our dataset, then we will download and install the tools for analyzing the data.

### Cars Dataset

For the purpose of this article, I’ve chosen a cars dataset, because it’s simple and intuitive. The data analysis will simply confirm what we already know about the cars &mdash; which is fine, since our focus is on data flow and tools.

We can download a used cars dataset from <a href="https://www.kaggle.com/">Kaggle</a>, one of the biggest sources of free datasets. You’ll need to register first.

After downloading the file, open it and take a look. It’s a really big CSV file, but you should get the gist. A line in this file will look like this:

<pre><code class="language-javascript">19500,2015,2965,Miami,FL,WBA3B1G54FNT02351,BMW,3
</code></pre>

As you can see, this data point has several variables separated by commas. Since we now have the dataset, let’s talk a little about tools.

### Tools of the Trade

We will use the R language and RStudio to analyze the dataset. R is a very popular and easy to learn language, used not only by data scientists, but also people in financial markets, medicine and many other areas. RStudio is the environment where R projects are developed, and there’s a free version, which is more than enough for our needs as UX designers.

It’s likely that some UX designers use Excel for their data workflow. If that means you, try R &mdash; there is a good chance you’ll like it, since it is easy to learn, and more flexible and powerful than Excel. Adding R to your tool kit will make a difference.

### Installing the Tools

First, we need to download and install [R](https://www.r-project.org/) and [RStudio](https://rstudio.com/products/rstudio/download/). You should install R first, then RStudio. The installation processes for both R and RStudio are simple and straightforward.

### Project Setup

Once the installation is complete, create a project folder &mdash; I’ve called it <i>used-cars-prj</i>. In that folder, create a subfolder called <i>data</i>, and then copy the dataset file (downloaded from [Kaggle](https://www.kaggle.com/jpayne/852k-used-car-listings/download)) into that folder and rename it to <i>used-cars.csv</i>. Now go back to our project folder (<i>used-cars-prj</i>) and create a plain text file called <i>used-cars.r</i>. You should end up with the same structure as in the screenshot below.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c49107ce-9c63-4d54-873a-6da80ec5080f/01-project-folders-structure.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c49107ce-9c63-4d54-873a-6da80ec5080f/01-project-folders-structure.png" sizes="100vw" caption="Project folder structure (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c49107ce-9c63-4d54-873a-6da80ec5080f/01-project-folders-structure.png'>Large preview</a>)" alt="project folder structure" >}}

Now we have the folder structure in place, we can open RStudio and create a new R project. Chose <b>New Project…</b> from the <b>File</b> menu and select the second option, <b>Existing Directory</b>. Then select the project directory (<i>used-cars-prj</i>). Finally, press the <b>Create Project</b> button and you’re done. Once the project is created, open <i>used-cars.r</i> in RStudio &mdash; this is the file where we will add all our R code.

{{% ad-panel-leaderboard %}}

## Importing Data

We will add our first line in <i>used-cars.r</i>, for reading data from the <i>used-cars.csv</i> file. Remember that CSV files are just plain text files used for storing data. Our first line of R code will look like this:

<div class="break-out">

 <pre><code class="language-javascript">cars <- read.csv("./data/used-cars.csv", stringsAsFactors = FALSE, sep=",")
</code></pre>
</div>

It might look a little intimidating, but it really isn’t &mdash; by the way, this is the most complex line in the entire article. What we have here is the `read.csv` function, which takes three parameters.

The first parameter is the file to read, in our case <i>used-cars.csv</i>, which is located in the <i>data</i> folder. The second parameter, `stringsAsFactors=FALSE` is set to make sure strings like “BMW” or “Audi” aren’t converted to factors (the R jargon for categorical data) &mdash; as you recall, qualitative or categorical variables can have only discrete values like `red/green/blue`. Finally, the third parameter, `sep=","` specifies the kind of separator used to separate values in the CSV file: a comma.

After reading the CSV file, the data is stored into the `cars` data frame object. A <strong>data frame</strong> is a two-dimensional data structure (like an Excel table), which is very useful in R to manipulate data. After introducing the line and running it, a `cars` data frame will be created for you. If you look in the top-right quadrant in RStudio, you will notice the `cars` data frame, in the <b>Data</b> section under the <b>Environment</b> tab. If you double click on <b>cars</b>, a new tab will open in the top-left quadrant of RStudio, and will present the `cars` data frame. As you might expect, it looks like an Excel table.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aba42d76-70ac-4bd2-b055-4d0d4e3a24ad/02-cars-raw-df.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aba42d76-70ac-4bd2-b055-4d0d4e3a24ad/02-cars-raw-df.png" sizes="100vw" caption="Cars raw data frame (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aba42d76-70ac-4bd2-b055-4d0d4e3a24ad/02-cars-raw-df.png'>Large preview</a>)" alt="cars raw data frame" >}}

This is actually the raw data we downloaded from Kaggle. But since we want to perform data analysis, we need to process our dataset first.

## Data Processing

By processing, we mean removing, transforming or adding information to our dataset, in order to prepare for the kind of analysis we want to perform. We have the data in a data frame object, so now we need to install the `dplyr` library, a powerful library for manipulating data. To install the library in our R environment, we need to write the following line at the top of our R file.

<pre><code class="language-javascript">install.packages("dplyr")
</code></pre>

Then, to add the library to our current project, we will use the next line:

<pre><code class="language-javascript">library(dplyr)
</code></pre>

Once the `dplyr` library has been added to our project, we can start processing data. We have a really big dataset, and we need only the data representing the same car maker and model, in order to correlate that with price. We’ll use the following R code to keep only data concerning the BMW 3 Series, and remove the rest. Of course, you could choose any other manufacturer and model from the dataset, and expect to have the same data characteristics.

<pre><code class="language-javascript">cars <- cars %>% filter(Make == "BMW", Model == "3")
</code></pre>

Now we have a more manageable dataset, though still containing more than 11,000 data points, that fits with our intended purpose: to analyze the cars’ price, age and mileage distributions, and also the correlations between them. For that, we need to keep only “Price”, “Year” and “Mileage” columns and remove the rest &mdash; this is done with the following line.

<pre><code class="language-javascript">cars <- cars %>% select(Price, Year, Mileage)
</code></pre>

After removing other columns, our data frame will look like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3add7bff-45fe-4fa3-be45-2f6ec52a1ff1/03-cars-semi-processed-df.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3add7bff-45fe-4fa3-be45-2f6ec52a1ff1/03-cars-semi-processed-df.png" sizes="100vw" caption="Cars semi-processed dataframe (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3add7bff-45fe-4fa3-be45-2f6ec52a1ff1/03-cars-semi-processed-df.png'>Large preview</a>)" alt="Cars semi-processed dataframe" >}}

There is one more change we want to make to our dataset: to replace the manufacture year with the age of the car. We can add the following two lines, the first to calculate the age, the second to change the column name.

<pre><code class="language-javascript">cars <- cars %>% mutate(Year = max(Year) - Year)
cars <- cars %>% rename(Age = Year)
</code></pre>

Finally, our full processed data frame looks like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e4fe614-4a9f-4159-b153-91e586ea73a4/04-cars-processed-df.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e4fe614-4a9f-4159-b153-91e586ea73a4/04-cars-processed-df.png" sizes="100vw" caption="Cars fully processed dataframe (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e4fe614-4a9f-4159-b153-91e586ea73a4/04-cars-processed-df.png'>Large preview</a>)" alt="Cars fully processed dataframe" >}}

At this point, our R code will look like the following, and that’s all for the data processing. We can now see how easy and powerful the R language is. We’ve processed the initial dataset quite dramatically with only a few lines of code.

<pre><code class="language-javascript">install.packages("dplyr")
library(dplyr)
cars = read.csv("./data/cars.csv", stringsAsFactors = FALSE, sep=",")
cars <- cars %>% filter(Make == "BMW", Model == "3")
cars <- cars %>% select(Price, Year, Mileage)
cars <- cars %>% mutate(Year = max(Year) - Year)
cars <- cars %>% rename(Age = Year)
</code></pre>

{{% ad-panel-leaderboard %}}

## Data Analysis

Our data is now in the right shape, so we can go to make some plots. As already mentioned, we will focus on two aspects: individual variables’ distribution, and the correlations between them. Variable distribution helps us to understand what is considered a medium or high price for a used car &mdash; or the percentage of cars above a specific price. The same applies for the age and mileage of the cars. Correlations, on the other hand, are helpful in understanding how variables like age and mileage are related to each other.

That said, we will use two kinds of data visualization: histograms for variable distribution, and scatter plots for correlations.

### Price Distribution

Plotting the car price histogram in the R language is as easy as this:

<pre><code class="language-javascript">hist(cars$Price)
</code></pre>

A small tip: if you are in RStudio you can run the code line by line; for example, in our case, you need run only the line above to display the histogram. It’s not necessary to run all the code again since you ran it once already. The histogram should look like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60af0150-9104-48d6-a454-b659850f8f67/05-cars-price-distribution.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60af0150-9104-48d6-a454-b659850f8f67/05-cars-price-distribution.png" sizes="100vw" caption="Car price distribution histogram (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60af0150-9104-48d6-a454-b659850f8f67/05-cars-price-distribution.png'>Large preview</a>)" alt="Car price distribution histogram" >}}

If we look at the histogram, we notice a bell-like distribution of the cars’ prices, which is what we expected. Most of the cars fall in the middle range, and we have fewer and fewer as we move to each side. Almost 80% of the cars are between $10,000 and $30,000 USD, and we have a maximum of more than 2,500 cars between $20,000 and $25,000 USD. On the left side we have probably around 150 cars under $5,000 USD, and on the right side even fewer. We can easily see how useful such plots are to get insights into data.

### Age Distribution

Just as for the cars’ prices, we’ll use a similar line to plot the cars’ age histogram.

<pre><code class="language-javascript">hist(cars$Age)
</code></pre>

And here is the histogram:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c4bac79-8bee-4e9c-8428-45d88a6c595f/06-cars-age-distribution.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c4bac79-8bee-4e9c-8428-45d88a6c595f/06-cars-age-distribution.png" sizes="100vw" caption="Car age distribution histogram (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c4bac79-8bee-4e9c-8428-45d88a6c595f/06-cars-age-distribution.png'>Large preview</a>)" alt="Car age distribution histogram" >}}

This time the histogram looks counterintuitive &mdash; instead of a simple bell shape, we have here four bells. Basically, the distribution has three local and one global maximum, which is unexpected. It would be interesting to see if this strange distribution of the cars’ ages stays true for another car maker and model. For the purpose of this article we’ll stay with the BMW 3 Series dataset, but you can dig deeper into the data if you are curious. Regarding our car age distribution, we notice that more than 90% of the cars are less than 10 years old, and more than 80% less than 7 years old. Also, we notice that the majority of the cars are less than 5 years old.

### Mileage Distribution

Now, what can we say about mileage? Of course, we expect to have the same bell shape we had for price. Here is the R code and the histogram:

<pre><code class="language-javascript">hist(cars$Mileage)
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3321dfda-ad3e-48da-9a56-6529acdf5085/07-cars-mileage-distribution.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3321dfda-ad3e-48da-9a56-6529acdf5085/07-cars-mileage-distribution.png" sizes="100vw" caption="Cars mileage distribution histogram (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3321dfda-ad3e-48da-9a56-6529acdf5085/07-cars-mileage-distribution.png'>Large preview</a>)" alt="Cars mileage distribution histogram" >}}

Here we have a left-skewed bell shape, meaning that there are more cars with less mileage on the market. We also notice that the majority of the cars have less than 60,000 miles, and we have a maximum around 20,000 to 40,000 miles.

### Age–Price Correlation

Regarding correlations, let’s take a closer look at the cars age–price correlation. We might expect the price to be negatively correlated with the age &mdash; as a car’s age increases, its price will go down. We will use the R `plot` function to display the price–age correlation as follows:

<pre><code class="language-javascript">plot(cars$Age, cars$Price)
</code></pre>

And the plot looks like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8eb546f-3478-491d-9ccd-b96fa0171fdf/08-cars-age-price-correlation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8eb546f-3478-491d-9ccd-b96fa0171fdf/08-cars-age-price-correlation.png" sizes="100vw" caption="Car age–price correlation scatterplot (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8eb546f-3478-491d-9ccd-b96fa0171fdf/08-cars-age-price-correlation.png'>Large preview</a>)" alt="Car age–price correlation scatterplot" >}}

We notice how the cars’ prices go down with age: there are expensive new cars, and cheaper old cars. We can also see the price variation interval for any specific age, a variation that decreases with a car’s age. This variation is largely driven by the mileage, configuration and overall state of the car. For example, in the case of a 4-year-old car, the price varies between $10,000 and $40,000 USD.

### Mileage–Age Correlation

Considering the mileage–age correlation, we would expect mileage to increase with age, meaning a positive correlation. Here is the code:

<pre><code class="language-javascript">plot(cars$Mileage, cars$Age)
</code></pre>

And here is the plot:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/316126db-8c71-4f4a-a00a-68c00c225b89/09-cars-mileage-age-correlation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/316126db-8c71-4f4a-a00a-68c00c225b89/09-cars-mileage-age-correlation.png" sizes="100vw" caption="Car mileage–age correlation scatterplot (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/316126db-8c71-4f4a-a00a-68c00c225b89/09-cars-mileage-age-correlation.png'>Large preview</a>)" alt="Car mileage–age correlation scatterplot" >}}

As you can see, a car’s age and mileage are positively correlated, unlike a car’s price and age, which are negatively correlated. We also have an expected mileage variation for a specific age; that is, cars of the same age have varying mileages. For example, most 4-year-old cars have the mileage between 10,000 and 80,000 miles. But there are outliers too, with greater mileage.

### Mileage–Price Correlation

As expected, there will be a negative correlation between the cars’ mileage and the price, which means that increasing the mileage reduces the price.

<pre><code class="language-javascript">plot(cars$Mileage, cars$Price)
</code></pre>

And here is the plot:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/622bd639-b75d-4244-8ba9-f42f6db5a2e8/10-cars-mileage-price-correlation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/622bd639-b75d-4244-8ba9-f42f6db5a2e8/10-cars-mileage-price-correlation.png" sizes="100vw" caption="Car mileage–price correlation scatterplot (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/622bd639-b75d-4244-8ba9-f42f6db5a2e8/10-cars-mileage-price-correlation.png'>Large preview</a>)" alt="Car mileage–price correlation scatterplot" >}}

As we expected, a negative correlation. We can also notice the gross price interval between $3,000 and $50,000 USD, and the mileage between 0 and 150,000. If we look closer at the distribution shape, we see that the price goes down much faster for cars with less mileage than it does for cars with more mileage. There are cars with almost zero mileage, where the price drops dramatically. Also, above 200,000 miles range &mdash; because the mileage is very high &mdash; the price stays constant.

### From Numbers To Data Visualizations

In this article, we used two types of visualization: histograms for data distributions, and scatter plots for data correlations. Histograms are visual representations that take the values of a data variable (actual *numbers*) and show how they are distributed across a range. We used the R `hist()` function to plot a histogram.

Scatter plots, on the other hand, take pairs of numbers and represent them on two axes. Scatter plots use the `plot()` function and provide two parameters: the first and the second data variables of the correlation we want to investigate. Thus, the two R functions, `hist()` and `plot()` help us translate sets of numbers in meaningful visual representations.

## Conclusion

Having got our hands dirty going through the entire data flow of importing, processing, and plotting data, things look much clearer now. You can apply the same data flow to any shiny new dataset that you will encounter. In user research, for example, you could graph time on task or error distributions, and you could also plot a time on task vs. error correlation.

To learn more about the R language [Quick-R](https://www.statmethods.net) is a good place to start, but you could also consider [R Bloggers](https://www.r-bloggers.com). For documentation on R packages, like `dplyr`, you can visit [RDocumentation](https://www.rdocumentation.org). Playing with data can be fun, but it is also extremely helpful to any UX designer in a data-driven world. As more data is collected and used to inform business decisions, there is an increased chance for designers to work on data visualization or data products, where understanding the nature of data is essential.

{{< signature "ah, il, og" >}}
