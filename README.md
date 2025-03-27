
# GitHub Kaggle Project AJL-TEAM-2



### **👥 Team Members**
| Ivette Adame-Castro | @bettzv2 | Began data loading, trained ResNet50, contributed to README file |

| Alexia Ventura | @alexiaventura | Tested ResNet, contributed to README file |

| Abdulaziz Khader | @aokhader | Researched data-upscaling, Trained ResNet101, contributed to README file |

| Ava Gonick | (Fill in GitHub name) | (Top 3 tasks you completed) |

---

## **🎯 Project Highlights**

**Example:**

* Built a Visual Transformer by pretraining it on sample data to accurately detect skin cancers on different parts of the body for various skin types.
* Achieved an F1 score of 0.64623 and a ranking of 12/75 on the final Kaggle Leaderboard
* Implemented a learning rate scheduler and weight decay to optimize results within compute constraints

🔗 [Equitable AI for Dermatology | Kaggle Competition Page](https://www.kaggle.com/competitions/bttai-ajl-2025/overview)

---

## **👩🏽‍💻 Setup & Execution**

**Provide step-by-step instructions so someone else can run your code and reproduce your results. Depending on your setup, include:**

* How to clone the repository
* How to install dependencies
* How to set up the environment
* How to access the dataset(s)
* How to run the notebook or scripts

---

## **🏗️ Project Overview**

**Describe:**

* The Kaggle competition and its connection to the Break Through Tech AI Program
* The objective of the challenge
* The real-world significance of the problem and the potential impact of your work

---

## **📊 Data Exploration**

**Describe:**

* The dataset(s) used (i.e., the data provided in Kaggle \+ any additional sources)
* Data exploration and preprocessing approaches
* Challenges and assumptions when working with the dataset(s)

- We used the HAM 1000 dataset to pre-train the model on a smaller sample size: ![HAM 1000](https://www.kaggle.com/datasets/kmader/skin-cancer-mnist-ham10000)
- Then we used the main dataset to train the model: ![AJL dataset](https://www.kaggle.com/competitions/bttai-ajl-2025/data)

**Potential visualizations to include:**

* Plots, charts, heatmaps, feature visualizations, sample dataset images

---

## **🧠 Model Development**

**Describe (as applicable):**

* Model(s) used (e.g., CNN with transfer learning, regression models)
* Feature selection and Hyperparameter tuning strategies
* Training setup (e.g., % of data for training/validation, evaluation metric, baseline performance)

---

## **📈 Results & Key Findings**

**Describe (as applicable):**

* Performance metrics (e.g., Kaggle Leaderboard score, F1-score)
* How your model performed overall
* How your model performed across different skin tones (AJL)
* Insights from evaluating model fairness (AJL)

**Potential visualizations to include:**

* Confusion matrix, precision-recall curve, feature importance plot, prediction distribution, outputs from fairness or explainability tools

---

## **🖼️ Impact Narrative**

**Answer the relevant questions below based on your competition:**

**AJL challenge:**

As Dr. Randi mentioned in her challenge overview, “Through poetry, art, and storytelling, you can reach others who might not know enough to understand what’s happening with the machine learning model or data visualizations, but might still be heavily impacted by this kind of work.”
As you answer the questions below, consider using not only text, but also illustrations, annotated visualizations, poetry, or other creative techniques to make your work accessible to a wider audience.
Check out [this guide](https://drive.google.com/file/d/1kYKaVNR\_l7Abx2kebs3AdDi6TlPviC3q/view) from the Algorithmic Justice League for inspiration!

1. What steps did you take to address [model fairness](https://haas.berkeley.edu/wp-content/uploads/What-is-fairness_-EGAL2.pdf)? (e.g., leveraging data augmentation techniques to account for training dataset imbalances; using a validation set to assess model performance across different skin tones)
   - Balanced the Dataset – We used data augmentation techniques (such as rotation, flipping, and color normalization) to increase representation for underrepresented skin tones.
3. What broader impact could your work have?
   - Improved Healthcare Accessibility – By ensuring diverse representation, the model can help dermatologists provide more accurate diagnoses across all skin tones.
   - 

All images given in the dataset were used in the training, so no data in this dataset was excluded based on skin condition, skin color, and other factors. Techniques such as data augmentation and SMOTE were also used to account for imbalances. This work can have a broader impact by also being trained for more skin conditions than just what was in this dataset, such as exxtremely rare skin conditions or skin conditions that look very similar to each other and need further diagnosis from other factors.

---

## **🚀 Next Steps & Future Improvements**

**Address the following:**

* What are some of the limitations of your model?
* What would you do differently with more time/resources?
* What additional datasets or techniques would you explore?

With ResNet in particular, the accuracy scores weren't as high as the ResNet value got larger, so it limited usage of that technique. Additionally, there were some issues with getting specific ResNet values to work based on importing the tools, which also limited which ResNet values could be used for testing. With more time and resources, we would have tried other data techniques to keep seeing if we could improve the accuracy score, or used a combination of models as filters to get a better result.
---

## **📄 References & Additional Resources**

* Cite any relevant papers, articles, or tools used in your project

---
