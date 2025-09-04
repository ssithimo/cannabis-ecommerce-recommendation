# 🥦 cannabis-ecommerce-recommendation
This project analyzes cannabis product and user interaction data from an e-commerce platform and builds a **hybrid recommendation engine** that blends **graph embeddings** (Node2Vec) with **text-based similarity** (TF-IDF on product descriptions). The goal is to improve personalization and discovery in cannabis marketplaces such as Weedmaps.

---

## 🔍 Project Overview
- **Domain:** Cannabis e-commerce and product recommendation
- **Techniques:** Exploratory data analysis (EDA), feature engineering, graph embeddings, NLP, classification modeling, and hybrid recommendation
- **Objective:** Build a scalable framework for personalized product recommendations that leverage both user behavior patterns and product content

---

## 🛠️ Tech Stack
- **Languages:** Python  
- **Libraries & Tools:** pandas, NumPy, scikit-learn, XGBoost, imbalanced-learn (SMOTE), TF-IDF, NetworkX, Node2Vec, Matplotlib, Seaborn  
- **Key Skills:** Data Cleaning, Data Visualization, Graph Analytics, NLP, Machine Learning, Recommender Systems  

---

## 📈 Key Features
- **User Behavior Analysis:** Modeled engagement (click, save, cart, buy) and conversion funnels  
- **Feature Engineering:** Captured time-based recency, product popularity, pricing sensitivity, and user engagement signals  
- **NLP Content Similarity:** Vectorized product descriptions, tags, and strain attributes with TF-IDF  
- **Graph-Based Recommendation:** Created bipartite user-product graph and trained Node2Vec embeddings  
- **Hybrid Recommendation Engine:** Combined graph embeddings and NLP similarity for top-N product recommendations  
- **Purchase Prediction Models:** Built Logistic Regression, Random Forest, and XGBoost classifiers; tuned via GridSearchCV and SMOTE to improve recall  

---

## 📊 Exploratory Data Analysis Highlights
- Category and strain-level product distribution
- Pricing trends and boxplots for product categories
- Funnel visualization from click → cart/save → purchase
- Rating distributions across product segments

---

## 🚀 Outcomes
- Designed a **personalization system tailored to cannabis retail** platforms  
- Demonstrated hybrid recommender capability leveraging **both behavior data and product content**  
- Framework ready for deployment or extension into deep learning and real-time systems  

---

## 🔮 Next Steps
- Integrate conditional probabilities for purchasing behaviors in simulated data for better model outcomes
- Integrate user demographics for more granular personalization  
- Experiment with LightGCN or other graph neural network recommenders  
- Deploy as an API endpoint for product recommendation
- Employ LLM text embeddings (OpenAI api) with graph-based emebeddings to create a better hybrid recommendation system

---

## 🧑‍💻 Author
**Sam Sithimolada**  
- [LinkedIn](https://linkedin.com/in/SamSithimolada)
- [Portfolio](https://github.com/ssithimo)

