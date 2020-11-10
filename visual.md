# Project1

## 1. Student(s)

+ Xiangwen Qiao, qiaoxw18@lzu.edu.cn
+ Zunye tang, tangzy18@lzu.edu.cn

## 2. Three Main Methods
In our implement, we encapsulate three methods one class named *Box()*. Now I'm gonna introduce three main parts of this class.

### 2.1 info_boxplot
Defination and parameters are as follows:

```python
def info_boxplot(self, data:list(list()), ax=None, multiplebox=False, edgecolor="black",central_line_color="red", alpha=0.8, ignore_outlier=False):
    """
    :param data: Required int or float type data in the format of list(list()), each list has a box plot.
    :param ax: Option axis, a single `~matplotlib.axes.Axes` object.
    :param multiplebox: Boolean, default False, plot every 5%-percentile line from the 1st quartile (Q1) until the 3rd quartile (Q3)
    :param edgecolor: Option, default black.
    :param central_line_color: Option, default red, 50%-percentile data line.
    :param alpha: Option, default = 0.8,
    :param ignore_outlier: Boolean, default False, ignore outlier data.
    :return: ~matplotlib.figure()
    """
```
Remove the **Null value** in the data. And calculate the **25, 50, 75 percentile data of each list**. 
```python
for d in data:
    d = d[np.logical_not(np.isnan(d))]
    t = np.percentile(d, (25, 50, 75), interpolation='midpoint')
```
Find the **outliers** of each data list, and temperaly **append them in a list named outlier_list**.

In the end, according to the **ratio of the length of y-axis and x-axis**, add **patches.Ellipse(xy,width=0.05,height=0.05*ratio)**.
```python
ratio = (up_lim-low_lim)/p
for i,j in enumerate(outlier_list):
    for k in j:
        ell = mpatch.Ellipse((i+1,k), width=0.05, height=0.05 * ratio, edgecolor=edgecolor, facecolor="white")
        self.ax.add_patch(ell)
```

### 2.2 histobox_plot
```python
def histobox_plot(self,data:list(list()), ax=None, edgecolor="black",central_line_color="red",alpha=0.8, facecolor="darkgrey"
                    ignore_outlier=False):
    """
    :param data: Required int or float type data in the format of list(list()), each list has a box plot.
    :param ax: Option axis, a single `~matplotlib.axes.Axes` object.
    :param edgecolor: Option, default black.
    :param central_line_color: Option, default red, 50%-percentile data line.
    :param alpha: Option, default = 0.8.
    :param facecolor: Option, default darkgrey.
    :param ignore_outlier: Boolean, default False, ignore outlier data.
    :return: ~matplotlib.figure()
    """
```
Remove the parameter *multiplebox* and keep the left part of the boxplot.

But add patches in this method.
```python
bin = 10
(counts, bins) = np.histogram(d, bins=bin)
step = (maxm-minm)/(bin+1)
normalized_counts = (counts - np.min(counts)) / (np.max(counts) - np.min(counts)) / 2

for i in range(bin):
    rect = plt.Rectangle((p,step*i),width=normalized_counts[i],height=step, fill=True, facecolor=facecolor, alpha=alpha,
        linewidth=2,edgecolor="black")
    self.ax.add_patch(rect)
```

### 2.3 creative_boxplot




## 3. Android Open Source Data and Create instance
```python
df = pd.read_csv(r"PATH",header=0)  # Load Android Open Source Data path.
data = []
subdf = df.loc[:50,["rating_value","commits","sonar_major_issues","sonar_minor_issues_ratio"]]
for i in range(subdf.shape[1]):
    data.append(np.array(subdf.iloc[:,i]))
```

Using **real dataset Android Open Source Data**, and use columns, **"rating_value", "commits","sonar_major_issues", "sonar_minor_issues_ratio"**, as examples.

**rating_value:** Continuous data type. 

**commits:** Discrete data type.

**sonar_major_issues:**  Discrete data type.

**sonar_minor_issues_ratio:** Ratio data type.

### 3.1 info_boxplot
```python
box = Box()
box.info_boxplot(data,None,multiplebox=True,ignore_outlier=True)
plt.show()
```
We ignore_outlier data for a better view of data. The first group data and the fourth group data is continuous and ratio data type, so they are **too small** to show. We can do a little trick to solve this problem by multiply two columns 100 times or we can just remove these too big conlumns.

<center>
<img width=500, src=./figures/info_boxplot.png />
</center>

After transformation:
<center>
<figure>
<img width=265, src=./figures/info_boxplot_pro1.png /><img width=265, src=./figures/info_boxplot_pro2.png />
</figure>
</center>

### 3.2 histobox_plot
```python
box.histobox_plot(data,None,ignore_outlier=True)
plt.show()
```
Similar to the first one.
<center>
<img width=500, src=./figures/histobox_plot.png />
</center>

### 3.2 creative_boxplot
```python
box.creative_boxplot(data,None)
plt.show()
```
This plot shows that the boxplot figure at the left y-axis in a more appearent way, and we add probability density curve at the right y-axis. We think PDF can show the distribution of the data, and we wanna try to mix two plot into one figure.

<center>
<img width=500, src=./figures/creative_boxplot.png />
</center>


**??？需要把creative_boxplot再改改**



## 4. Additional Information

### 4.1 About Conhensiveness
We donot split this project into two parts strictly, instead, we implement this project 

### 4.2 Test Data and Data Type
In our project, we illustrate an example using real data set, Android Open Source Dataset, and clarify the data type of the data in the third part.


### 4.3 Execution Notes

**Plot three main methods(info_boxplot,histobox_plot,creative_boxplot) in one figure will cause unknown problems.** It may overlay draw the figure or loss one of the figures.

It's better set the axis is None, it will create a brand-new figure that will not ever cross with each other. In this way, code will execute without issues.




**???explain data plot**