#Install Rfacebook package in RStudio
install.packages("Rfacebook") 

#Install plotly package in RStudio
install.packages("plotly")

#Next step is to load the Rfacebook package using library() function.
library(Rfacebook)

#Load plotly package using library() function again.
library(plotly)

#Fill the token here('XXXX') that you get from https://developers.facebook.com/tools/explorer.
token = 'XXXXX'


#########For Clinton vs Trump#########


#Now, save 10 posts from Hillary Clinton's page into page_h variable.
page_h <- getPage("hillaryclinton", token, n = 10, since='2015/11/06', until='2015/11/12')

#Save the number of likes on the posts in y1
y1 = page_h$likes_count

#Save 10 posts from Donald Trump's page into page_t variable.
page_t = getPage("donaldtrump", token, n = 10, since='2015/11/06', until='2015/11/12')

#Save the number of likes on the posts in y2
y2 = page_t$likes_count

#To plot, combine the posts' names.
x = c("Post1", "Post2", "Post3","Post4", "Post5", "Post6","Post7", "Post8","Post9", "Post10")

#Combine everything.
data <- data.frame(x, y1, y2)

#This will make sure everything goes in an order.
data$x <- factor(data$x, levels = data[["x"]])

#Plot the data using plotly function and give labels.
p = plot_ly(data, x = ~x, y = ~y1, type = 'bar', name = 'Hillary Clinton', marker = list(color = 'rgb(49,130,189)')) %>%    
 add_trace(y = ~y2, name = 'Donald Trump', marker = list(color = 'rgb(204,204,204)')) %>%
 layout(xaxis = list(title = "Facebook posts in US Election week 2016", tickangle = -45),
 yaxis = list(title = "No. of likes"),
 margin = list(b = 80),
 barmode = 'group')

#Finally show the graph.
 p


#########For Obama vs Trump#########


 page_h <- getPage("barackobama", token, n = 10, since='2015/11/04', until='2015/11/12')

y1 = page_h$likes_count

page_t = getPage("donaldtrump", token, n = 10, since='2015/11/06', until='2015/11/12')

y2 = page_t$likes_count

x = c("Post1", "Post2", "Post3","Post4", "Post5", "Post6","Post7", "Post8","Post9", "Post10")

data <- data.frame(x, y1, y2)

data$x <- factor(data$x, levels = data[["x"]])

p = plot_ly(data, x = ~x, y = ~y1, type = 'bar', name = 'Barack Obama', marker = list(color = 'rgb(49,130,189)')) %>%    
 add_trace(y = ~y2, name = 'Donald Trump', marker = list(color = 'rgb(204,204,204)')) %>%
 layout(xaxis = list(title = "Facebook posts in US Election week 2016", tickangle = -45),
 yaxis = list(title = "No. of likes"),
 margin = list(b = 80),
 barmode = 'group')

 p