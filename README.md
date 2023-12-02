# R-work-Probability-and-Statistics
## Overview
Welcome to the repository for the STAT2010 quiz "QUIZ4-STA2010." This quiz explores various aspects of bivariate normal distributions, visualizations, and statistical tests. Each task is carefully documented with code snippets and interpretations. Feel free to explore the sections below to understand the analysis and findings.

### Task 1: Generate Bivariate Normal Samples and Analyze Relationships
#### 1.1 Generate 1000 random samples from a bivariate normal distribution.
```{r}
# Load necessary libraries
library(MASS)
# Set parameters
mean_vector <- c(1, 2)
covariance_matrix <- matrix(c(2, 0.5, 0.5, 1), nrow = 2)
```
#### 1.2 Plot the generated samples using a scatter plot
```{r}
# Plot the generated samples
plot(random_samples, main = "Scatter Plot of Bivariate Normal Samples",
     xlab = "X-axis", ylab = "Y-axis")
# Calculate the regression line
regression_line <- lm(random_samples[, 2] ~ random_samples[, 1])
abline(regression_line, col = "red", lty = 2)  # Adding a regression line
```
#### 1.3 Interpretation and Further Analysis
- Positive Slope
- Strength of the Relationship
- Interpretation of the Scatter Plot
- Covariance Matrix Influence

### Task 2: Calculate and Plot Densities
```{r}
# Create a grid
x <- seq(-2, 4, length.out = 100)
y <- seq(-1, 5, length.out = 100)
grid <- expand.grid(X = x, Y = y)
grid
# Calculate the bivariate normal density for each point in the grid
grid$density <- dmvnorm(grid, mean = mean_vector, sigma = covariance_matrix)

# Convert the grid to a matrix for filled.contour
density_matrix <- matrix(grid$density, nrow = length(x), byrow = TRUE)

# Plot the bivariate normal density using filled.contour
filled.contour(x, y, density_matrix,
               main = "Filled Contour Plot of Bivariate Normal Density",
               xlab = "X-axis", ylab = "Y-axis",
               color.palette = terrain.colors, plot.title = element_text(hjust = 0.5))
```
### 3. Calculate Probabilities.
```{r}
# Choose a region of interest
region_of_interest <- subset(grid, X < 2 & Y < 3)

# Calculate the probability for the chosen region
probability <- sum(region_of_interest$density)

# Print the calculated probability
cat("Probability in the region of interest:", probability, "\n")

```
Visualising the region of interest
```{r}
# Plot the bivariate normal density using filled.contour
filled.contour(x, y, density_matrix,
               main = "Filled Contour Plot with Region of Interest",
               xlab = "X-axis", ylab = "Y-axis",
               color.palette = terrain.colors, plot.title = element_text(hjust = 0.5))

# Add a rectangle to highlight the region of interest
rect(-2, -1, 2, 3, col = rgb(1, 0, 0, 0.3), border = 1)

```
# 4. Testing for Multivariate Normality
```{r}
# Generate a sample of at least 100 observations and two variables
set.seed(456)
sample_data <- rmvnorm(n = 100, mean = mean_vector, sigma = covariance_matrix)

# Test for multivariate normality
shapiro_test <- shapiro.test(sample_data)

# Print and interpret the test results
cat("Shapiro-Wilk test for multivariate normality:\n")
print(shapiro_test)
if (shapiro_test$p.value > 0.05) {
  cat("The data follows a multivariate normal distribution.\n")
} else {
  cat("The data does not follow a multivariate normal distribution.\n")
}

```
## Conclusion
The analysis of the STAT2010 quiz "QUIZ4-STA2010" has provided valuable insights into the characteristics of bivariate normal distributions, visualizations, and statistical tests. 
