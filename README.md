# 🎥 Deepfake Detection with Deep Learning (FET312)

Bu proje, **FET312 Derin Öğrenme** dersi kapsamında, **FaceForensics++ (C23)** veri seti kullanılarak deepfake videoların tespit edilmesi amacıyla geliştirilmiştir. Proje, vize aşamasında temel (baseline) CNN modellerinin geliştirilmesini ve analiz edilmesini kapsamaktadır.

## Ekip Üyeleri (Team Members)

| Ad Soyad                      | Öğrenci No  | Röller                            |
|-------------------------------|-------------|-----------------------------------|
| **Khaiitmurod Khabibullayev** | 22040101116 | Veri İşleme & **SimpleCNN**       |
| **Muhammed Ali Cüre**         | 23040101006 | **BatchNormCNN** (LeakyReLU)      |
| **Abdumajid Abdulkhaev**      | 22040101002 | **RescaledCNN** (Optimized Input) |

---

## Proje Dosya Yapısı (Repository Structure)

Bu repo, proje ilerleme raporunu ve her grup üyesinin geliştirdiği özgün model kodlarını içermektedir.

├── notebooks/           # Grup üyelerinin geliştirdiği kaynak kodlar (.ipynb)
│   ├── FET312_..._1.ipynb  -> SimpleCNN Modeli (Khaiitmurod)
│   ├── FET312_..._2.ipynb  -> BatchNormCNN Modeli (Muhammed)
│   └── FET312_..._3.ipynb  -> RescaledCNN Modeli (Abdumajid)
│
├── reports/             # Proje İlerleme Raporu (PDF)
│   └── FET312_..._ProjectOutline.pdf
│
└── README.md            # Proje dokümantasyonu

Proje Özeti ve Yöntemler (Methodology)
1. Veri Seti (Dataset)
Projede FaceForensics++ (C23 Compression) veri seti kullanılmıştır.
Eğitim: 250 Real + 250 Fake (Deepfakes, Face2Face, FaceSwap vb. karışık)
Test: 25 Real + 25 Fake (Modelin hiç görmediği hold-out set)
Ön İşleme: Videolardan kare (frame) çıkarımı, face_recognition kütüphanesi ile yüz tespiti ve kırpma (cropping).
2. Geliştirilen Modeller (Baseline Models)
Vize aşamasında hazır mimariler (ResNet, VGG vb.) kullanılmamış, grubumuz tarafından sıfırdan tasarlanan 3 farklı CNN mimarisi test edilmiştir:
SimpleCNN: 3 katmanlı, Dropout destekli temel mimari.
BatchNormCNN: 4 katmanlı, Batch Normalization ve LeakyRelu kullanan daha derin yapı.
RescaledCNN: 128x128 giriş boyutuna sahip, Rescaling katmanı içeren hafif yapı.

Sonuçlar (Results)
Modellerin 50 videoluk test seti üzerindeki performans karşılaştırması aşağıdadır:
Model	Doğruluk (Accuracy)	Precision (Fake)	Recall (Fake)	F1 Score
SimpleCNN	%58.00	0.83	0.20	0.32
BatchNormCNN	%62.00	0.80	0.32	0.46
RescaledCNN	%50.00	0.50	1.00	0.67
Analiz: Vize aşamasında BatchNormCNN en dengeli sonucu vermiştir. Sığ (shallow) modellerin deepfake tespitinde sınırlı kaldığı görülmüş olup, 
final projesinde Transfer Learning yöntemlerine geçiş yapılacaktır.

Kurulum ve Kullanım (Installation)
Kodlar Google Colab üzerinde çalıştırılmak üzere tasarlanmıştır. Çalıştırmak için:
notebooks/ klasöründeki .ipynb dosyasını Google Colab'da açın.
Gerekli kütüphaneleri yükleyin:
!pip install face_recognition dlib torch torchvision opencv-python
Kaggle API anahtarınızı (kaggle.json) yükleyerek veri setini indirin (Kod içerisinde adımlar mevcuttur).
Tüm hücreleri sırasıyla çalıştırın.

Gelecek Planları (Future Work)
Final projesinde performansın artırılması için aşağıdaki mimariler kullanılacaktır:
InceptionV3: Çok ölçekli özellik çıkarımı için.
ResNet50: Derinlemesine doku analizi için.
MobileNetV2: Mobil uyumlu ve hızlı çıkarım için.

Lisans ve Referanslar
Bu çalışma akademik amaçla hazırlanmıştır.
Dataset Citation: Rössler et al., "FaceForensics++: Learning to Detect Manipulated Facial Images", ICCV 2019.
