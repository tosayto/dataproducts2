---
title       : USA Facts at 70s 
subtitle    : Income, Population etc.
author      : Z Ozcan 
job         : Internet
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## ui.R
- One picture is better than thousands words (numbers in this case).
- It looks simple when you see the results, but it isn't.
- Take the idea try it at home.
- You can apply it in many different situations.


```
library(shiny)

shinyUI(fluidPage(
  # Application title
  titlePanel("USA Facts at 70s"),
  # Sidebar with a select input
  sidebarLayout(
    sidebarPanel(
      selectInput('x','Select your fact',names[-1])
    ),
    # Show a plot of the chosen fact
    mainPanel(
            h3(textOutput("factTitle")),
      htmlOutput("distPlot")
    )
  )
))

```

--- 

## global.R

- Why global.R?
- If you need the same data in ui.R and server.R
- You don't need to duplicate your data.

```
stateDF = data.frame(State = state.name, state.x77)
names<-names(stateDF)

```



--- 

## server.R

- Problems with renderGvis function
- Solved with htmlOutput function in ui.R

```
library(shiny)
library(googleVis)
shinyServer(function(input, output) {
        
        output$factTitle<-renderText(
                ...
        )     
  output$distPlot <- renderGvis({

          
          gchart = gvisGeoChart(...)
          return(gchart)
  })
})

```

---  

## gvisGeochart function

- For the completeness


```
gchart = gvisGeoChart(data = stateDF,
                                locationvar = "State",
                                colorvar = input$x,
                                options = list(region="US",
                                               displayMode="regions",
                                               resolution="provinces",
                                               width=600, height=400
                                               ))

```

Don't you think that every president must use this kind of applications?
 
