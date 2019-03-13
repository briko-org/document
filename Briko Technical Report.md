# Corpus production workflow, workload estimation and rewarding mechanism for Briko blockchain community

Version:0.1 Draft @ March 7, 2019

## ——Content——

1. [Overview](#Overview)

2. [Phase 1-Text Corpus Review and Scoring](#phase-1---text-corpus-review-and-scoring)

   [Target Overview](#Target-Overview)

   [Key Notes for the Community Work](#Key-Notes-for-the-Community-Work)

   [Models and Procedures](#Models-and-Procedures)

   1. [Task Definition](#1-Task-Definition)

   2. [Machine Filtering](#2-Machine-Filtering-12)

   3. [Manual Reviewing and Scoring](#3-Manual-Reviewing-and-Scoring)

   4. [Machine Ranking and Sorting](#4-Machine-ranking-and-sorting)

   5. [Summary](#5-Summary)

   [Workload Estimation](#Workload-Estimation)

   [Reward System and Its Calculation](#Reward-System-and-Its-Calculation)

3. [Phase 2 & 3](#Phase-2--3)

   [Reference](#Reference)

## ——Overview——

This document describes the design of a Briko-initiated workflow to crowdsource high-quality text corpora from the general public. The workflow should be clear, modular, and the workload should be accurately quantifiable. The main modules include submission review and scoring, corpus revision and editing and new corpus composition. The target also includes designing a scoring system that evaluates the skill level of contributors, providing a total workload estimation model and developing a reward mechanism. The workflow of the text corpus processing is as shown below:

<img src="/img/overall_flow.png" width="480">

Following is the detailed workflow and modeling of each module.

## ——Phase 1 - Text Corpus Review and Scoring——

### **Target Overview**

This phase targets at designing a workflow to crowdsource, from the general public, the tasks of filtering an existing corpus or raw data crawled from the internet. The workflow includes a machine filtering process and a manual review process for which the raw data are provided by Briko. We also need to estimate the overall workload, design a scoring system that evaluates the contributors' skill level and design a reward mechanism for the contributors.  

### **Key Notes for the Community Work**

* The scoring system is designed based on community collaboration. It is used for estimating text corpus contributors’ skill level.
* Briko makes rules according to both the collaboration process and the target of task modules, the execution of which is overseen by the community.  
* Final scores are affected by the weight matrices of the participants.
* A reward is granted to users based on their weighted contribution calculated with parameters such as individual weight matrix and individual workload.
* The integrity of the scoring system is protected from malicious behaviors by challenging tasks as well as the dynamic weight matrices.
* Additional phases can be added to the process, for instance, corpus revision can be implemented to further improve the corpus quality.

### **Models and Procedures**

#### 1. Task Definition

No manual input is required during this step. Briko identifies a corpus filtering task, e.g., internet clawed data filtering or existing corpus filtering. The task is to acquire *k * P* amount of filtered data from the *P* raw input data, where *0 < k < 1*. While there are many types of text corpora, such as bilingual parallel corpus, corpus with sentimental tags, and question answering datasets, in this document, We use the bilingual parallel corpus as an example for the following discussions. The total workload is denoted as *W<sub>Phase1</sub>*, and the total budget is denoted as *BGE<sub>budget</sub>*.

#### 2. Machine Filtering [1][2]

No Manual input required within this step. Coarsely filtering of the dataset can be implemented, for example:

* The length ratio of corresponding data, Source (*S*) and Target (*T*), should stay within a certain range (such as *0.4 < S/T < 2.5*).
Specific tokens should appear simultaneously in both *S* and *T* (email, URL, large numbers, etc.).
* The Edit Distance of *S* and *T* must be greater than a specified value (small editing distances have a negative impact on the model training).
* The length of a sentence, denoted as *N<sub>Token</sub>*, must be within certain range (such as *2 < N<sub>Token</sub>< 80*).
* Use tools, such as Python langid package, to make sure that the dataset is of the target language type.
* (To be continued...)

We will get *P<sub>R</sub>* amount of corpus for the review process and *P-P<sub>R</sub>* amount of removed data. The main purpose of this step is to filter out corpus data which have little value to be improved and thus reduce the unnecessary community manual input.

#### 3. Manual Reviewing and Scoring

Filtered corpus data are distributed to R community users for review and *AR* number of users are involved in the review process(even distribution of workload is not mandatory). The options are 1-5 stars. The score from each user is noted as *Score<sub>n</sub>*, and individual weight parameter is denoted as *a<sub>R_n</sub>*:

* 5 stars: +5 points, no change required.
* 4 stars: +4 points, less than three-word change is required to be 5 stars.
* 3 stars: +3 points, more than three-word change is required, but no sentence order adjustment needed, nor does it contain any irrelevant component.
* 2 stars: +2 points, major modification required, or it contains irrelevant components.
* 1 star: +1 point, incorrect/irrelevant translation, re-work required.

<img src="/img/fig1.png" width="560">

The final score is the weighted average of the scores from *R* users, The final score, *Score*, has a range of [1, 5], and can be calculated as:

<img src="/img/eq1.png" height="70" align="middle">

Corpus data are ranked according to their scores.

The workload for an individual user to review one sentence is denoted as *W<sub>n</sub>*, and the total workload in a task is *∑W<sub>n</sub>*, and therefore, the overall workload for this task is <img src="/img/eq2.png" height="40" align="middle">, and we have *W<sub>Phase1</sub>* = <img src="/img/eq2.png" height="40" align="middle">. We also need to include randomly distributed challenge task, with a total workload of *W<sub>CR</sub>*, to protect the result from the malicious scoring attempts, *W<sub>CR</sub>* is included in *W<sub>Phase1</sub>*, and equals approximately 5% of the *W<sub>Phase1</sub>* (TBD).

The range of the weight parameter *a<sub>R_n</sub>* is *0.8 ≤ a<sub>R_n</sub> ≤ 1.2*, the initial value of each contributor depends on his/her completion of the beginner tasks, and is calculated as follows:

The standard deviation of user’s score, *Score<sub>n</sub>*, from the final score, *Score* is defined as error, *x*, which reflects the individual user’s skill level. Lower the *x* is, higher the quality of the user’s score is. Map *x* as a normal distribution over the interval [0.8, 1.2] (*x=0* is mapped as 1.2) with a mean of 1 to calculate for the individual weight parameter *a<sub>R_n</sub>*. The distribution function and parameters can be adjusted according to the income distribution of the community. *X* remains unchanged for correctly answering the challenge task, while increases by 0.05 if the answer was incorrect.

#### 4. Machine Ranking and Sorting

No manual input required during this step. The corpus data are sorted by their final scores, and the top *k * P* amount will be kept, the process is as illustrated in the following figure.

<img src="/img/fig2.png" width="560">

If higher quality corpus dataset is required, the data close to the cut-off line can be passed onto phase 2 for review and revision. Detailed process can be found in Chapter - Phase 2.

#### 5. Summary

A simplified corpus filtering process is as shown below:

<img src="/img/fig3.png" width="560">

If the revision and re-make of the corpus are required, the process can move to phase 2 or 3. The details will be released in the future.

### **Workload Estimation**

In a parallel corpus filtering task of *P<sub>R</sub>* sentences:

* Each sentence is reviewed and scored by *R* users, the total amount of reviews required is *R * P<sub>R</sub>*, and there are *AR* numbers of users involved.
* The workload for reviewing and scoring one sentence is *W<sub>n</sub>* and *W<sub>n</sub>* varies depending on the specifics of the task. 
* Challenge tasks with a total workload of *W<sub>CR</sub>* is introduced.

Therefore, the total workload of a task can be calculated as:

<img src="/img/eq3.png" height="55" align="middle">

The total budget *BGE<sub>budget</sub>* is proportional to the total workload *W<sub>Phase1</sub>*. One Briko Granted Endorsement (BGE) is set temporarily equivalent to the payout of one minute workload.

### **Reward System and Its Calculation**

The basic rule of the reward system is that the members with quality and frequent submissions receive more rewards under the same circumstances.  

Community members receive BGE rewards for completing corpus filtering tasks, and the total number is denoted as *BGE<sub>pay</sub>*. The total budget is *BGE<sub>budget</sub>* when defining a task. *BGE<sub>res</sub>* is the reserved amount for the platform (for supplementary tasks, newcomer rewards, etc.), and *BGE<sub>fine</sub>* is the amount of the confiscated deposit withheld by the platform. Therefore, the estimated total payout is  *BGE<sub>pay</sub> = BGE<sub>budget</sub> - BGE<sub>res</sub>*, and the actual payout is *BGE<sub>paid</sub> = BGE<sub>budget</sub> - BGE<sub>res</sub> - BGE<sub>fine</sub>*. The reward of a member is calculated based on their weighted workload:

<img src="/img/eq4.png" height="50" align="middle">

We will also introduce a parameter related to the overall workload in the future design so that productive members obtain more rewards under the same circumstances.

To discourage malicious behaviors, the deposit is set to be 1.5 times the value of the daily task package. The tasks are sent back to our server after the reviewing and scoring, the scoring error is then be calculated for this specific package (not the overall error parameter *x*). If the error is more than 1.5 points, the submission is considered unsuccessful, and the deposit should not be refunded consequently. Since the deposit is more than the reward of this package, malicious behaviors would eventually result in a negative value net income. These task packages reviewed by malicious users, once determined, are set to be redistributed to other users in the following rounds.

Briko will publicly repurchase issued BGE through the secondary market with future income from our text corpora and computing services, and community members are free to trade their BGE to fiat or other digital currencies.

## ——Phase 2 & 3——
(Ongoing work...)

## Reference

[1] Jun Lu  and  Xiaoyu Lv  and  Yangbin Shi  and  Boing Chen, “Alibaba Submission to the WMT18 Parallel Corpus Filtering Task”, WMT18, 2018.

[2] Marcin Junczys-Dowmunt, “Dual Conditional Cross-Entropy Filtering of Noisy Parallel Corpora”, WMT18, 2018.
