# assi6b
dataset = read.csv('dataset.csv')
#delete missing value
dataset$age = ifelse(is.na(dataset$age),ave(dataset$age, FUN = function(x) mean(x, na.rm = 
'TRUE')),dataset$age)
dataset$salary = ifelse(is.na(dataset$salary), ave(dataset$salary, FUN = function(x) mean(x, na.rm = 
'TRUE')), dataset$salary)
dataset$age = as.numeric(format(round(dataset$age, 0)))
dataset$nation = factor(dataset$nation, levels = c('India','Germany','Russia'), labels = c(1,2,3))
dataset$purchased_item = factor(dataset$purchased_item, levels = c('No','Yes'), labels = c(0,1))
#splitting data
install.packages('caTools') #install once
library(caTools) # importing caTools library
set.seed(123)
split = sample.split(dataset$purchased_item, SplitRatio = 0.8)
training_set = subset(dataset, split == TRUE)
test_set = subset(dataset, split == FALSE)
training_set[,3:4] = scale(training_set[,3:4])
test_set[,3:4] = scale(test_set[,3:4])
