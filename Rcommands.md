# Sample commands in R
```
sudo -i R
# test installation 
install.packages('txtplot')
library('txtplot')
cars
txtplot(cars[,1], cars[,2], xlab = "speed", ylab = "distance")

# install the ggplot2 package
install.packages("ggplot2")  

# load the package
library(ggplot2)
ggplot(mpg, aes(displ, hwy, colour = class)) + 
  geom_point()

# check installed packages
installed.packages()
# list all packages where an update is available
old.packages()

# update all available packages
update.packages()

# update, without prompts for permission/clarification
update.packages(ask = FALSE)

# update only a specific package use install.packages()
install.packages("plotly")
```
