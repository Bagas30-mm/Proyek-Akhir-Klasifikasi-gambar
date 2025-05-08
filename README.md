
# Proyek Klasifikasi Simbol Matematika Tulis Tangan

Proyek ini bertujuan untuk membangun model klasifikasi gambar menggunakan metode Convolutional Neural Network (CNN) untuk mengenali simbol matematika yang ditulis tangan.

## Dataset

Dataset yang digunakan berasal dari Kaggle dengan nama: [Handwritten Math Symbols](https://www.kaggle.com/datasets/sagyamthapa/handwritten-math-symbols). Dataset ini terdiri dari gambar-gambar simbol matematika seperti angka, operator, dan tanda kurung yang tersimpan dalam subdirektori sesuai dengan labelnya.

Dataset diunduh menggunakan `kagglehub`:

```python
import kagglehub
path = kagglehub.dataset_download("sagyamthapa/handwritten-math-symbols")
```

## Langkah-Langkah Proyek

### 1. Preprocessing Data

Gambar dimuat dari direktori menggunakan `ImageDataGenerator` dengan fitur:

- Normalisasi nilai piksel (rescale)
- Split otomatis antara data training dan validasi (validation_split)
- Target size gambar disesuaikan ke (64, 64)

### 2. Arsitektur Model

Model dibuat menggunakan `tf.keras.Sequential` dan terdiri dari:

- Beberapa lapisan Conv2D dan MaxPooling2D untuk ekstraksi fitur
- Lapisan Flatten untuk mengubah hasil konvolusi ke bentuk vektor
- Lapisan Dense dan Dropout
- Lapisan output dengan fungsi aktivasi `softmax` untuk klasifikasi 19 kelas

### 3. Training Model

Model dilatih dengan:

- Optimizer: Adam
- Loss function: Categorical Crossentropy
- Metric: Accuracy

### 4. Callbacks

- `ModelCheckpoint`: menyimpan model terbaik berdasarkan akurasi validasi
- `EarlyStopping`: menghentikan training jika tidak ada peningkatan dalam beberapa epoch

### 5. Evaluasi

Model diuji menggunakan data test dan menghasilkan akurasi yang tinggi. Hasil pelatihan divisualisasikan menggunakan `matplotlib`.

### 6. Ekspor Model

Model diekspor ke dalam tiga format:

- **SavedModel**: untuk TensorFlow Serving
- **TFLite**: untuk perangkat mobile/embedded
- **TensorFlow.js**: untuk digunakan di web

Label untuk model TFLite disimpan sebagai `label.txt`.

### 7. Validasi Prediksi

Prediksi dilakukan dengan menggunakan `tf.lite.Interpreter` dan divisualisasikan untuk memeriksa akurasi model terhadap data nyata.

## Struktur Direktori Output

```
/Submission/
├── saved_model/        # Model dalam format SavedModel
├── tflite/
│   ├── model.tflite    # Model dalam format TFLite
│   └── label.txt       # Label kelas
├── tfjs_model/         # Model dalam format TensorFlow.js
└── models.zip          # Arsip ZIP dari semua model di atas
```

## Lisensi dan Referensi

Dataset disediakan oleh [Sagyam Thapa](https://www.kaggle.com/datasets/sagyamthapa/handwritten-math-symbols) di Kaggle. Model dan kode dikembangkan untuk keperluan pembelajaran dalam Coding Camp Dicoding x DBS Foundation.

---

🧠 Dibuat oleh peserta Coding Camp 2025 dalam proyek klasifikasi gambar berbasis deep learning.
