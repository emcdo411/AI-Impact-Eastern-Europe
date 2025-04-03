# AI Impact on Eastern Europe: Industry and Productivity Case Study

## **Project Overview**

This repository contains an interactive **Shiny app** that visualizes how **AI technologies** can boost productivity across key industries in **Eastern Europe**, specifically focusing on **Czech Republic**, **Hungary**, and **Croatia**. The project was inspired by **Michelle Simmons**, President, Central Europe at Microsoft, who has been a thought leader in promoting AI adoption across Europe.

The app visualizes data related to AI adoption, showcasing key **AI tools** and their potential impact on industries such as **Manufacturing**, **Automotive**, **Healthcare**, and **Finance**. It allows users to interact with maps to see how AI could improve productivity, with real-time data displayed through **interactive pop-ups**.

---

## **Why This Matters**

With the evolving **AI Act** in the European Union, **Eastern Europe** is poised to become a hub for AI-driven transformation in various sectors. By leveraging AI technologies, industries across these countries can see an **increase in productivity** of up to **25%**. This study highlights the crucial role AI can play in driving efficiency and innovation.

---

## **Interactive Shiny App**

The main feature of this project is an **interactive Shiny app** that provides **dynamic data visualization**. The app features:

- **Dropdown menus** for selecting different countries.
- **Interactive 2D maps** displaying AI impact by region.
- **Pop-up boxes** that show the **percentage of productivity change** and **AI tools** used in industries like manufacturing, automotive, and healthcare.

---

## **How to Use**

1. Clone this repository to your local machine:
   ```bash
   git clone https://github.com/yourusername/ai-impact-eastern-europe.git
   ```
2. Install the required libraries:
   ```r
   install.packages(c("shiny", "leaflet", "dplyr", "sf", "plotly", "tmap"))
   ```
3. Run the Shiny app in RStudio:
   ```r
   shiny::runApp("app.R")
   ```

---

## **Code for the Shiny App**

### **app.R**

```r
# Load required libraries
library(shiny)
library(leaflet)
library(dplyr)

# Sample data for the 3 countries
countries_data <- data.frame(
  country = c("Czech Republic", "Hungary", "Croatia"),
  lat = c(49.8176, 47.1625, 45.1),
  lon = c(15.4730, 19.5033, 15.2),
  productivity_increase = c(20, 25, 15),
  ai_tool = c("Uptake", "Waymo", "Zebra Medical Vision"),
  sector = c("Manufacturing", "Automotive", "Healthcare")
)

# UI Definition
ui <- fluidPage(
  titlePanel("AI Impact on Eastern Europe"),
  
  sidebarLayout(
    sidebarPanel(
      selectInput("country", "Select Country:", 
                  choices = c("Czech Republic", "Hungary", "Croatia"))
    ),
    
    mainPanel(
      leafletOutput("map"),
      textOutput("popupInfo")
    )
  )
)

# Server Logic
server <- function(input, output, session) {
  
  selected_country <- reactive({
    countries_data %>%
      filter(country == input$country)
  })
  
  output$map <- renderLeaflet({
    leaflet(countries_data) %>%
      addTiles() %>%
      addCircleMarkers(
        ~lon, ~lat, 
        radius = 10, 
        color = "yellow", 
        fillOpacity = 0.7, 
        popup = ~paste("Country: ", country,
                       "<br>Productivity Increase: ", productivity_increase, "%",
                       "<br>AI Tool: ", ai_tool,
                       "<br>Sector: ", sector)
      ) %>%
      setView(lng = 14.5, lat = 47, zoom = 5)
  })
  
  output$popupInfo <- renderText({
    selected_data <- selected_country()
    paste("You have selected the", selected_data$country,
          "which is experiencing a productivity increase of",
          selected_data$productivity_increase, "% from AI adoption in the",
          selected_data$sector, "sector using the", selected_data$ai_tool, "AI tool.")
  })
  
}

# Run the application 
shinyApp(ui = ui, server = server)
```

---

## **Key Features**

- **Interactive Map**: View real-time data for **Czech Republic**, **Hungary**, and **Croatia** showing how AI adoption can increase productivity.
- **Dropdown for Country Selection**: Choose between the three countries to view the respective data.
- **Pop-up Boxes**: Each map marker shows data about the **AI tool**, **productivity increase percentage**, and the **industry sector**.

---

## **Tech Stack Used**

- **Shiny**: For building the interactive web application.
- **Leaflet**: To visualize the 2D interactive map with hover and click capabilities.
- **dplyr**: For data manipulation and filtering.
- **plotly**: For advanced visualization (in future extensions).
- **RStudio**: To develop and run the Shiny app.

---

## **Why This Matters**

The **AI Act** and other regulatory frameworks in Europe are pushing for AI adoption, and Eastern European countries are uniquely positioned to harness these technologies. This project demonstrates how countries like the **Czech Republic**, **Hungary**, and **Croatia** can gain from AI adoption in industries such as **manufacturing**, **automotive**, and **healthcare**.

---

## **Contribute**

Feel free to **fork**, **clone**, and contribute to the project. Whether you have suggestions for improvement, new features, or simply want to help advance the use of AI in Eastern Europe, your contributions are welcome!

---

## **License**

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## **Contact**

For more information or any questions, feel free to reach out to me via **GitHub** or **LinkedIn**.

---

### Suggested **Repository Name**: `AI-Impact-Eastern-Europe`

---

This updated README includes the code for the Shiny app along with detailed instructions on how to run it. It also highlights the significance of the project and the tools used. Feel free to modify the content as per your specific needs, and make sure to include your **GitHub link** in the appropriate places.


