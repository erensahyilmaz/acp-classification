# 🧬 AntiKanser Peptit Sınıflandırması (ACP Classification)

Bu projede iki farklı antikanser peptit (ACP) veri seti kullanılarak, çeşitli makine öğrenimi ve derin öğrenme yöntemleri ile ACP sınıflandırması gerçekleştirilmiştir. Projenin amacı, verilen peptit dizilerinin antikanser etkili olup olmadığını ya da etki derecesini tahmin etmektir.

---

## 📁 Kullanılan Veri Setleri

- **ACP-740**: [Scientific Reports (2021)](https://www.nature.com/articles/s41598-021-02703-3) çalışmasından alınmıştır. 740 örnek içerir.
- **Kaggle ACP Dataset**: [Kaggle - Anticancer Peptides Data Set](https://www.kaggle.com/datasets/anuragupadhyaya/anticancer-peptides-data-set). 4 sınıfa sahiptir (very active, mod active, inactive-exp, inactive virtual).

---

## ⚙️ Uygulanan Yöntemler

### 1. **Özellik Çıkarımı**
- **AAC (Amino Acid Composition)**: Her dizideki amino asitlerin oranları çıkarılmıştır.
- **ProtBERT Embedding**: `Rostlab/prot_bert` ile dizilerden 1024 boyutlu vektörler çıkarılmıştır.

### 2. **Makine Öğrenimi Modelleri**
- **SVC (Support Vector Classifier)**:
  - AAC verileriyle eğitim yapılmıştır.
  - Kaggle seti: 4 sınıf
  - ACP-740: 2 sınıf (ACP vs Non-ACP)

### 3. **Derin Öğrenme Modeli**
- **CNN + LSTM Hibrit Yapısı**:
  - BERT → CNN
  - AAC → LSTM
  - Concatenate edilip Dense katmanla çıkış sağlandı.
  - `TensorFlow` ile eğitildi.

---

## 📊 Performans Sonuçları (Özet)

| Veri Seti       | Yöntem        | Accuracy | F1-Score | Precision | Recall |
|------------------|---------------|----------|----------|-----------|--------|
| Kaggle ACP       | SVC           | 0.90     | 0.48     | 0.53      | 0.48   |
| ACP-740          | SVC           | 0.81     | 0.82     | 0.82      | 0.81   |
| ACP-740          | CNN + LSTM    | 0.90     | 0.90     | 0.88      | 0.92   |

---

## 📈 Görseller

### 🎯 Sınıf Dağılımı (Kaggle)
![indir (31)](https://github.com/user-attachments/assets/ff306e92-5f21-4014-a31e-4891a764eb4e)

### 📊 Peptid Uzunlukları(ACP-740)
![indir (38)](https://github.com/user-attachments/assets/696484b5-7f78-4664-8479-e1ecbdfec7c7)

### 🔥 Korelasyon Haritası (AAC-Kaggle)
![indir (39)](https://github.com/user-attachments/assets/ee36d7ea-3f10-43c9-b9c6-38151f81f2b6)

### 📉 Confusion Matrix - SVC (Kaggle)
![indir (43)](https://github.com/user-attachments/assets/d2f81af3-2a83-43f8-9b66-1f2effa50512)

### 📉 Confusion Matrix - SVC (ACP-740)
![indir (41)](https://github.com/user-attachments/assets/c3ceada0-bf74-4d48-a66f-b1469e3d81cd)

### 📉 Confusion Matrix - CNN+LSTM (ACP-740)
![indir (42)](https://github.com/user-attachments/assets/091c93c6-4ec6-4c67-9910-5cff2aa18612)

---

## ⚙️ Gereksinimler

```bash
pip install pandas seaborn scikit-learn matplotlib torch transformers tensorflow tqdm
