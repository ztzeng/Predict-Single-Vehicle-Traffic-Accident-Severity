# Predict Single-Vehicle Traffic Accident Severity with Machine Learning using Apache Spark

Open Database: 
https://www.kaggle.com/tsiaras/uk-road-safety-accidents-and-vehicles

While traffic accidents have declined globally over the past few decades, they
remain the leading cause of death for young adults and injure tens of millions of people
every year. 

From an economic standpoint, the United Kingdom Department of Transport (DofT) estimated the cost of all traffic accidents to be about £36 billion ($46.7 billion) per year.

The motivation for this project is to understand the factors that contribute to accidents and use machine learning to predict accident severity level: slight, severe, and fatal. 

In this project, we used AWS S3 to store the data, then launched 10 AWS EC2(with replicated shards) to import data from S3 into MongoDB. 
Lastly, we launched an AWS EMR to query data and do SparkML on the data.
![Alt text](/overview.jpg?raw=true "Optional Title")


For the SparkML part, due to the following reasons, we built tree-based models and chose F1-score as the primary metric, recall
as the optimizing metric:

1) data is high-dimensional 
2) labels suffer from imbalance (slight, severe, and fatal)
3) algorithm can be integrated into a distributed computing framework

Ultimately, Random Forest was chosen as the final model because it performed the best on Recall for fatal, our optimizing metric. 
Processing speed was not a determining factor because all the models ran in a reasonable amount of time.

Also, the top 5 most important features for predicting accident severity were: Speed Limit, Vehicle maneuver, Junction detail, Police force district, 
Vehicle location. Concrete actions (such as turning, passing a car, moving through an
intersection, or entering a zone with a different speed limit) proved to be more important
than characteristics regarding identity (e.g. driver sex). A simple effort to educate people
about safe driving practices could be a worthwhile use of time. The junction detail
statistics could also provide some guidance for improved road layout designs.

The project has its flaws. For further study, we can do more feature engineering and hyperparameter tuning for adjustment. Also,
the output has high variance. Potentially, we can gather more features, combine this dataset with other information, and improve the predict power.
