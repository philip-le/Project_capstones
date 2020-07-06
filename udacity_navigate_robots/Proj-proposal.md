# Machine Learning Engineer Nanodegree
## Capstone Proposal
Hoang Phuoc Le

July 4th, 2020

## Proposal: Detecting floor surface for an autonomous Robot Indoor Navigation

### Domain Background
<!-- _(approx. 1-2 paragraphs) -->

Autonomous robots, just like humans, should have the ability to make their own decisions and then act accordingly. An autonomous robot is one that can perceive its environment, make decisions based on what it perceives, and then actuate a movement. For an autonomous robot to navigate a task or go on a journey, it will need the input of its surrounding environment. One of the traditional problems in robotic navigation is to recognize the surface it passed by.

The project is inspired by the Kaggle CareerCon 2019 - Help Navigate Robots. There are several other papers [[1]](#1), [[2]](#2), which you can find in the reference list.

<!-- In this section, provide brief details on the background information of the domain from which the project is proposed. Historical information relevant to the project should be included. It should be clear how or why a problem in the domain can or should be solved. Related academic research should be appropriately cited in this section, including why that research is relevant. Additionally, a discussion of your personal motivation for investigating a particular problem in the domain is encouraged but not required. -->


<img src="./data/sensor.jpeg" width="250" height="300">

### Problem Statement
<!-- _(approx. 1 paragraph)_ -->

In this project, a robot is arranged to travel through different floor surfaces. It is attached with an Inertial Measurement Units (IMU sensors) for data collection. The aim of our task is to build a classification model and predict the type of surface based on the new input sensor data. The output will be uploaded to Kaggle for the scoring feedback.

<!-- In this section, clearly describe the problem that is to be solved. The problem described should be well defined and should have at least one relevant potential solution. Additionally, describe the problem thoroughly such that it is clear that the problem is quantifiable (the problem can be expressed in mathematical or logical terms) , measurable (the problem can be measured by some metric and clearly observed), and replicable (the problem can be reproduced and occurs more than once). -->

### Datasets and Inputs
<!-- _(approx. 2-3 paragraphs) -->

The dataset locates in the Kaggle platform, which has been collected by researchers from Tampere University, Finland.

The IMU sensor data is the combination of accelerometer data, gyroscope data (angular rate) and internally estimated orientation. In particular:

    - Orientation: encode the current angles how the robot is oriented as a quaternion, including 4 attitude quaternion channels, 3 for vector part and one for scalar part;
    - Angular rate: describes the angle and speed of motion, including 3 channels, corresponding to the 3 orthogonal IMU coordinate axes X, Y, and Z;
    - Acceleration: describe how the speed is changing at different times, including 3 channels, specific force corresponding to 3 orthogonal IMU coordinate axes X, Y, and Z.

The input data, covering 10 sensor channels and 128 measurements per time series plus three ID columns:

    - row_id: The ID for this row.
    - series_id: ID number for the measurement series. Foreign key to y_train/sample_submission.
    - measurement_number: Measurement number within the series.


<!-- In this section, the dataset(s) and/or input(s) being considered for the project should be thoroughly described, such as how they relate to the problem and why they should be used. Information such as how the dataset or input is (was) obtained, and the characteristics of the dataset or input, should be included with relevant references and citations as necessary It should be clear how the dataset(s) or input(s) will be used in the project and whether their use is appropriate given the context of the problem. -->

### Solution Statement
<!-- _(approx. 1 paragraph)_ -->

We plan to build several methods and compared with each other to select the best approach for the problem.
One of the traditional approach is to apply feature engineering and create a set of features (statistics and Fast Fourier Transform) for each series (10 sensor channels and 128 measurements). Afterwards, we can apply algorithms like Random Forest or Gradient Boosting for building a classification model.

Another approach will be to apply Recurrent Neural Network with LSTM for timeseries data or Conv-1d to train the raw data and build a deep learning model for the task.

<!-- In this section, clearly describe a solution to the problem. The solution should be applicable to the project domain and appropriate for the dataset(s) or input(s) given. Additionally, describe the solution thoroughly such that it is clear that the solution is quantifiable (the solution can be expressed in mathematical or logical terms) , measurable (the solution can be measured by some metric and clearly observed), and replicable (the solution can be reproduced and occurs more than once). -->

### Benchmark Model
<!-- _(approximately 1-2 paragraphs)_ -->

The paper of F. Lomio et al.(2019)[[3]](#3) gives us the baseline, which achieves an
accuracy of over 68% with the nine-category dataset. The high result of Kaggle competition output (more than 95%)  was due to the data leak of Orientation input, which will not be feasible in practice. Therefore we will only utilize the right features to build the model and compare with the formal benchmark.


<!-- In this section, provide the details for a benchmark model or result that relates to the domain, problem statement, and intended solution. Ideally, the benchmark model or result contextualizes existing methods or known information in the domain and problem given, which could then be objectively compared to the solution. Describe how the benchmark model or result is measurable (can be measured by some metric and clearly observed) with thorough detail. -->

### Evaluation Metrics
<!-- _(approx. 1-2 paragraphs)_ -->

The Multiclass Accuracy, which is the average number of observations with the correct label for all the categories, will be used as the evaluation metrics. However, we will also compute the satisficing metric of Area Under the ROC Curve (AUC) to further understand the problem.

<!-- In this section, propose at least one evaluation metric that can be used to quantify the performance of both the benchmark model and the solution model. The evaluation metric(s) you propose should be appropriate given the context of the data, the problem statement, and the intended solution. Describe how the evaluation metric(s) are derived and provide an example of their mathematical representations (if applicable). Complex evaluation metrics should be clearly defined and quantifiable (can be expressed in mathematical or logical terms). -->

### Project Design
<!-- _(approx. 1 page)_ -->

Machine learning project is quite highly iterative in general; as we progress through the ML lifecycle, we'll need to iterate on a section until reaching a satisfactory level of performance, then proceeding forward to the next task (which may be circling back to an even earlier step). However, we will approach the project using the pipeline as follows:

    - Gathering data (Kaggle platform)
    - Data pre-processing (cleaning and featuring engineering)
    - Researching the model that will be best for the type of data (Random Forest, Boosting or Deep Learning models)
    - Training and testing the model
    - Evaluation

To improve the model we might also tune the hyper-parameters of the model and maximize the accuracy.




<!-- 
In this final section, summarize a theoretical workflow for approaching a solution given the problem. Provide thorough discussion for what strategies you may consider employing, what analysis of the data might be required before being used, or which algorithms will be considered for your implementation. The workflow and discussion that you provide should align with the qualities of the previous sections. Additionally, you are encouraged to include small visualizations, pseudocode, or diagrams to aid in describing the project design, but it is not required. The discussion should clearly outline your intended workflow of the capstone project. -->

-----------

<!-- **Before submitting your proposal, ask yourself. . .**

- Does the proposal you have written follow a well-organized structure similar to that of the project template?
- Is each section (particularly **Solution Statement** and **Project Design**) written in a clear, concise and specific fashion? Are there any ambiguous terms or phrases that need clarification?
- Would the intended audience of your project be able to understand your proposal?
- Have you properly proofread your proposal to assure there are minimal grammatical and spelling mistakes?
- Are all the resources used for this project correctly cited and referenced? -->

### References:
<a id="1">[1]</a> Lauro Ojeda, Johann Borenstein, Gary Witus, and Robert Karlsen.
Terrain characterization and classification with a mobile robot. Journal
of Field Robotics, 23(2):103–122, 2006

<a id="2">[2]</a> Terrain traversability analysis methods for unmanned ground vehicles: A survey
P Papadakis - Engineering Applications of Artificial Intelligence, 2013 - Elsevier

<a id="3">[3]</a> Surface Type Classification for Autonomous Robot Indoor Navigation
Francesco Lomio, et al. - arXiv, 2019 - https://arxiv.org/abs/1905.00252

<a id="4">[4]</a> Kaggle - CareerCon 2019 - Help Navigate Robots https://www.kaggle.com/c/career-con-2019/
