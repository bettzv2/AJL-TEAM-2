
# AJL-TEAM-2 Skin Disorder Detector



### **👥 Team Members**
| Ivette Adame-Castro | @bettzv2 | Began data loading, trained ResNet50, contributed to README file |

| Alexia Ventura | @alexiaventura | Tested ResNet, contributed to README file |

| Abdulaziz Khader | @aokhader | Researched data-upscaling, trained ResNet101, contributed to README file |

| Ava Gonick | @avagonick | Researched and performed data preparation, trained ResNet50 and ViT16, contributed to README file |

| Chris Taguba | @ectaguba | Researched models and dataset balancing, conducted data exploration, contributed to README file |

---

## **🎯 Project Highlights**

* Built a Visual Transformer by training the pretrained ViT16 model on the HAM1000 dataset and then fine-tuning on sample data to accurately detect skin cancers on different parts of the body for various skin types.
* Achieved an F1 score of 0.64623 and a ranking of 12/75 on the final Kaggle Leaderboard
* Implemented a learning rate scheduler and weight decay to optimize results within compute constraints

🔗 [Equitable AI for Dermatology | Kaggle Competition Page](https://www.kaggle.com/competitions/bttai-ajl-2025/overview)
🔗 [HAM1000 page](https://www.kaggle.com/datasets/kmader/skin-cancer-mnist-ham10000)

---

## **👩🏽‍💻 Setup & Execution**

To run the notebook, you have to either set it up on your local machine or use a cloud-based environment such as Google Colab.

To run on a cloud-based environment:
- Download the datasets and put them into your Google Drive account
- Run the notebook on your environment

To run on your local machine:
- Clone the repository using your preferred method of cloning. For example, if you wanted to clone the repo using the the HTTPS link, run:
  ```
  git clone https://github.com/bettzv2/AJL-TEAM-2.git
  ```
- Once you clone the repo to your local machine, you have to add the HAM 1000 and AJL datasets to your Google Drive or local file system.
  - If you chose to save the datasets on your local machine, change the dataset loading portion of the code to load the datasets from your local machine.
  - To do so, change the code portion that mounts your Google drive account and loads the dataset into the following snippet (assuming the files are in the same directory as the program):
  ```
  import os

  filepath = os.path.dirname(__file__)   # gets the directory of the current program
  hamdataset = ""
  ajldataset = ""

  hampath = os.path.join(filepath, hamdataset)
  ajlpath = os.path.join(filepath, ajldataset)
  ```
  - Now just change the paths when loading the dataset into *hampath* and *ajlpath*.

---

## **🏗️ Project Overview**

The Kaggle competition aimed to challenge us to solve real-world problems using machine learing. Specifically, it aimed at potentially solving the problem of being unable to diagnose darker-colored skin tones with skin cancer, which is a complex problem in the medical field. The Break Through Tech AI Program prepared us to face this challenge with all the necessary information we need to create an accurate and unbiased model. With the right model, we can potentially help doctors around the world with diagnosing skin cancers and speed up the treatment process, therefore decreasing the number of cancer-related sickness and deaths.

---

## 📊 Data Exploration

### Datasets Used
- **[HAM 1000](https://www.kaggle.com/datasets/kmader/skin-cancer-mnist-ham10000) Dataset:**  
  Used to pre-train the model on a similar sample size.

- **[AJL dataset](https://www.kaggle.com/competitions/bttai-ajl-2025/data) Dataset:**  
  The final dataset for model submissions.

### Data Exploration & Preprocessing
We conducted a concise analysis of key demographic and lesion attributes:

- **Demographics:**  
  Analyzed age, sex, and skin tone distributions. Preprocessing involved renaming columns and mapping abbreviated diagnostic labels (e.g., `akiec`, `bcc`) to full names.

- **Lesion Characteristics:**  
  Explored lesion locations and diagnosis confirmation methods (histopathology, follow-up, expert consensus, confocal microscopy).

- **Class Imbalance:**  
  Addressed the underrepresentation of skin cancers in darker skin tones using data augmentation, SMOTE, and HAM1000 pre-training.

### Visualizations

#### HAM1000 Dataset
- **Age Distribution:**  
  <img src="https://github.com/bettzv2/AJL-TEAM-2/blob/main/images/Age%20Distribution.png" width="500" />

- **Detailed Skin Tone Distribution:**  
  <img src="https://github.com/bettzv2/AJL-TEAM-2/blob/main/images/Detailed%20Skin%20Tone%20Distribution.png" width="500" />

- **Diagnosis Confirmation:**  
  <img src="https://github.com/bettzv2/AJL-TEAM-2/blob/main/images/Diagnosis%20Confirmation.png" width="500" />

- **Diagnosis Count:**  
  <img src="https://github.com/bettzv2/AJL-TEAM-2/blob/main/images/Diagnosis%20Count.png" width="500" />

- **Lesion Localization:**  
  <img src="https://github.com/bettzv2/AJL-TEAM-2/blob/main/images/Lesion%20Localization.png" width="500" />

- **Sex Distribution:**  
  <img src="https://github.com/bettzv2/AJL-TEAM-2/blob/main/images/Sex%20Distribution.png" width="500" />

#### Given Dataset
- **Skin Cancers Distribution:**  
  <img src="https://github.com/bettzv2/AJL-TEAM-2/blob/main/images/Skin%20Cancers%20Distribution.png" width="500" />

- **Skin Heatmap:**  
  <img src="https://github.com/bettzv2/AJL-TEAM-2/blob/main/images/Skin%20Cancers%20Distribution.png" width="500" />

- **Skin Tone Distribution:**  
  <img src="https://github.com/bettzv2/AJL-TEAM-2/blob/main/images/Skin%20Tone%20Distribution.png" width="500" />

### Challenges and Assumptions
- **Class Imbalance:**  
  Mitigated skewed lesion and skin tone distributions (fewer cancers on darker skin) using data augmentation, SMOTE, and HAM 1000 pre-training.
- **Data Consistency:**  
  Assumed uniform metadata across datasets for accurate diagnosis and confirmation mapping.
- **Interpretability:**  
  Improved clarity by renaming columns and converting codes to full descriptive labels.

---

## **🧠 Model Development**

Two different model approaches were used. One used a pretrained ResNet, and the other used a pretrained ViT16. 

### ResNet
We first started by developing a model based on a pretrained ResNet. We first began by fine-tuning just the last linear layer in a resNet18, resNet50, and resNet101. Out of these three, the resNet50 performed the best, so we decided to further optimize the resNet50. For this resNet50, we first pretrained layers 3 and 4 of the model on the HAM1000 dataset for 10 epochs. We then trained layer 4 of the model on the AJL dataset, using 80% of the dataset for training and 20% of the dataset for testing for 20 epochs. For this we used a learning rate of 1e^-4, a reduce on plateau learning rate scheduler with a patience of 2. As our optimizer, we used Adam, and for our Loss function, we used Cross Entropy Loss. For evaluation metrics, we used Validation accuracy and Validation f1 score. This resulted in a validation accuracy of 0.4783 and a validation F1 score of 0.4705. 

**Optimizing the ResNet50**

To achieve this accuracy for the ResNet50 we did some optimizations. First, we found that pretraining on the HAM1000 dataset, a dataset with images of skin lesions as well as labels, performed better than just training on the AJL dataset. We also experimented with the number of layers within the ResNet50 that we pretrained.


### Vit16
We then developed a model based on the ViT16. We started with a similar approach to the resNet50, where we pretrained the last half of the model on the HAM1000 dataset for 10 epochs, then trained the last two layers on the AJL dataset for 20 epochs. The AJL dataset was split into 80% training data and 20% validation data. For this we used a learning rate of 1e^-4, a reduce on plateau learning rate scheduler with a patience of 2. This model performed much better than the ResNet50 we had made, with a validation accuracy of 0.57 compared to a validation accuracy of 0.47 with the ResNet50. We then optimized this model. The final model we developed involved pretraining the entire ViT16 on the HAM10000 dataset and then fine-tuning the last 8 layers of the model on the AJL dataset. For the AJL dataset we used data augmentation. In particular, we used random crops of size 224, random horizontal flips, color jitter (which slightly changed the brightness, contrast, saturation, and hue of the data), random rotations up to 20 degrees, slight Gaussian blur, and slight elastic transformations. We used an Adam optimizer with an initial learning rate of 1e^-4 as well as weight decay of 5e^-5. We also used a reduce on plateau learning rate scheduler with a patience of 3 and a minimum learning rate of 1e^-7. This model gave us a validation accuracy of 0.6416 and a validation F1 score of 0.5841. On the private kaggle leaderboard it gave us an F1 score of 0.64623. 

**Optimizing the ViT16**

To optimize the ViT16, we tested with many different hyperparameters. We tried different learning rate schedulers, comparing the cosine annealing scheduler to the reduce on plate,u finding that the reduce on plateau scheduler did better. We tested with different amounts of weight decay as the model seemed to be initially overfitting. For this, we tried no weight decay and values of 1e^-4, 5e^-5, and 1e^-,5 finding that 5e^-5 did the best. Less resulted in more overfitting but more resulted in too much underfitting. We also tested around with the amount of the model that was trained on the AJL dataset. We tested training all the layers, the last 8, 6, 4, and 2 layers. We found that training on the last 8 layers did better with training on all of the layers, resulting in some overfitting, and training on fewer layers resulted in some underfitting. We also tested different amounts of data augmentation. We found that if we added in too much data augmentation, particularly adding too much color jitter made the model do worse. However, we also found that doing no data augmentation made the model do worse. 



---

## **📈 Results & Key Findings**

**Describe (as applicable):**

* Performance metrics (e.g., Kaggle Leaderboard score, F1-score)
* How your model performed overall
* How your model performed across different skin tones (AJL)
* Insights from evaluating model fairness (AJL)

With our final model, we ended up with an F1 score 0.64623 and a ranking of 12/75 on the Kaggle leaderboard. 

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
   - Balanced the Dataset – We used data augmentation techniques (such as rotation, flipping, and color normalization) to increase representation for underrepresented skin tones. We also used more data to train the model on identifying skin cancers regardless of the type, which allowed the model to identify more possible skin cancers.
3. What broader impact could your work have?
   - Improved Healthcare Accessibility – By ensuring diverse representation, the model can help dermatologists provide more accurate diagnoses across all skin tones.
   - The model can have a larger impact by also being trained for more skin conditions than just what was in this dataset, such as exxtremely rare skin conditions or skin conditions that look very similar to each other and need further diagnosis from other factors.

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
