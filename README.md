# photo
# 🔍 Image Similarity Search Engine  

![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python)  
![Flask](https://img.shields.io/badge/Flask-Backend-green?logo=flask)  
![Torch](https://img.shields.io/badge/PyTorch-ResNet18-red?logo=pytorch)  
![License](https://img.shields.io/badge/License-MIT-lightgrey)  

A **deep learning–powered search engine** that lets you upload an image (or provide an image URL) and instantly find **visually similar products** from a catalog 📦.  

Using **ResNet18 embeddings** + **cosine similarity**, the system ranks catalog items most similar to the query image.  

---

## 🌐 Live Demo  

🚀 *Coming Soon* (Will update once deployed)  
<!-- Example placeholders for deployment -->
<!-- [Frontend Live](#) | [Backend API](#) -->

---

## ✨ Features  

- 📂 **Catalog Indexing** from a `products.csv` (id, name, category, price, image URL)  
- 📷 **Query by Image Upload or URL** (supports remote & local images)  
- 🧠 **Deep Learning Embeddings** using pretrained ResNet18 (ImageNet)  
- 📊 **Cosine Similarity Search** across catalog embeddings  
- 🎛 Adjustable **Similarity Threshold** (default 70%)  
- ⚡ **Fast Caching** of images & embeddings  
- 🎨 Simple, responsive **Flask + HTML UI**  

---

## 🗂 Project Structure  

```bash
image-similarity-search/
├─ backend/
│  ├─ app.py             # Flask backend (routes, embedding, search)
│  ├─ data/
│  │   ├─ products.csv   # Catalog metadata (id, name, price, img_url)
│  │   └─ index.csv      # Cached embeddings (auto-generated)
│  ├─ cache/             # Downloaded/cached images
│  └─ templates/
│      └─ index.html     # Web frontend (UI)
```
# 🔎 How It Works  

## 1️⃣ Indexing  
- Reads `products.csv`  
- Downloads catalog images (or loads from `/static/`)  
- Extracts **512-D embeddings** using pretrained **ResNet18**  
- Saves them in `index.csv`  

## 2️⃣ Query  
- User uploads an image / pastes a URL  
- Extracts embedding vector  
- Computes **cosine similarity** against catalog  

## 3️⃣ Results  
- Filters matches ≥ threshold (default 70%)  
- Sorts by similarity score  
- Displays **name, category, price, image, similarity score**  

---
# 🧭 Approach  

This project follows a **deep learning feature extraction + similarity matching** pipeline to deliver fast and accurate visual search results. The catalog is first indexed by reading `products.csv`, which contains product metadata such as id, name, category, price, and image path or URL. Each product image is processed using a **pretrained ResNet18 model**, where the final fully connected layer is removed to obtain **512-dimensional feature embeddings**. These embeddings capture the visual characteristics of each image and are stored in `index.csv` for quick reloading.  

When a user uploads an image or provides a remote URL, the system applies the same preprocessing and embedding extraction process. The query embedding is then compared with catalog embeddings using **cosine similarity**, which measures how close the images are in high-dimensional feature space. Results above a configurable threshold (e.g., 70%) are retrieved, sorted, and displayed with product details and similarity scores.  

The system ensures efficiency through caching, so repeated queries or previously downloaded images are processed faster. By combining **PyTorch** for embeddings, **Flask** for serving, and **Pandas/NumPy** for data handling, this project demonstrates how deep learning can power real-world applications like e-commerce visual search engines.  

---

# 🛠 Tech Stack  

- **Backend** → Flask, Pandas, NumPy, Torch, Torchvision, Pillow, Requests  
- **Model** → Pretrained ResNet18 (ImageNet features)  
- **Frontend** → HTML, CSS, Bootstrap (Flask templates)  
- **Storage** → CSV-based lightweight indexing  
- **Deployment** → Flask (Docker / Render / Heroku supported)  

---

# 🚀 Getting Started (Local)  

## 1️⃣ Clone the repo  
```bash
git clone https://github.com/your-username/image-similarity-search.git
cd image-similarity-search/backend
```
## 2️⃣ Setup environment
``` bash
python -m venv .venv
# Activate:
# Windows: .venv\Scripts\activate
# Linux/Mac: source .venv/bin/activate

pip install -r requirements.txt
```
### 📌 requirements.txt
``` txt
flask
torch
torchvision
pandas
numpy
pillow
requests
```
## 3️⃣ Prepare catalog data
- Create/edit backend/data/products.csv like:
``` csv
id,name,category,price,image_url
1,Red Shirt,Clothing,499,static/images/redshirt.jpg
2,Blue Jeans,Clothing,999,https://example.com/bluejeans.jpg
```
## 4️⃣ Run backend
``` bash
python app.py
```
## App runs at → http://127.0.0.1:5000

## 5️⃣ Open UI

### Go to browser → upload an image / paste URL → see results 🚀

## 🧪 Example Inputs
### ✅ Remote Image URL
``` bash
https://upload.wikimedia.org/wikipedia/commons/9/99/Black_square.jpg
```
### ✅ Local Static File
``` bash
static/images/item001.jpg
```
### 📡 API Reference
`🔸 POST /search`
### 📌 Form-Data Params
- `file` → uploaded image *(optional)*
- `image_url` → string *(optional)*
- `threshold` → number *(default: 70 → cosine ≥ 0.70)*

---

### 📤 Response
HTML page with:
- List of top matches  
- Similarity scores

## ☁ Deployment
- ✅ Run locally via Flask
- ✅ Deploy with Docker + Render/Heroku
- ✅ Persist cache/ & data/index.csv across runs

## 📸 Screenshots


