---
title: "Visualizing The Gender Gap In College Degrees"
date: 2018-08-01
tags: [data wrangling, data science, messy data]
header:
excerpt: "Data Wrangling, Data Science, Messy Data"
mathjax: "true"
---

```python
#Guided Project - Visualizing The Gender Gap In College Degrees

%matplotlib inline
import pandas as pd
import matplotlib.pyplot as plt
```


```python
women_degrees = pd.read_csv('percent-bachelors-degrees-women-usa.csv')
cb_dark_blue = (0/255,107/255,164/255)
cb_orange = (255/255, 128/255, 14/255)
stem_cats = ['Engineering', 'Computer Science', 'Psychology', 'Biology', 'Physical Sciences', 'Math and Statistics']
```


```python
fig = plt.figure(figsize=(18, 3))

for sp in range(0,6):
    ax = fig.add_subplot(1,6,sp+1)
    ax.plot(women_degrees['Year'], women_degrees[stem_cats[sp]], c=cb_dark_blue, label='Women', linewidth=3)
    ax.plot(women_degrees['Year'], 100-women_degrees[stem_cats[sp]], c=cb_orange, label='Men', linewidth=3)
    ax.spines["right"].set_visible(False)    
    ax.spines["left"].set_visible(False)
    ax.spines["top"].set_visible(False)    
    ax.spines["bottom"].set_visible(False)
    ax.set_xlim(1968, 2011)
    ax.set_ylim(0,100)
    ax.set_title(stem_cats[sp])
    ax.tick_params(bottom="False", top="False", left="False", right="False")
    
    if sp == 0:
        ax.text(2005, 87, 'Men')
        ax.text(2002, 8, 'Women')
    elif sp == 5:
        ax.text(2005, 62, 'Men')
        ax.text(2001, 35, 'Women')
plt.show()
```

    C:\Users\Jamarco\Anaconda3\lib\site-packages\matplotlib\cbook\deprecation.py:107: MatplotlibDeprecationWarning: Passing one of 'on', 'true', 'off', 'false' as a boolean is deprecated; use an actual boolean (True/False) instead.
      warnings.warn(message, mplDeprecation, stacklevel=1)
    


![png](images/Project_files/Project_2_1.png)



```python
stem_cats = ['Psychology', 'Biology', 'Math and Statistics', 'Physical Sciences', 'Computer Science', 'Engineering']
lib_arts_cats = ['Foreign Languages', 'English', 'Communications and Journalism', 'Art and Performance', 'Social Sciences and History']
other_cats = ['Health Professions', 'Public Administration', 'Education', 'Agriculture','Business', 'Architecture']
```


```python
#defining a function to plot our 3 lists
#category: the list we wanted to plot
#plotting_start_pos: the start position of our plot
def plotting_charts(category,plotting_start_pos):
    #iterates through the list we passed as a parameter
    for field in range(0,len(category)):
        #creates the plot and plot the lines
        ax = fig.add_subplot(6,3,plotting_start_pos)
        ax.plot(women_degrees['Year'], women_degrees[category[field]],
                c=cb_dark_blue, label='Women', linewidth=3)
        ax.plot(women_degrees['Year'], 100-women_degrees[category[field]],
                c=cb_orange, label='Men', linewidth=3)
        #setting the spines off
        for pos in ax.spines:
            ax.spines[pos].set_visible(False)      
        #setting the x and y limits - min , max
        ax.set_xlim(1968, 2011)        
        ax.set_ylim(0,100)
        #setting the plot title
        ax.set_title(category[field])
        
        #turning off the ticks on all 4 sides and turning off the label of the x-axis
        ax.tick_params(bottom="False", top="False", left="False", right="False",
                      labelbottom='False')
        
        #setting the only tick we wanted in the y-axis
        ax.set_yticks([0,50,100])
        
        #setting a vertical line at the 50%
        ax.axhline(y=50, c=(171/255, 171/255, 171/255), alpha=0.3)
        
        #setting the caption on some plots and the label on the x-axis in the bottom plots
        if (plotting_start_pos == 1):
            ax.text(2002, 87, 'Women')
            ax.text(2002, 8, 'Men')
        elif (plotting_start_pos == 2):
            ax.text(2002, 78, 'Women')
            ax.text(2002, 18, 'Men')
        elif (plotting_start_pos == 3):
            ax.text(2002, 92, 'Women')
            ax.text(2002, 5, 'Men')
        elif (plotting_start_pos == 14):
            ax.tick_params(labelbottom='True')
        elif (plotting_start_pos == 16):
            ax.text(2002, 92, 'Men')
            ax.text(2002, 5, 'Women') 
            ax.tick_params(labelbottom='True')
        elif (plotting_start_pos == 18):
            ax.text(2002, 70, 'Men')
            ax.text(2002, 25, 'Women')
            ax.tick_params(labelbottom='True')
        
        #setting the position of the next plot - if the list isn't finished yet.
        plotting_start_pos += 3

```


```python
fig = plt.figure(figsize=(12,18))
plot_pos = 1


plotting_charts(stem_cats, 1)
plotting_charts(lib_arts_cats,2)
plotting_charts(other_cats, 3)
plt.savefig('biology_degrees.png')
plt.show()
    
    
        
```

    C:\Users\Jamarco\Anaconda3\lib\site-packages\matplotlib\cbook\deprecation.py:107: MatplotlibDeprecationWarning: Passing one of 'on', 'true', 'off', 'false' as a boolean is deprecated; use an actual boolean (True/False) instead.
      warnings.warn(message, mplDeprecation, stacklevel=1)
    


![png](images/Project_files/Project_5_1.png)



```python
women_degrees.dropna()
```
