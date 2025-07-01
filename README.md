# 🧬 Anticancer Peptide (ACP) Sınıflandırması ve Açıklanabilir Derin Öğrenme

Bu proje, anticancer peptidlerin (ACP) sınıflandırılması amacıyla klasik makine öğrenmesi ve derin öğrenme yöntemlerini bir araya getiren **multimodel** bir yaklaşım sunmaktadır. Ayrıca, model kararlarının yorumlanabilirliğini sağlamak amacıyla **açıklanabilir yapay zeka (XAI)** teknikleri olan **SHAP** ve **LIME** uygulanmıştır.

---

## 📌 İçindekiler

- [Proje Amacı](#proje-amacı)
- [Kullanılan Veri Setleri](#kullanılan-veri-setleri)
- [Özellik Çıkarımı](#özellik-çıkarımı)
- [Model Mimarileri](#model-mimarileri)
- [Sonuçlar](#sonuçlar)
- [Açıklanabilirlik (XAI)](#açıklanabilirlik-xai)
- [Görseller](#görseller)
- [Kaynakça](#kaynakça)

---

## 🎯 Proje Amacı

Bu çalışmada hedef:
- ACP’leri doğru şekilde sınıflandırmak
- Farklı embedding (AAC, ProtBERT, TAPE, ESM) tekniklerini karşılaştırmak
- Derin öğrenme mimarilerini test etmek
- Model kararlarını açıklamak

---

## 📂 Kullanılan Veri Setleri

| Veri Seti      | Pozitif Örnek | Negatif Örnek | Kaynak |
|----------------|---------------|----------------|--------|
| ACP-740        | 376           | 364            | Ahmed et al. (2021) |
| AntiCP2        | 970           | 970            | Lv et al. (2021) |
| ACPred-FL      | 332           | 332            | Wei et al. (2018) |
| DeepGram       | 444           | 444            | Akbar et al. (2022) |
| Kaggle ACP     | 949 (çok sınıflı) | -        | Upadhyaya (2023) |

---

## 🧪 Özellik Çıkarımı

- **AAC (Amino Acid Composition):** Her dizideki 20 amino asit oranı
- **ProtBERT:** Protein dil modeli (1024 boyutlu gömme)
- **TAPE:** Transformer tabanlı protein embedding
- **ESM:** Facebook AI Research tarafından geliştirilen protein temsili

Bu embedding'ler **tek başına** veya **birleştirilerek** (örneğin `ProtBERT + TAPE`) kullanılmıştır.

---

## 🧠 Model Mimarileri

- Klasik ML: `SVC (Support Vector Classifier)`
- Derin Öğrenme: `CNN` (ProtBERT/ESM) + `LSTM` (AAC/TAPE)
- Eğitim parametreleri:
  - `batch_size = 32`
  - `epoch = 30`
  - `optimizer = Adam`

---

## 📈 Sonuçlar

Aşağıda çeşitli kombinasyonların doğruluk (Accuracy), F1-score, Precision ve Recall metrikleri yer almaktadır:

| Veri Seti     | Model                  | Accuracy | F1    | Precision | Recall |
|---------------|------------------------|----------|-------|-----------|--------|
| Kaggle (ACP)  | SVC                    | 0.90     | 0.48  | 0.53      | 0.48   |
| ACP-740       | SVC                    | 0.81     | 0.81  | 0.82      | 0.81   |
| ACP-740       | ProtBERT + AAC         | 0.84     | 0.85  | 0.83      | 0.86   |
| ACP-740       | ProtBERT + TAPE        | 0.87     | 0.88  | 0.85      | 0.91   |
| ACP-740       | ESM + TAPE             | 0.89     | 0.89  | 0.90      | 0.88   |
| ACPred-FL     | ProtBERT + AAC         | 0.82     | 0.82  | 0.80      | 0.85   |
| ACPred-FL     | ProtBERT + TAPE        | 0.81     | 0.81  | 0.81      | 0.82   |
| ACPred-FL     | ESM + TAPE             | 0.83     | 0.85  | 0.77      | 0.94   |
| AntiCp2       | ProtBERT + AAC         | 0.90     | 0.90  | 0.92      | 0.88   |
| AntiCp2       | ProtBERT + TAPE        | 0.89     | 0.89  | 0.94      | 0.84   |
| AntiCp2       | ESM + TAPE             | **0.92** | 0.92  | 0.90      | **0.95** |
| DeepGram      | ProtBERT + AAC         | 0.83     | 0.83  | 0.82      | 0.84   |
| DeepGram      | ProtBERT + TAPE        | 0.86     | 0.86  | 0.85      | 0.86   |
| DeepGram      | ESM + TAPE             | 0.83     | 0.83  | 0.79      | 0.87   |

> 📌 **Not:** SVC dışındaki tüm modeller CNN + LSTM mimarisine sahiptir.

---

## 🧾 Açıklanabilirlik (XAI)

Projede aşağıdaki yöntemler uygulanmıştır:

- **SHAP (SHapley Additive Explanations)**
- **LIME (Local Interpretable Model-agnostic Explanations)**

# Örnek SHAP görseli

![shap-svc5](https://github.com/user-attachments/assets/f0fdb3d4-0ea0-41d2-a61b-0e8a614469bd)



## 🖼️ Görseller

Aşağıda farklı veri setleri ve modeller için oluşturulmuş bazı örnek grafikler sunulmuştur. Bu grafikler, model eğitiminin performansını, sınıf ayrımındaki doğruluğu ve genel başarı durumunu analiz etmeye yardımcı olmaktadır.

---

### 📉 1. Loss Grafiği - AntiCp2 Veri Seti / CNN(ESM) + LSTM(TAPE)

![esm_tape_loss](https://github.com/user-attachments/assets/212c7ae4-bb3c-4f73-bf3a-e6e6f49c322b)

> Bu grafikte, eğitim sürecinde epoch başına kayıp (loss) değerinin azaldığı görülmektedir. Modelin öğrenme eğrisinin istikrarlı olduğu, overfitting'e düşmeden başarılı bir şekilde optimize edildiği anlaşılmaktadır.

---

### 📈 2. ROC-AUC Grafiği - AntiCp2 Veri Seti / CNN(ESM) + LSTM(TAPE)

![roc_esm_tape](https://github.com/user-attachments/assets/47074704-7c2e-4430-a52c-0f5d5df96792)

> ROC eğrisi, sınıflandırma modelinin pozitif ve negatif örnekleri ayırt etme başarısını gösterir. AUC değeri 0.95'e yakın olup modelin güçlü bir ayrıştırıcı olduğunu ortaya koymaktadır.

---

### 📊 3. Confusion Matrix - AntiCp2 Veri Seti / CNN(ESM) + LSTM(TAPE)

![cm_esm_tape](https://github.com/user-attachments/assets/24398254-58a3-4de0-bcbf-335f7374df78)

> Karmaşıklık matrisi, modelin hem pozitif hem de negatif örnekleri büyük oranda doğru sınıflandırdığını göstermektedir. Yanlış pozitif ve yanlış negatif oranları düşüktür.

---


### 📊 4. Confusion Matrix - ACPred-FL Veri Seti / CNN(ProtBERT) + LSTM(TAPE)

![cm-bert_tape](https://github.com/user-attachments/assets/96054c27-ee7d-4e94-8b01-a66e859021af)

> ACPred-FL veri setinde model, 0 ve 1 sınıflarını oldukça başarılı şekilde ayırabilmiştir. Özellikle pozitif sınıftaki doğruluk oranı dikkat çekicidir.

---

### 📉 5. Loss Grafiği - DeepGram Veri Seti / CNN(ProtBERT) + LSTM(AAC)

![bert_aac_loss](https://github.com/user-attachments/assets/72f2092c-dd82-42eb-8e38-d54c1a574893)

> DeepGram veri setinde loss eğrisi, modelin eğitim sürecinde istikrarlı şekilde kaybı azalttığını göstermektedir. Başarılı bir öğrenme süreci sergilenmiştir.

---

### 📉 6. Genel Model Değerlendirmesi

![model_cpmparasion](https://github.com/user-attachments/assets/502653c0-7412-4f7e-beed-dbec0e277db4)

> Tüm verisetlerinin ve model performanslarının genel değerlendirmesi.

---



## ⚙️ Gereksinimler

```bash
pip install pandas seaborn scikit-learn matplotlib torch transformers tensorflow tqdm
