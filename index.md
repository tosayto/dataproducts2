---
title       : Usa Facts at 70s 
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


```
stateDF = data.frame(State = state.name, state.x77)
names<-names(stateDF)

```



--- 

## server.R

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

 
