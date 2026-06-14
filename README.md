Դասընթաց: Մեքենայական Ուսուցում (Machine Learning)
Խնդրի տեսակ: Binary Classification
Dataset: Telco Customer Churn (IBM Sample Dataset)
Dataset link: https://raw.githubusercontent.com/IBM/telco-customer-churn-on-icp4d/master/data/Telco-Customer-Churn.csv
Խնդրի նկարագրություն
Նպատակն է կանխատեսել՝ հաճախորդը կհեռանա ընկերությունից (Churn = Yes/1) թե կմնա (Churn = No/0)՝ հիմնվելով նրա դեմոգրաֆիկ, account-ի, և ծառայությունների տվյալների վրա։
Սա Binary Classification խնդիր է, որտեղ input-ը հաճախորդի բնութագրիչներն են, output-ը՝ 0 կամ 1 (կմնա/կհեռանա)։

Dataset-ի նկարագրություն

Տողերի քանակ7,043 հաճախորդ
Սյունակների քանակ21 (20 feature + 1 target)
TargetChurn (Yes / No)
Class balance~73% No / ~27% Yes (մի փոքր imbalanced)

Feature-ների խմբեր:
Դեմոգրաֆիկ: gender, SeniorCitizen, Partner, Dependents
Account/Billing: tenure, Contract, PaperlessBilling, PaymentMethod, MonthlyCharges, TotalCharges
Ծառայություններ: PhoneService, MultipleLines, InternetService, OnlineSecurity, TechSupport, StreamingTV, StreamingMovies

Կիրառված մոդելներ և արդյունքներ

Նույն dataset-ի վրա կիրառեցինք 5 տարբեր classification ալգորիթմ.

Մոդել               Accuracy   Precision  Recall   F1      ROC-AUC
Logistic Regression 0.738       0.765     0.847   0.804    0.780
SVM (RBF)           0.715       0.742     0.842   0.789   0.757
Random Forest       0.707       0.742     0.824   0.781   0.747
Decision Tree       0.695       0.731     0.821   0.773   0.708 
KNN                 0.695       0.718     0.853   0.780   0.688

Արդյունքների վերլուծություն

Լավագույն մոդել — Logistic Regression (ROC-AUC = 0.780)

Logistic Regression-ը ցույց տվեց լավագույն արդյունք, քանի որ dataset-ում feature-ների և target-ի կապը հիմնականում linear/additive է (հատկապես one-hot encoded categorical features-ի դեպքում)։

Ինչու KNN-ը ամենավատն էր:
One-hot encoding-ից հետո feature-ների թիվը մեծ է (sparse, high-dimensional space)։ KNN-ը distance-based մոդել է, և high-dimensional տարածությունում distance-ը կորցնում է իմաստը (curse of dimensionality)։

Preprocessing քայլեր
Missing values — TotalCharges-ի դատarky արժեքները լրացվեցին median-ով
Drop — customerID հանվեց (ոչ-ինֆoрматив)
Feature Engineering — 5 նոր feature ստեղծվեց
Target Encoding — Churn: Yes→1, No→0
One-Hot Encoding — բոլոր categorical feature-ները վերածվեցին 0/1 սյունակների
Train/Test Split — 80%/20%, stratified
StandardScaler — feature-ները բերվեցին mean=0, std=1
