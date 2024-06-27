# Sample AI script 

## Question 1(for Q4 part d)

**ME:** 

i already have a plot called pass_plot

pass_plot <- soccer_pitch_design + geom_point(data = passes, aes(x = location_x, 
                                                                 y = location_y, 
                               color = possession_team.name, shape = type.name), 
             size = 2) +
  labs(
    title = "Passes: Australia vs. Brazil (2019 Women's World Cup)",
    x = NULL,
    y = NULL,
    color = "Team",
    shape = "Type"
  ) +
  scale_color_manual(
    values = c("Australia" = "#1C9E77", "Brazil" = "#D95F02"),  
    labels = c("Australia", "Brazil") 
  ) +
  guides(shape = FALSE) +
  theme(
    legend.position = "bottom",  
    legend.title = element_blank()  
  )

is there a way of putting this into my code below, so that i can do a lineup?

ggplot(lineup(null_permute('possession_team.name'), passes), 
       aes(x= location_x, y= location_y, colour= possession_team.name)) +
  geom_point() +
  scale_color_manual(values = c("Australia" = "#1C9E77", "Brazil" = "#D95F02"), 
                     labels = c("Australia", "Brazil")) +
    theme_minimal() + 
    facet_wrap(~.sample) + 
    theme(legend.position = "bottom", legend.title = element_blank()) +
    theme(axis.text = element_blank(),
        axis.title = element_blank()) +
    ggtitle("Lineup for Passes: Australia vs. Brazil in 2019 Women's World Cup")
    

**CHATGPT:** To incorporate your pass_plot into the code for creating a lineup plot, you can use the annotate function to overlay the pass plot on top of the lineup plot. Here's how you can do it:

library(ggplot2)

# Your pass_plot code
pass_plot <- soccer_pitch_design + geom_point(data = passes, aes(x = location_x, 
                                                                 y = location_y, 
                                                                 color = possession_team.name, 
                                                                 shape = type.name), 
                                              size = 2) +
  labs(
    title = "Passes: Australia vs. Brazil (2019 Women's World Cup)",
    x = NULL,
    y = NULL,
    color = "Team",
    shape = "Type"
  ) +
  scale_color_manual(
    values = c("Australia" = "#1C9E77", "Brazil" = "#D95F02"),  
    labels = c("Australia", "Brazil") 
  ) +
  guides(shape = FALSE) +
  theme(
    legend.position = "bottom",  
    legend.title = element_blank()  
  )

# Your lineup plot code
lineup_plot <- ggplot(lineup(null_permute('possession_team.name'), passes), 
                      aes(x = location_x, y = location_y, colour = possession_team.name)) +
  geom_point() +
  scale_color_manual(values = c("Australia" = "#1C9E77", "Brazil" = "#D95F02"), 
                     labels = c("Australia", "Brazil")) +
  theme_minimal() + 
  facet_wrap(~.sample) + 
  theme(legend.position = "bottom", legend.title = element_blank()) +
  theme(axis.text = element_blank(),
        axis.title = element_blank()) +
  ggtitle("Lineup for Passes: Australia vs. Brazil in 2019 Women's World Cup")

# Overlay the pass plot on top of the lineup plot using annotate
final_plot <- lineup_plot +
  annotation_custom(ggplotGrob(pass_plot), xmin = -Inf, xmax = Inf, ymin = -Inf, ymax = Inf)

# Print or save the final_plot as needed
print(final_plot)


In this code, annotation_custom is used to overlay the pass_plot on top of the lineup_plot. This way, you can create a lineup plot with the pass information included.


--------

ANALYSIS: 

ChatGPT guided me on how to combine the pitch plot I already made for passes with the code I drafted to make a lineup, as I was unsure of how to maintain the pitch plot design in my lineup plots. It provided useful code that was easily understandable and straightforward, and also did not change any unnecessary aspects of the code which I had initially drafted. Hence, I was able to create a suitable lineup of plots that included the pitch plot design I wanted. 

However, it did not explain in detail the logic behind the 'annotation_custom' function. This may be difficult if I wanted to modify or adapt the solution for other different scenarios. Additionally, the provided solution does not provide information on customizing the plot further such as adjusting the size, position, or appearance of the pass plot within the lineup plot. This requires further experimentation on my part if I wanted to achieve specific design aspects for my plot.



## References 

Brown, L. (n.d.) Phone Aspect Ratio Vertical Definition, Types and Tips. Retrieved from https://filmora.wondershare.com/video-editing/phone-aspect-ratio.html

Department of Health. (2020). Tuberculosis notifications in Australia, 2015–2018. *Communicable diseases intelligence,* *44,* 1-39. https://doi.org/10.33321/cdi.2020.44.88 

Department of Health and Aged Care. (2022). Tuberculosis notifications in Australia [annual reports]. Retrieved from https://www1.health.gov.au/internet/main/publishing.nsf/Content/cda-pubs-annlrpt-tbannrep.htm

Gilroy, N. (1999). Tuberculosis notifications in Australia, 1997. National TB Advisory Group. Communicable Disease Network Australia and New Zealand. *Communicable diseases intelligence,* *23*(13), 337–348.

National Health and Medical Research Council. (2020). History of tuberculosis control in Australia. Retrieved from https://www.nhmrc.gov.au/about-us/resources/impact-case-studies/history-tuberculosis-control-australia

