# Project 2

### 1. Group and Student member

+ Yi Zhang  yzh18@lzu.edu.cn 320180940611
+ Xiangwen Qiao qiaoxw18@lzu.edu.cn 320180940161
+ Zunye Tang  tangzy18@lzu.edu.cn 320180940261
+ Weijia Yang wjyang2018@lzu.edu.cn 320180940261

### 2. Abstract

In this report, we replicate a graph that has been shared in a public website. The original visualization are represented by a line chart and a pie chart. After replicating we make some adjustments about the graph according to the principles taught in the class to make the visualizations more effective and unbiased. According to the visualizations, we can directly see the trend of curve growth and the number of people who are infected by coronavirus in different provinces so that effective measures can be taken to better control the spread of the new coronavirus.

### 3. Introduction

The pandemic of coronavirus in China had become more and more serious since the first case of COVID-19 was spotted in Wuhan, Hubei. Back to February 12, 2020, the spreading of the coronavirus reached its peak, with 15152 newly confirmed cases appeared in China. Chinese government took effective measures to control the pandemic. Almost all people in China stayed at home, and if they had to go out, they always wore a mask, which was of great help for preventing virus from spreading. 

In this report, [time_series_covid19_confirmed_global.csv](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv) is the dataset we use which is created by Johns Hopkins University. This dataset is updated every day. It shows novel coronavirus pneumonia daily confirmed in different countries since January 22, 2020.

The original visualizations include a line chart, which reveals the trend of the increasement of confirmed cases from January 22, and a pie chart, which shows the proportion of confirmed cases in different provinces by November 28. The improvements of the line chart include removing the grid, adjusting the x-axis, and emphasizing the turning point. The improvements of the pie chart include using labels instead of legends, adjusting the label, and removing the shadow.

### 4. Replicate the Graph and Make some Improvement

#### 4.1 Temporal Trend since Jan 22, 2020.

Now looking at the temporal distribution graph of the coronavirus in China, we can intuitively know that since January 22, the number of confirmed cases had been increased to about 80000 in 45 days or so. After that, the increase in the number of confirmed cases has slowed down, and the order of production and life in various places has gradually recovered.

Here is the original visualization.

<center>
<img width=800, src=./chart/__results___39_20.png>
</center>

We replicate the visualization by using matplotlib. The title of the visualization is "China confirmed cases". However, as a matter of fact, confirmed cases in Taiwan is not included in this visualization. In other words, the data the author uses only includes mainland China, Hongkong and Macau. So the title must be changed.

Here the visual variable is the **position of x-axes and y-axes**.

<center>
<img width=800, src=./chart/line_chart.png>
</center>

We improve the graph according to the guidelines of information visualization. The details are as follows.

+ Grid is not very essential because in our opinion, it is better for us to know to what extent the curve goes rather than the exact number of confirmed cases every day. In other words, we are trying to reflect the trend of the virus. Besides, removing the grid is helpful to increase the data ink ratio.
+ We also make some changes of the axis. Originally, the author used numeric values to represent the number of days after January 22. However, if the readers want to know the datetime, they ought to do some calculations between the number on the x-axis and January 22 to get the exact date, which may make it troubled for readers. Therefore, in this line plot, it is better to use time stamps in X-axis rather than numeric values.
+ On March 5, the number of confirmed cases in China increases to more than 80000. But after that, the trend goes up more slowly than before. Therefore, we think that point is a turning point so that we point it out directly in the graph.

<center>
<img width=800, src=./chart/improved_line_chart.png>
</center>

Eventually, we make a dynamic line chart based on the line chart shown above. The code about generating the dynamic line chart is put in another file named *"Dynamic_line_chart.ipynb"*. One of the ontology of visualizaions based on user task is to zoom in. Nevertheless, a regular static line chart does not allow readers to zoom in and out. Different from the line chart made before, this dynamic line chart provides interactive tools to zoom in and zoom out so that the reader can zoom in on items of interest.

<center>
<img width=800, src=./chart/Dynamic_line_chart.png>
</center>

After executing the code, a html file which contains the dynamic line chart is generated and put in the same folder.

[Covid-19_visualization](Covid-19_visualization.html)

As can be seen from the graph, in the early days of the outbreak, that is, before March, the number of confirmed cases of new coronavirus increased sharply. This was mainly because people had limited understanding of the virus at that time and did not know the severity of the epidemic. And the beginning of February is the Spring Festival, which is a traditional Chinese festival. At that time, a lot of people who went out to work would choose to go home and reunite for the New Year. This caused a nationwide population movement and provided conditions for the spread of the virus. 

At that time, the Chinese government took some measures to coordinate and control the epidemic. On 23 January 2020, the central government of China imposed a lockdown in Wuhan and other cities in Hubei in an effort to quarantine the center of an outbreak of coronavirus disease 2019 (COVID-19). The strictest control measure was applied after April 8. Meanwhile, every Chinese citizen complied with quarantine regulations, consciously stayed at home and reduced unnecessary outings. The Chinese government had also adopted measures including free nucleic acid testing for the public, the government’s burden of patient treatment costs, and the adoption of various digital health certification measures, which were all proved to be important roles in coordinating epidemic control. 

#### 4.2 Epidemic of New Coronavirus in Different Provinces

The author selected the top five provincial administrative regions with the largest number of confirmed cases. The original visualization is as follows.

<center>
<img width=400, src=./chart/__results___110_8.png>
</center>

Similarly, we replicate the original visualization by matplotlib. The visual variables are **angle of the circle for the portion and color for category**.

<center>
<img src=./chart/pie_chart.png>
</center>


From the pie chart and dataset, we can know that as of November 28, Hubei Province has 67,704 cases in total, because first case broke out in Wuhan, where is the provincial capital of the Hubei. The region with the second largest number of confirmed cases is Hong Kong with 6,238 confirmed cases. Followed by Guangzhou, Shanghai and Zhejiang, their confirmed numbers were 1,963, 1,321, 1,284 respectively. There are 13,576 confirmed cases in other provinces, municipalities, autonomous regions and special administrative regions across the country.

> Note: If you want to look up other provinces' confirm cases, change **labels** in **Project2.ipynb** file.

There are also something in this pie chart that needs to be improved. Here are some points concerning how and why we make these improvements.

+ In the original visualization, legend is used to represent what each color represents for. Admittedly, using a legend is a good way to distinguish different categories. But according to congnitive theory and guidelines for information visualizations, legends require the reader to go back and forward, which may make it hard for them focus on the picture as a whole. Besides, in previous classes, we learnt that information visualization should avoid unwanted congnitive tunneling that is a mental state in which your brain focuses on a particular thing and does not see the rest of the environment. If there is a legend in the graph, the readers will be difficult to process the graph. In addition, as is known to all, our working memory is limited. The readers will have to load the working memory with the legend, which may result in overload of working memory. Taking what has been discussed above into consideration, the best solution to this problem is to use labels so that readers can focus on the picture as a whole and extract useful information directly from the picture.
+ Pie chart displays how the size of each category adds up to the whole population. It visualizes portions that sum up to 1. Therefore, in pie chart, the size of the circle represents the portion rather than the exact number of individual in each category.
+ The shadow in original visualization only serves the purpose of decoration and is of no use to describe the data. Removing the shadow also helps increase the data ink ratio of the graph. So it is necessary for us to remove the shadow.

<center>
<img src=./chart/improved_pie_chart.png>
</center>

Pie charts help us see how the size of each category adds up to 1. The data type of the pie chart is norminal with ratio. If we only want to compare the portion of different categories, pie chart is enough. But if we want to compare the number of items that each category has directly, bar chart is more suitable.

Details of improvement for bar chart:
+ We turn each sector in the pie chart into different bars in the bar chart. The data type of x-axis in bar chart is categorical, which means x-axis shows the specific categories being compared. Unlike the pie chart, there is no need to use different colors to distinguish different categories. The angle of sector represents the portion while the height of the bar represent the number of individuals in different catrgories. Thus, the data type of y-axis in bar chart ought to be discrete. 
+ The right, upper, and left borders should be erased so that data ink ratio can be increased. 
+ Elements should be directly labeled in order to avoid indirect look-up. Cognitive tunnelling may naturally happen when looking at a visual element in the graph. lf that happens,the user will not lose relevant information as long as the labels are close. So the number of items in each category should be labeled directly on the top of the bar.

The visual variable here is **the height of the bar and the position in x-axis**.

<center>
<img src=./chart/bar_chart.png>
</center>


### 5. Conclusion

As is mentioned above, what we have done to improve the pie chart are:

+ Removing the grid in order to erase the non-data ink.
+ Converting the data type of the x-axis from numeric to timestamp.
+ Emphasizing March 3, which can be seen as a turning point.

Our improvements to the pie chart are:

+ Using labels instead of legends
+ Modifying the label to the ratio of the number of individuals in each category to the total number.
+ Removing the shadow which is unnecessary.

Finally, we create a bar chart based on the pie chart and mark the number of individuals of each category at the top of each bar for easier comparison.

