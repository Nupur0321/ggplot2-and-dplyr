# ggplot2-and-dplyr
Visualisation in R by ggplot2 and dplyr

Exercise 1\
Use the mtcars dataset to generate a scatterplot of the mpg against disp. Colour the points on the chart based on the number of gears the car has. Make the size of the points link to the number of carburettors the car has.

solution
```
data <- mtcars
data
View(mtcars)
library(ggplot2)
```

ggplot(data=mtcars, aes(x=disp, y=mpg, colour=gear, size=carb)) + geom_point()

Exercise 2\
Generate a boxplot of the mpg of the dataset.\
(i) Now generate this but a different boxplot for each number of cylinders a car has.\
(ii) Regenerate this with a violin plot instead of a boxplot.

solution

boxplot(mtcars$mpg)\
ggplot(data=mtcars, aes(x=mpg, y=cyl)) + geom_boxplot()

boxplot(mtcars$mpg ~ mtcars$cyl)

u <- ggplot(data=mtcars, aes(x=mpg, y=cyl, colour=mpg))\
u + geom_boxplot()

str(mtcars)\
mtcars$cyl <- as.factor(mtcars$cyl)\
u <- ggplot(data=mtcars, aes(x=cyl, y=mpg, colour=mpg))\
u + geom_violin()


Exercise 3\
It is proposed that the number of cylinders a car has is linked to its horsepower. You should use appropriate visualisations to explore this relationship. You should also use appropriate smoothers to explore this hypothesis.

solution

ggplot(data=mtcars, aes(x=cyl, y=hp, colour=cyl)) + geom_point() +
  geom_smooth(method = "auto", se=T)+ geom_jitter()+
  labs(subtitle="Horsepower vs Number cylinders",\
       y="Horsepower",\
       x="No of Engine Cylinders",\
       title = "smoothed scatterplot",\
       caption = "source:mtcars")

Exercise 4\
Two car enthusiasts are debating which has more of an impact on a standing quarter mile sprint time. One says horsepower is all that matters. You should conduct an analysis to see if the data in this dataset supports this.

solution

ggplot(data=mtcars, aes(x=qsec, y=mpg, colour=qsec)) + geom_point()\
ggplot(data=mtcars, aes(x=hp, y=mpg, colour=qsec)) + geom_point()


Exercise 5\
It has been proposed that V engines have a particular advantage over inline engines. Explore the dataset to see if you can find any evidence to support this.

solution

mtcars$vs2[mtcars$vs=="0"] <- "V-shaped"\
mtcars$vs2[mtcars$vs=="1"] <- "Straight"\
ggplot(data=mtcars, aes(x=vs2, y=hp, colour=vs)) + geom_boxplot()
