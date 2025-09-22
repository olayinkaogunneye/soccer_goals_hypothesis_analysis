#load required libraries
library(dplyr)
library(lubridate)
library(ggplot2)
library(here)
library(readr)

## Step 2: Load and Inspect the Data

# Load the datasets using here()
women <- read.csv(here("data", "raw", "women_results.csv"))
men   <- read.csv(here("data", "raw", "men_results.csv"))

# Check structure
str(women)
str(men)

# Peek at the first few rows
head(women)
head(men)

## Step 3: Filter for FIFA World Cup Matches After 2002-01-01
### We want to:
  ###  Include only official FIFA World Cup matches (not qualifiers)
  ### Only matches after January 1, 2002

# Filter women's FIFA World Cup matches after 2002-01-01
women_wc <- women %>%
            filter(tournament == "FIFA World Cup", date >= as.Date("2002-01-01"))

#Filter men's FIFA World cup matches after 2002-01-01
men_wc <- men %>%
  filter(tournament == "FIFA World Cup", date >= as.Date("2002-01-01"))

# Add total goals column
women_wc <- women_wc %>% 
            mutate(total_goals = home_score + away_score)

men_wc <- men_wc%>%
   mutate(total_goals = home_score + away_score)


# Step 4: Exploratory Data Analysis

# Summary stats
summary(women_wc$total_goals)
summary(men_wc$total_goals)

# Standard deviation
sd(women_wc$total_goals)
sd(men_wc$total_goals)

# Histogram comparison
p_total_goals <- ggplot() +
  geom_histogram(data = women_wc, aes(x = total_goals), fill = "pink", alpha = 0.8, bins = 15) +
  geom_histogram(data = men_wc, aes(x = total_goals), fill = "lightblue", alpha = 0.8, bins = 15) +
  labs(title = "Distribution of Total Goals per Match",
       x = "Goals per Match", y = "Frequency") +
  theme_minimal()

# Save the plot
ggsave(
  filename = here( "outputs", "figures", "Distribution_of_Total_Goals.png"), 
  plot = p_total_goals, 
  width = 8, height = 6
)


# Combine datasets for boxplot
combined <- bind_rows(
  women_wc %>% select(total_goals) %>% mutate(gender = "Women"),
  men_wc %>% select(total_goals) %>% mutate(gender = "Men")
)

write_csv(combined, here("data", "processed", "fifa_WC men and women.csv"))

# Boxplot
box_plot_distribution <- ggplot(combined, aes(x = gender, y = total_goals, fill = gender)) +
  geom_boxplot(alpha = 0.7) +
  labs(title = "Goals per Match: Women vs Men",
       x = "Match Type", y = "Total Goals") +
  scale_fill_manual(values = c("pink", "lightblue")) +
  theme_minimal()

# Save the plot
ggsave(
  filename = here( "outputs", "figures", "Boxplot_Distribution_of_Total_Goals.png"), 
  plot = box_plot_distribution, 
  width = 8, height = 6
)

# Step 5: Hypothesis Test

# Hypotheses

# This is a one-tailed independent t-test.

# One-tailed t-test
t_test_result <- t.test(
  women_wc$total_goals,
  men_wc$total_goals,
  alternative = "greater",   # one-tailed: women > men
  var.equal = FALSE          # Welch's t-test (doesn't assume equal variance)
)

t_test_result


