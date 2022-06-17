# ML1_AFLW2000_HeadPoseEstimation
This work is done with collaboration of my colleague and my friend: **Abdelrhman Amr**

# Description

This project is developed using 68 landmarks of face to estimate 3 angle rotation, **yaw**, **pitch**, **roll.** 

The model uses Dlib along side with model trained on **AFLW2000_3D** dataset
![image](https://user-images.githubusercontent.com/54750418/174401818-c7139533-09f6-497a-9394-98ff5a80988e.png)


# Data Preprocessing

After reading the data 

1. Normalization of all the landmarks to one referenced landmark.
    
    ![image](https://user-images.githubusercontent.com/54750418/174401870-722df03f-03ad-4a23-8097-520a1fc1c535.png)
    
    - Using the sparse representation of the normalized coordinates in this [paper](https://github.com/Abdelrhman-Amr-98/Head-Pose-Estimation/blob/main/Sources%20and%20References/%5B1%5D%20Sparse_Bayesian_Regression_for_Head_Pose_Estimation.pdf) outline **3.1**
    - Given that we have the nose landmark [**31**] performing as the CG feature of the face
        - We have used it instead of the approximation performed in the paper to estimate its position
        - Then we applied the normalization method using the nose as our CG.
2. Feature Selection
3. Using the Interquartile Rule to Find Outliers in both (**labels** and **landmarks**)
    - Calculate the interquartile range for the data. **Multiply the interquartile range (IQR) by 1.5**
     (a constant used to discern outliers). Add 1.5 x (IQR) to the third quartile. Any number greater than this is a suspected outlier.
4. Normalization of all selected features from [0, 1]

# Model

1. Dividing data using `train_test_split` from `sklearn.model_selection`
    - Training: **60%**
    - Validation: **20%**
    - Testing: **20%**
2. **Histogram** plot of all training, validation and testing data to make sure they all follow a **gaussian distribution**.
3. **Training** using six models:
    - Linear Regression
    - Decision tree Regressor
    - Support vector Regression (SVR)
        - Grid Search
    - RandomForestRegressor
    - GradientBoostingRegressor
    - AdaBoostRegressor

### Model Performance and **Landmarks**

- **Pitch**: **12** landmarks were used
    - R2-score for testing data: **92.12% (SVR using Grid Search)**
- **Yaw: 5** landmarks were used
    - R2-score for testing data: **99.35% (Random Forest)**
- **Roll: 5** landmarks were used
    - R2-score for testing data: **93.28% (SVR using Grid Search)**

# Evaluation Metrices

- R2 Score
- Mean Absolute Error (MAE)
- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- Mean Absolute Percentage Error (MAPE)
- Explained Variance Score
- Max Error
- Median Absolute Error

# Video Trial

[https://drive.google.com/file/d/1-QBsdB9aymuR-JAm5MSdUS7_PQRX7tCf/view?usp=sharing](https://drive.google.com/file/d/1-QBsdB9aymuR-JAm5MSdUS7_PQRX7tCf/view?usp=sharing)

# References

- Main paper:  [Sparse Bayesian Regression for Head Pose Estimation](https://github.com/DinaZakaria/ML1_AFLW2000_HeadPoseEstimation/blob/master/Papers/Sparse_Bayesian_Regression_for_Head_Pose_Estimatio.pdf)
