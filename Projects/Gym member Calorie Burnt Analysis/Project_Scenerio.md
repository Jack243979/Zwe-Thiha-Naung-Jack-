# Project Scenario

A Gym operator would like to analyse the fitness patterns and performance across diverse gym experience levels. The dataset provides a detailed overview of gym members' exercise routines, physical attributes, and fitness metrics. It contains 4000+ samples of gym data, including key performance indicators such as heart rate, calories burned, and workout duration. Each entry also includes demographic data and experience levels, allowing for comprehensive analysis of fitness patterns, athlete progression, and health trends.

## Objective
Analyze relationships between demographic/physiological factors and **Calories_Burned**, and build predictive models to understand which features most influence the target.

## Key Features
- **Age**: Age of the gym member.
- **Gender**: Gender of the gym member (Male or Female).
- **Weight (kg)**: Member’s weight in kilograms.
- **Height (m)**: Member’s height in meters.
- **Max_BPM**: Maximum heart rate (beats per minute) during workout sessions.
- **Avg_BPM**: Average heart rate during workout sessions.
- **Resting_BPM**: Heart rate at rest before workout.
- **Session_Duration (hours)**: Duration of each workout session in hours.
- **Calories_Burned** *(Target)*: Total calories burned during each session.
- **Workout_Type**: Type of workout performed (e.g., Cardio, Strength, Yoga, HIIT).
- **Fat_Percentage**: Body fat percentage of the member.
- **Water_Intake (liters)**: Daily water intake during workouts.
- **Workout_Frequency (days/week)**: Number of workout sessions per week.
- **Experience_Level**: Level of experience, from beginner (1) to expert (3).
- **BMI**: Body Mass Index, calculated from height and weight.

## Modeling Scope
- Algorithms: Linear Regression, Decision Tree, Random Forest, Gradient Boosting
- Dataset variants: Encoded vs Non-encoded categoricals
- Splits: 60/40 and 70/30 (fixed random seed for reproducibility)
- Metrics: ASE (MSE), RMSE

## Deliverables
- Cleaned dataset(s) and partition settings
- SAS Viya model configurations and screenshots
- Model comparison tables and interpretation (feature importance, encoding impact)
- Recommendations for **prediction-focused** vs **interpretability-focused** use cases
