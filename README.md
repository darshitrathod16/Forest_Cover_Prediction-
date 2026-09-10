# Forest Cover Type Prediction

This project predicts the type of forest cover on a piece of land using cartographic data, based on data collected by the US Forest Service. It was done as part of my data science internship project (PRCP-1005).

## Problem Statement

Forest cover type is normally identified through field surveys or satellite imagery, which takes time and effort. The goal here is to build a model that can predict the forest cover type of a land patch using only terrain and environmental measurements, no direct observation needed.

## Dataset

The dataset has 15,120 records from four wilderness areas in Roosevelt National Forest, Colorado. It includes terrain features like elevation, slope, and aspect, distance based features like distance to water and roads, sunlight exposure at different times of day, and categorical data on wilderness area and soil type. The target, Cover_Type, has 7 classes and is perfectly balanced.

## What I did

- Checked the data for missing values, duplicates, and zero-variance columns (found two soil types that never appear in the dataset at all)
- Did EDA across univariate, bivariate, and multivariate levels to see which features actually separate the cover types
- Found that Elevation, Wilderness_Area, and several soil types were strong predictors, while Aspect and Hillshade looked weak on their own
- Dropped the Id column and the two zero-variance soil types before modeling
- No scaling or encoding was needed, since the data was already numeric and one-hot encoded from the source
- Trained and compared 4 ensemble models: Random Forest, Extra Trees, Gradient Boosting, and AdaBoost
- Tuned Random Forest and Extra Trees using RandomizedSearchCV
- Checked feature importance to see if it matched what EDA had already suggested

## Results

Extra Trees (Tuned) gave the best overall performance, so it was picked as the final model. It scored 85.78% accuracy, a macro F1-score of 0.8556, and ROC-AUC of 0.9832 on the test data. Random Forest was very close behind. AdaBoost performed poorly (36% accuracy), mainly because its default weak learner couldn't handle the complexity of this dataset.

The most useful feature by far was Elevation, followed by distance to roadways, distance to fire points, and Wilderness_Area4.

## Key takeaway

Elevation alone tells you a lot about what grows on a piece of land, which makes sense since different tree species survive in different climate zones. Soil type and wilderness area also matter a lot, some soil types were found to belong to a single cover type over 90% of the time.

## Tools used

Python, Pandas, Matplotlib, Seaborn, Scikit-learn

## Files

- `Forest_Cover_Pred.ipynb` - full notebook with EDA, feature engineering, modeling, and conclusion
- `forest_cover_extra_trees_tuned.pkl` - saved final model
