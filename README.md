# 🥦 Cannabis E-Commerce Hybrid Recommendation System

> *Most cannabis platforms show the same products to every user. This project builds a personalization engine that combines what users do with what products contain, generating recommendations that reflect both behavior and content.*

---

## 🧩 Business Context

Cannabis e-commerce platforms like Weedmaps face a personalization challenge that most retail recommendation systems don't. Product names, strain types, effect tags, and THC/CBD percentages are highly specific attributes that drive purchase decisions but don't map cleanly to standard collaborative filtering approaches. A user who buys an Indica flower for relaxation has very different needs than one buying a Sativa concentrate for creativity, even if their click behavior looks similar on the surface.

This project addresses that gap by building a hybrid recommendation engine that combines two signals: what users have interacted with (behavioral graph embeddings via Node2Vec) and what products are about (content similarity via TF-IDF on descriptions, strain types, and effect tags). Neither signal alone is sufficient. Together they produce recommendations that reflect both demonstrated preference and product relevance.

---

## 📊 Dataset

**Two simulated datasets reflecting a cannabis e-commerce platform:**

Products catalog:
- 100 cannabis products across 4 categories (Flower, Concentrate, Edible, Vape Cartridge)
- Attributes: strain type, THC/CBD percentage, potency, price, vendor, product description, effect tags

User behavior:
- 29,010 user interactions across 5 event types: view, click, save, cart, buy
- Purchases represent 8.98% of all interactions, indicating significant class imbalance

---

## 🔍 EDA Highlights

**Funnel conversion rates:**

| Stage | Conversion Rate |
|-------|----------------|
| Click to Cart | 96.0% |
| Cart to Buy | 94.6% |

High funnel efficiency means the bottleneck is not conversion — it is discovery. Users who engage with a product almost always buy it. The recommendation problem is therefore about surfacing the right products in the first place, not about nudging hesitant buyers.

**Category performance:**

| Category | Total Clicks | Total Purchases | Avg Rating |
|----------|-------------|----------------|-----------|
| Edibles | ~3,000 | ~700 | 3.67 |
| Concentrates | ~2,900 | ~800 | 3.62 |
| Flower | ~2,100 | ~650 | 3.68 |
| Vape Cartridges | ~1,800 | ~450 | 3.43 |

Concentrates drive the most purchases despite fewer clicks than Edibles, suggesting higher purchase intent per session. Vape Cartridges have both the fewest interactions and the lowest ratings, pointing to a potential assortment or quality gap.

---

## 🛠️ Recommendation System Architecture

**Why a hybrid approach?**

Collaborative filtering alone (Node2Vec graph embeddings) captures what users with similar behavior liked. Content-based filtering alone (TF-IDF) captures product similarity on text attributes. Neither is sufficient independently for cannabis retail:

- Pure collaborative: new products with no interactions get no recommendations regardless of how relevant their content is
- Pure content: two products with identical descriptions but different user appeal get treated the same

The hybrid approach blends both signals with a weighted score (alpha = 0.6 for graph, 0.4 for content), generating top-5 recommendations that reflect both behavioral patterns and product content relevance.

**Graph Embeddings (Node2Vec)**
- Built a bipartite user-product interaction graph using NetworkX
- Trained Node2Vec embeddings to capture user-product relationship patterns
- Generated user preference profiles via weighted average of interacted product embeddings, weighting by interaction type (buy > cart > save > click > view)
- Applied cosine similarity between user profiles and product embeddings to score recommendations

**Content Similarity (TF-IDF)**
- Vectorized product text combining name, strain type, category, tags, and descriptions
- Computed cosine similarity matrix across all products
- Maximum product-to-product similarity score of 0.35 reflects genuine diversity in the product catalog

**Cold Start Handling**   
- Users with no interaction history receive top popular products by interaction volume rather than personalized recommendations

---

## 📈 Purchase Prediction Models

Three classifiers were evaluated to predict purchase likelihood from behavioral features, with SMOTE applied to address the 8.98% purchase rate class imbalance.

| Model | ROC-AUC (Pre-SMOTE) | Recall Class 1 | Notes |
|-------|--------------------|--------------------|-------|
| Logistic Regression | ~0.53 | 0.55 | Near-random |
| Random Forest | ~0.53 | 0.62 | Near-random |
| XGBoost | ~0.53 | 0.68 | Best recall |

**Why models underperformed:**

   All three models returned ROC-AUC scores near 0.53, barely above random chance. This is not a modeling failure — it is a simulation constraint. In this dataset, funnel progression (click, save, cart, buy) was assigned using random probabilities applied uniformly across all users and products with no feature-driven bias. When purchase outcomes are effectively weighted coin flips uncorrelated with product price, category, or user history, no model can learn a meaningful decision boundary. This is the same fundamental limitation as any model trained on noise.

   SMOTE improved recall on the minority class but did not improve ROC-AUC, confirming the issue is feature signal quality rather than class balance. In a production dataset where purchases correlate with price sensitivity, brand loyalty, strain preference, and prior behavior, these models would be expected to perform significantly better.

**Recall remains the right primary metric.** 

   Missing a potential buyer carries higher opportunity cost than an incorrect recommendation. The business case for optimizing recall holds regardless of the simulation constraint.

---

## 🔑 Key Takeaways

**Discovery is the real problem, not conversion**

   - With 96% click-to-cart and 94.6% cart-to-buy conversion rates, users who find products they want almost always buy them. The recommendation engine addresses the upstream challenge of getting the right product in front of the right user.

**Hybrid architecture handles cannabis-specific challenges**

   - Product content (strain type, effect tags, THC/CBD) carries meaningful personalization signal that pure collaborative filtering ignores. The TF-IDF layer ensures product attributes inform recommendations even for new or low-interaction products.

**Simulation realism is the binding constraint on model performance**

   - Purchase prediction underperformed because behavioral signals were randomly assigned rather than feature-driven. The modeling framework is sound. The limitation is the data generation process, not the approach. With no bias or a priori about user behavior, the model learns randomly. 

---

## 🚀 Future Work

- Bias simulation probabilities by product features (price, category, strain type, ratings) to create learnable patterns for purchase prediction models
- Integrate user demographics for more granular personalization
- Experiment with LightGCN or other graph neural network recommenders as alternatives to Node2Vec
- Replace TF-IDF with LLM embeddings (OpenAI API) for richer semantic product similarity
- Deploy as an API endpoint for real-time product recommendation

---

## 🔧 Tools
Python, Node2Vec, NetworkX, TF-IDF, XGBoost, Random Forest, Logistic Regression, SMOTE, GridSearchCV, Pandas, NumPy, Matplotlib, Seaborn,scikit-learn, imbalanced-learn
