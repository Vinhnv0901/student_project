<h1 align="center">Course Recommendation for University Environments</h1>

##1. dataset.
###1.1. statistic dataset.
  data set is collected from row data of university of information technology from 2013 to 2016
  in the data set includes 96269 registration lines from 4049 students and 10 faculties managing subjects.
###1.1.2. split train and test data.
* Divide the number of random students in the ratio 8:2 as train and test, respectively.
* In which test data only takes data from 2013 to 2015. The reason is because 2 periods of 2016 will be used for prediction.
* In the data there will be freshmen of the first semester of 2016 so there is no previous score data so it will be remove.
##2. Model
###2.1. Course Recommendation model base on enroll and grade
* apply the model of the paper [Course Recommendation](https://educationaldatamining.org/files/conferences/EDM2020/papers/paper_90.pdf)
* Model predicting and counting student registrations and score data to evaluate 3 Score.
  ![Top 10 popular Subjects](/image/Top10_popular_subject.png)
###2.1.1. Interest Score.
* We will be based on the number of subjects registered by each faculty of a student:
  ![P](/image/p.svg)
* Use P to calculate the similarity between 2 students using cosine:
  ![sim1](/image/sim_IS1.svg)
* In order to prioritize students with the same faculty, we will have lamda weight to calculate the similarity. **Samemajor()** is equal to 1 when 2 students have the same faculty and 0 when different faculties.
  ![sim2](/image/sim_IS2.svg)
* The final formula for assessing a student's interest in a subject:
  ![IS](/image/IS.svg)

###2.1.2.	Timing and popularity based  Score.

* The choice of subjects depending on each period is also very important. Which semester is more suitable for taking this course?
  ![Tt](/image/Tt.svg)
* Which courses are popular now?
  ![Tp](/image/Tp.svg)
* Combining the above two formulas, we will have a formula to evaluate the appropriateness of a subject for a semester:
  ![TS](/image/TS.svg)

###2.1.3. Grade-based Score.
* Many students will decide to take high-scoring subjects to improve their Grade Point Average (GPA). So we will predict the grade and assess how the grade of that subject will be. We will use the subjects that the student studied and the average score of that student to calculate the similarity between the two students.
  ![Sim_grade](/image/sim_grade.svg) 
* Then we can predict what the score of student s and subject c will be?
  ![grade](/image/grade.svg)
* Finally, we will normalize it using the formula:
  ![grade](/image/nomalize_grade.svg)
###2.1.4 Combine three Score.
* After getting 3 scores we will combine them with the formula:
  ![grade](/image/Score.svg)
* In which, those three weights to evaluate the influence of each Score.
##3. Evaluation
###3.1. Course Recommendation model.
* We will run the above weights from 0 to 1 with a step size 0.05 in the test set to evaluate which set of weights is the best. We evaluate based on **recall**, **precision**, **f1-score**.
* We have trend of alpha like that:
  ![alpha](/image/alpha.png)
* We have trend of beta like that:
  ![beta](/image/beta.png) 
* We have trend of gamma like that:
  ![gamma](/image/gama.png) 
*We have the set(alpha, beta, gamma) with top 10 highest F1-Score:
  ![f1](/image/f1.png) 

* From the above results, we can see that Score grade is not as highly rated as the other 2 Scores. Because the subjects have changed over the years in many aspects. For example, faculties and departments can remove unessential subjects or add subjects in the program in university. Therefore, about the train data, we have not got the uniformity and generality. This greatly affects the calculation of similarity among students.
#4. Reference.

* [Course Recommendation for University Environments](https://educationaldatamining.org/files/conferences/EDM2020/papers/paper_90.pdf)
* [A Score Prediction Approach for Optional Course Recommendation via Cross-User-Domain Collaborative Filtering](https://ieeexplore.ieee.org/abstract/document/8636939)