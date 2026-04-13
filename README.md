# ml_assn1 - House Prices - Advanced Regression Techniques

კონკურსის მიზანია Ames-ში საცხოვრებელი სახლების გასაყიდი ფასების პროგნოზირება მოცემული 79 ცვლადის საფუძველზე, რომლებიც სახლს აღწერენ, როგორც რიცხვითი ისე არარიცხვითი მონაცემებით.
შეფასებას ვაკეთებთ ლოგარითმულად გარდაქმნილ ფასებზე RMSE-თი.

ფასების შესაფასებლად გავტესტე რამდენიმე სხვადასხვა მოდელი სხვადასხვა Feature Engineering-ებით. საუკეთესო შედეგი მივიღე Gradient Boosting Regressor-ით (RMSE = 0.13589). public RMSE = 0.13378.

# რეპოზიტორიის სტრუქტურა
ml_assn1/
│
├── model-experiment.ipynb     # მონაცემების დამუშავება, Cleaning, Feature Engineering, Feature Selection, Training, მოდელის სწავლება, MLFlow-თი ექსპერიმენტებზე დაკვირვება და მოდელების რეგისტრაცია.
├── model_inference.ipynb      # მოდელის ჩატვირთვა Model Registry-დან, პროგნოზი test set-ზე, submission-ის გენერირება Kaggle-ზე გაგზავნა.
└── README.md

# Feature Engineering
NaN მნიშვნელობების დამუშავება - რიცხვითებში სვეტებს ვავსებთ მედიანით, ხოლო კატეგორიულში "None" სტრინგით.
კატეგორიული ცვლადების რიცხვითში გადაყვანა - კატეგორიულ ცვლადებს გარდავქმნით one-hot encoding-ით.
Cleaning მიდგომები - სამიზნე ცვლადს, SalePrice-ს გარდავქმნით ლოგარითმულად, რათა შევამციროთ outlier-ის ეფექტი და განაწილება დავანორმალიზოთ.

# Feature Selection
საბოლოო მოდელში გამოყენებულია შემდეგი მიდგომები:
TotalSF-ში ერთად ვკრებთ ყველა საცხოვრებელ ფართს, განურჩევლად სართულისა.
ToralBathSF-ში ვკრებთ აბაზანების ფართს, სრულ აბაზანას ვანიჭებთ მეტ წონას, ვიდრე ნახევარს.
TotalRooms-ში ვკრებთ ოთახების რაოდენობას.

# Training
კონკურსზე მუშაობისას გავტესტეთ Random Forest Regressor-იც, რომელიც გვაძლევდა >=0.145 RMSE-ს, როცა Gradient Boosting Regressor გვაძლევდა <=1.139 RMSE-ს.
შესაბამისად, საბოლოოდ შევჯერდით Gradient Boosting Regressor-ზე, რომელიც იყენებს შემდეგ Hyperparameter-ებს:
n_estimators = 300
learning_rate = 0.05
max_depth = 3
random_state = 42

# MLflow Tracking
MLflow ექსპერიმენტების ბმული: https://dagshub.com/lkuch23/ml_assn1.mlflow
ჩაწერილი მეტრიკები:
RMSE Gradient Boosting Regressor-ის გამოყენებისას მერყეობს [0.1358; 0.1389] შუალედში.
public RMSE = 0.13378
