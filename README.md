# healthdataregression
Analyzing Medical Bills data

### Project Overview
In this project, I looked into seeing what goes into the total charge for medical bills. I analyzed different patients' bill totals along with different attributes to see what are the most important factors that go into determining higher or lower charges. 

### Dataset Description
The dataset consists of approximately 1,500 records of patients' medical bills which contain the following patient attributes: age, sex, bmi, children (number of children), smoker (yes/no), region (southwest, southeast, northwest, northeast), charges (total charge). The dataset consists of various data types including numeric, boolean and string

### Loading the Data
```r
df = read.csv('insurance.csv', header=TRUE)
num_cols <- unlist(lapply(df, is.numeric))  
```

### Exploratory Data Analysis
```{r}
plot(df[,num_cols])
```

![image](https://user-images.githubusercontent.com/114118047/192162626-59be2efa-5ddc-4395-a897-f63a66d89585.png)

The first step I took in the exploratory data analysis process was to plot the numeric values against each other to try and understand what this dataset might look like. Some of the more significant aspects I noticed here was that as the number of children goes up, the charges actually were lower. Also, looking at bmi, there seems to be two different clusters of data points. Other than that, there seems to be  correlation between age and charges.

```{r}
round(cor(df[,num_cols]),2)
```

To continue with the analysis, I found the correlations between the numeric attributes. The values for charges however were not too high. The highest values were with age and bmi which were only at 0.30 and 0.20 respectively. Nevertheless, these were not the only attributes in the dataset.

```{r}
boxplot(df$charges ~ df$smoker, main ='Smoker')
boxplot(df$charges ~ df$sex, main ='sex')
boxplot(df$charges ~ df$region, main ='region')
```

![image](https://user-images.githubusercontent.com/114118047/192162734-40fbe33d-7121-49e1-a878-ba96ee5af90c.png)

![image](https://user-images.githubusercontent.com/114118047/192162746-b8231f1c-a50c-41d0-ba97-9cd429737e87.png)

![image](https://user-images.githubusercontent.com/114118047/192162750-d65e6aa2-6dfe-4356-9169-b5c8d90de65b.png)

For the other attributes, I created a few box plots to see if they had any impact on the total charges. The attribute 'Smoker' had a clear impact since the average charges for smokers and the IQR in general was much higher than for non smokers. 'Sex' also seemed to have an impact since there did seem to be some higher values for males and the average for males looked to be slightly higher. The southeast region also seemed to play a significant role when determining charges as it seemed higher than other regions. The southwest region also seemed to have quite a bit of values on the higher end.

### Linear Regression
```{r}
model1 = lm(charges ~. , data =df)
summary(model1)
```
![Screenshot (135)](https://user-images.githubusercontent.com/114118047/192162874-39bada6a-6f8e-4db0-97f4-1c502910de3a.png)

The next step was to plot a Linear Regression model to be able to predict medical bill total charges based on certain significant attributes. We also wanted to find out what those attributes were. From the model, we can see that age, bmi, number of children, and region were definitely significant as they had p-values of less than 0.05. Age, BMI, number of children and smoker all being very highly significant. Sex was not significant. 


### Conclusion
With the analysis of this dataset, I have been able to discover more insight about medical data. I was able to create a linear regression model which can help people accurately estimate and potentially determine how much they will charged at the hospital. One of the more surpising discoveries from the linear regression model was that sex did not actually play a significant role. My assumption going into this project was that women on average would be charged more than men, but this analysis proved me wrong. It was also a surprising discovery that the region also plays a role. Patients in the southern regions tend to be charged more. 

Overall, analyzing this health data helped me gain more insight regarding the medical industry and motivated me to continue exploring this field even more.
