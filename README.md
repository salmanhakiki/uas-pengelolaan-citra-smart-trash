# ♻️ TrashVision: Real-Time Smart Trash Classifier

[![Python Version](https://img.shields.io/badge/python-3.9%20%7C%203.10%20%7C%203.11-blue)](https://www.python.org/)
[![Framework](https://img.shields.io/badge/backend-PyTorch%20%7C%20Ultralytics-ee4c2c)](https://pytorch.org/)
[![Frontend](https://img.shields.io/badge/ui-Streamlit-ff4b4b)](https://streamlit.io/)

Sistem klasifikasi sampah cerdas (Organik & Anorganik) berbasis web-dashboard yang dirancang untuk kebutuhan pemilahan sampah otomatis secara *real-time*. Sistem ini menggabungkan model *Deep Learning* **YOLOv8** dengan *fallback system* berbasis **HSV** untuk akurasi deteksi material yang optimal.

---

## ✨ Fitur Utama

1. **Klasifikasi AI Presisi Tinggi (Hybrid Approach)**
   - Menggunakan model *Deep Learning* **YOLOv8** (`yolov8n.pt`) yang dioptimasi untuk mendeteksi berbagai objek sampah dengan latensi rendah.
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
📁 Tugas Smart-trash/
├── 📄 app.py                     # Skrip utama antarmuka Streamlit (UI & Pipeline)
├── 📄 smart_classifier.py        # Modul AI (YOLOv8 Inference, HSV Masking, Preprocessing)
├── 📄 waste_knowledge_base.py    # Database pemetaan material sampah
├── 📄 serial_comm.py             # Modul komunikasi serial Python <-> ESP8266
├── 📄 yolov8n.pt                 # File pre-trained model YOLOv8 Nano
├── 📄 download_weights.py        # Skrip Python pengunduh bobot AI
├── 📄 download_massive_data.py   # Skrip pengunduh dataset masif
├── 📄 requirements.txt           # Dependensi library Python
├── 📄 run_app.bat                # Script batch untuk otomatisasi eksekusi server lokal (Streamlit)
├── 📄 setup.bat                  # Script batch untuk setup awal environment
├── 📄 download_weights.bat       # Script batch pendukung unduh bobot
└── 📁 __pycache__/               # Cache eksekusi Python
