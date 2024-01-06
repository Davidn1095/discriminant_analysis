# discriminant_analysis

# Load Data
datos <- read.table("discriminante.txt", header = TRUE)
attach(datos)
# Display the Data
datos

# Perform Linear Discriminant Analysis (LDA)
discrimi <- lda(discriminante ~ X1 + X2 + X3 + X4 + X5 + X6 + X7 + X8 + X9 + X10 + X11 + X12 + X13, 
                prior = c(0.33, 0.33, 0.34), method = "moment", tol = 0.001)
# Display Singular Values from LDA Model
discrimi$svd

# Create New Data for Prediction
Datos2 <- rbind(
    c(5.6, 4.2, 15.8, 1.7, 0.17, 1.6, 2.3, 6.0, 4.0, 5.27, 0.14, 216.25, 26.66),
    c(5.45, 3.09, 17.82, 1.56, 0.14, 1.62, 1.97, 5.21, 2.68, 7.45, 0.15, 285.71, 23.42)
)
Datos21 <- data.frame(Datos2)
# Make Predictions with New Data
discrimi2 <- predict(discrimi, newdata = Datos21, prior = discrimi$prior, 2)
# Display Predictions
discrimi2

# Comparing Predicted and Actual Classes
table(predict(discrimi)$class, discriminante)

# Plotting the LDA Model
plot(discrimi)

# Generate Pairwise Scatter Plots of the Linear Discriminants
pairs(discrimi)

