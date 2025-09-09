# Analisis Sentimen Ulasan PlayStore & Tokopedia

## Deskripsi Proyek
Proyek ini bertujuan untuk melakukan **analisis sentimen pada ulasan pengguna** dari PlayStore/Tokopedia.  
Model yang dibangun mampu mengklasifikasikan sentimen teks menjadi tiga kelas utama:
- **Positif**
- **Negatif**
- **Netral**

Pendekatan yang digunakan adalah **kombinasi Machine Learning klasik dan Deep Learning (IndoBERT, BiLSTM)**, serta melibatkan **pseudo-labeling** dan **fine-tuning** untuk meningkatkan akurasi.

---

## Kriteria Proyek
Proyek ini disusun untuk memenuhi persyaratan berikut:
1. **Dataset minimal 10.000 sampel** → hasil scraping mandiri dari PlayStore/Tokopedia.
2. **Tiga kelas sentimen** (positif, netral, negatif).
3. **Ekstraksi fitur & pelabelan**: kombinasi manual labeling + pseudo-labeling.
4. **Menggunakan algoritma Deep Learning** (BiLSTM, IndoBERT).
5. **Akurasi minimal 85% pada test set** (target utama).
6. **Tiga skema pelatihan berbeda**:
   - Skema 1: SVM + TF-IDF
   - Skema 2: BiLSTM + Word2Vec
   - Skema 3: IndoBERT fine-tuning + semi-supervised
7. **Inference testing** tersedia dalam `.ipynb` → menghasilkan output kategorikal (`positif`, `netral`, `negatif`).

---

## Tahapan Proses

### Scraping Data
- Data diambil dari **Google Play Store & Tokopedia Review**.
- Total data: **> 10.000 review**.
- Disimpan ke dalam file `.csv`.

### Preprocessing
- Normalisasi teks: lowercase, hapus angka/simbol/emoticon.
- Tokenisasi.
- Stopword removal (NLTK + stopword bahasa Indonesia).
- Lemmatization/Stemming ringan.

### Labeling
- **Manual labeling subset (±2.000–3.000 data)** → digunakan sebagai training set utama.
- **Pseudo-labeling dengan IndoBERT** → untuk memperluas dataset.
- Label encoding (`positif=0`, `netral=1`, `negatif=2`).

### Skema Eksperimen
- **Skema 1: SVM + TF-IDF**
  - TF-IDF digunakan sebagai ekstraksi fitur.
  - Hasil: akurasi val ~82–85%.
- **Skema 2: BiLSTM + Word2Vec**
  - Embedding Word2Vec.
  - Hasil: akurasi val ~64–70% (kurang baik).
- **Skema 3: IndoBERT Fine-tuning**
  - Fine-tuning model `indobenchmark/indobert-base-p1`.
  - Early stopping + scheduler + pseudo-labeling.
  - Hasil: akurasi test ≥85% (memenuhi kriteria reviewer).

### Evaluasi
- **Train Accuracy**: 90%+
- **Validation Accuracy**: 85–92%
- **Test Accuracy**: ≥85% (IndoBERT)
- **Metrik tambahan**:
  - Classification Report (Precision, Recall, F1)
  - Confusion Matrix
