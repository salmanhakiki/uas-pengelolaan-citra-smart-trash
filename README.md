# ♻️ Smart Trash Sorter: Sistem Pemilah Sampah Cerdas Berbasis Computer Vision & IoT

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-Framework-FF4B4B.svg)](https://streamlit.io/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-EfficientNetB0-FF6F00.svg)](https://www.tensorflow.org/)
[![ESP8266](https://img.shields.io/badge/IoT-ESP8266-success.svg)](https://www.espressif.com/)

Proyek ini dikembangkan sebagai pemenuhan Tugas Akhir / UAS mata kuliah **Pengelolaan Citra Digital**. 

Sistem ini merupakan purwarupa tempat sampah pintar yang mengintegrasikan pemrosesan citra digital (*Computer Vision*), kecerdasan buatan (*Deep Learning*), dan *Internet of Things* (IoT). Sistem mampu mengklasifikasikan jenis sampah (Organik vs Anorganik) melalui tangkapan kamera dan secara otomatis menggerakkan pintu tempat sampah yang sesuai menggunakan mikrokontroler.

---

## ✨ Fitur Utama

1. **Klasifikasi AI Presisi Tinggi (Hybrid Approach)**
   - Menggunakan model *Deep Learning* **EfficientNetB0** (Pre-trained ImageNet) yang dioptimasi untuk mendeteksi berbagai objek sampah.
   - Dilengkapi *fallback system* menggunakan heuristik ruang warna **HSV** untuk menganalisis material (seperti warna hijau/coklat untuk organik, dan warna transparan/abu untuk anorganik).
   - Implementasi *Multi-crop voting* (Full, 80% Center, 60% Center) untuk meningkatkan akurasi deteksi ROI (*Region of Interest*).

2. **Pipeline Pemrosesan Citra Digital**
   - **Original BGR:** Tangkapan citra mentah.
   - **Enhancement (CLAHE):** Peningkatan kontras adaptif untuk memperjelas tekstur sampah, terutama pada kondisi pencahayaan kurang.
   - **Edge Detection (Canny):** Ekstraksi fitur tepi menggunakan Gaussian Blur dan operator Canny.

3. **Antarmuka Web Interaktif (Dashboard)**
   - Dibangun menggunakan **Streamlit** untuk visualisasi *pipeline* citra secara *real-time*.
   - Mendukung Mode Simulasi (tanpa *hardware*) dan Mode Hardware Nyata.

4. **Komunikasi IoT Terintegrasi (Thread-Safe)**
   - Komunikasi serial asinkron dan *thread-safe* antara PC dan **ESP8266**.
   - Fitur *Auto-detect COM Port* (mendeteksi chip CH340/CP210x secara otomatis) dan mekanisme *auto-reconnect*.

---

## 🏗️ Arsitektur Perangkat Keras (Hardware)

* **Mikrokontroler:** ESP8266 (NodeMCU / Wemos D1 Mini)
* **Aktuator:** Motor Servo (Beroperasi pada rentang 0° hingga 180° untuk membuka flap sampah)
* **Indikator:** Layar LCD I2C (16x2) dan Buzzer (sebagai notifikasi audio)
* **Baud Rate Serial:** 115200 bps

---

## 📂 Struktur Direktori

```text
📁 uas-pengelolaan-citra-smart-trash/
├── 📄 final.py              # Skrip utama antarmuka Streamlit (UI & Pipeline)
├── 📄 classifier.py         # Modul AI (EfficientNetB0, HSV Masking, Preprocessing)
├── 📄 serial_comm.py        # Modul komunikasi serial Python <-> ESP8266
├── 📄 smart_trash.ino       # Source code C++ untuk di-upload ke ESP8266
└── 📄 Jalankan_Aplikasi.bat # Script batch untuk otomatisasi eksekusi server lokal
