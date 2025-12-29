# 🎬 CinemaScopeAI  
**Multi-Task Movie Trailer Frame Classification**

CinemaScopeAI investigates whether a **single frame from a movie trailer** can encode meaningful information about a film’s **genre** and **budget category**. The project frames this problem as a **multi-task visual learning task**, combining genre recognition and budget classification within a shared representation.

Rather than focusing solely on performance, this project emphasizes **model construction, task interaction, and representation learning** under controlled experimental settings.

---

## 🧠 Motivation & Research Question

Movie trailers are designed to convey high-level semantic cues—tone, scale, and production value—within very limited visual context. This project explores the following questions:

- Can a **single trailer frame** reflect a film’s **budget scale** and **genres**?
- How do **shared visual representations** support multiple prediction objectives?
- What are the trade-offs between **custom architectures** and **transfer learning** in multi-task settings?

---

## 📊 Dataset

- **IMDb Top 250 movies**
- Trailer videos scraped automatically using **Selenium**
- Representative frames extracted using **OpenCV**
- Labels:
  - **Genres**: 10 classes (multi-label)
  - **Budget categories**: 5 classes (multi-class)

To simplify controlled experimentation, labels are **binary-encoded and embedded directly into filenames**, enabling deterministic data loading without external metadata files.

---

## 🧩 Methodology

### Method 1: Custom CNN (From Scratch)

- Implemented a full `tf.data` pipeline for efficient image loading and preprocessing
- Designed a **dual-head CNN architecture** with shared convolutional layers:
  - **Genre head**: multi-label prediction (sigmoid)
  - **Budget head**: multi-class prediction (softmax)
- Training features:
  - Task-specific loss functions
  - Early stopping
  - Learning rate scheduling
  - Model checkpointing

This approach allows explicit study of how **shared visual features** support different semantic tasks.

---

### Method 2: Transfer Learning with VGG16

- Used **VGG16 pretrained on ImageNet** as a frozen feature extractor
- Attached a custom classification head:
- Reformulated the problem as a **15-bit multi-label task**:
- 10 genre labels
- 5 budget labels
- Trained using **Keras Functional API** with `binary_crossentropy`

This formulation allows joint learning while leveraging strong pretrained visual representations.

---

## 🔍 Results & Analysis

- Transfer learning provides **faster convergence and improved stability**
- Genre prediction is more visually grounded than budget prediction
- Budget classification is more sensitive to dataset imbalance and representation limits
- Multi-task learning highlights trade-offs between shared and task-specific features

The results suggest that while single-frame prediction is feasible for high-level semantics, budget inference remains inherently more ambiguous.

---

## 🛠 Tech Stack

- TensorFlow / Keras  
- OpenCV  
- Selenium, BeautifulSoup  
- tf.data  
- Convolutional Neural Networks (CNN)
