# 🧠👁️ Percepción y Visión - Sentidos del Robot Humanoide

## Propósito

Este módulo implementa la **percepción multimodal** del robot humanoide, simulando los sentidos humanos mediante sensores y algoritmos de procesamiento. El objetivo es crear un sistema perceptivo completo que permita al robot entender e interactuar con su entorno de manera similar a un humano.

El sistema integra **visión computacional avanzada** como el sentido primario, complementado con otros sistemas sensoriales para crear una percepción multimodal robusta.

---

## 🌐 Visión General: Los 7 Sentidos Robóticos

El robot humanoide integra los siguientes sistemas sensoriales:

| Sentido | Hardware | Software | Subcarpeta |
|---------|----------|----------|------------|
| 👀 **Visión** | Cámaras RGB + RGB-D | OpenCV, YOLO, ORB-SLAM | [`vision/`](#visión) |
| 👂 **Audición** | Micrófonos array | FFT, MFCC, Whisper, NLP | `sensores/audio/` |
| 👃 **Olfato** | Sensores de gas (MQ) | Clasificación ML | `sensores/chemical/` |
| 👅 **Gusto** | Biosensores químicos | Análisis de composición | `sensores/chemical/` |
| ✋ **Tacto** | Sensores hápticos/FSR | RNN, LSTM | `sensores/tactile/` |
| 🧭 **Propiocepción** | IMU, encoders | Filtros Kalman, PID | `sensores/imu/` |
| ⚖️ **Equilibrio** | IMU, giroscopio | Control dinámico | Ver [04_Planificacion_Control](../04_Planificacion_Control/) |

---

## 📂 Estructura del Directorio

```
02_Percepcion_Vision/
├── README.md (este archivo)
│
├── vision/                         # 👁️ Sistema visual completo
│   ├── detection/                 # Detección de objetos (YOLO, Faster R-CNN)
│   ├── segmentation/              # Segmentación semántica/instancia
│   ├── face_recognition/          # Reconocimiento facial
│   ├── pose_estimation/           # Estimación de pose humana
│   ├── slam/                      # SLAM Visual (ORB-SLAM3)
│   ├── depth/                     # Percepción de profundidad (RGB-D, estéreo)
│   ├── tracking/                  # Seguimiento de objetos (DeepSORT)
│   ├── gestures/                  # Reconocimiento de gestos
│   ├── ocr/                       # Reconocimiento de texto
│   └── models/                    # Modelos entrenados
│
├── sensores/                       # Drivers y procesamiento de sensores
│   ├── cameras/                   # Cámaras RGB y RGB-D
│   ├── audio/                     # Micrófonos y arrays
│   ├── chemical/                  # Sensores de gas y químicos
│   ├── tactile/                   # Sensores de fuerza y presión
│   ├── imu/                       # IMU, giroscopios, acelerómetros
│   └── temperature/               # Sensores de temperatura
│
├── fusion/                         # Fusión sensorial multimodal
│   ├── ekf/                       # Extended Kalman Filter
│   ├── ukf/                       # Unscented Kalman Filter
│   ├── complementary/             # Filtros complementarios
│   └── multimodal/                # Fusión de múltiples modalidades
│
├── preprocessing/                  # Preprocesamiento de señales
│   ├── calibration/               # Calibración de sensores
│   ├── filtering/                 # Filtrado de ruido
│   ├── normalization/             # Normalización de datos
│   └── feature_extraction/        # Extracción de características
│
└── notebooks/                      # Notebooks de demostración
    ├── vision_detection.ipynb
    ├── face_recognition.ipynb
    ├── audio_processing.ipynb
    ├── sensor_fusion.ipynb
    └── multimodal_perception.ipynb
```

---

## 👁️ Visión

### Capacidades del Sistema Visual

| Capacidad | Descripción | Tecnología Principal |
|-----------|-------------|---------------------|
| **Detección de objetos** | Identificar y localizar objetos | YOLO v8, Faster R-CNN |
| **Segmentación** | Separar objetos por píxeles | Mask R-CNN, U-Net |
| **Reconocimiento facial** | Identificar y verificar personas | FaceNet, ArcFace |
| **Estimación de pose** | Detectar posiciones de personas | OpenPose, MediaPipe |
| **SLAM Visual** | Mapeo y localización simultáneos | ORB-SLAM3, RTAB-Map |
| **Percepción 3D** | Reconstrucción tridimensional | Estéreo, RGB-D |
| **Seguimiento** | Rastrear objetos en movimiento | SORT, DeepSORT |
| **Gestos** | Interpretar gestos humanos | MediaPipe, CNN |

### Hardware Recomendado
- **Cámaras RGB**: Raspberry Pi Camera V2, Logitech C920
- **Cámaras de profundidad**: Intel RealSense D435i, Kinect v2
- **Estéreo**: Dual Pi Camera setup
- **Resolución**: Mínimo 720p @ 30fps

### Ejemplo: Detección de Objetos con YOLO

```python
from ultralytics import YOLO
import cv2

# Cargar modelo YOLO
model = YOLO('yolov8n.pt')

# Detectar objetos en tiempo real
cap = cv2.VideoCapture(0)
while cap.isOpened():
    ret, frame = cap.read()
    if ret:
        results = model(frame, conf=0.5)
        annotated_frame = results[0].plot()
        cv2.imshow('Detección', annotated_frame)
        
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
```

---

## 👂 Audición

### Hardware
- **Micrófonos**: Array de 4-6 micrófonos para localización de fuentes
- **Interfaz**: USB (Blue Yeti) o I2S (MEMS)

### Software
```python
import librosa
import numpy as np
from transformers import pipeline

# Reconocimiento de voz con Whisper
recognizer = pipeline("automatic-speech-recognition", model="openai/whisper-base")
result = recognizer("audio.wav")
print(result['text'])
```

---

## ✋ Tacto

### Hardware
- **FSR (Force Sensitive Resistors)**: Sensores de presión
- **Sensores capacitivos**: Detección de contacto
- **Encoders**: Retroalimentación de posición

### Aplicaciones
- Agarre adaptativo de objetos
- Detección de colisiones
- Interacción segura con humanos

---

## 🧭 Propiocepción y Equilibrio

### Hardware
- **IMU**: MPU6050, BNO055 (acelerómetro + giroscopio + magnetómetro)
- **Encoders**: En articulaciones para conocer ángulos

### Algoritmos
- **Filtro de Kalman**: Fusión de acelerómetro y giroscopio
- **Filtro Complementario**: Alternativa más ligera
- **PID**: Control de postura

---

## 🔗 Conexiones con Otros Módulos

- **[03_Localizacion_Mapeo](../03_Localizacion_Mapeo/)**: Usa datos de visión y sensores para SLAM
- **[04_Planificacion_Control](../04_Planificacion_Control/)**: Recibe datos sensoriales para control
- **[05_Aprendizaje_IA](../05_Aprendizaje_IA/)**: Entrena modelos de reconocimiento visual
- **[00_Fundamentos](../00_Fundamentos/)**: Teoría de procesamiento de señales y visión

---

## 📚 Recursos

### Datasets de Visión
- **COCO**: Common Objects in Context
- **ImageNet**: Clasificación de imágenes
- **KITTI**: Conducción autónoma y SLAM
- **LFW**: Labeled Faces in the Wild

### Librerías Principales
```python
import cv2                      # OpenCV
from ultralytics import YOLO    # YOLO v8
import torch
from torchvision import models
import pyrealsense2 as rs       # Intel RealSense
import librosa                  # Audio processing
import mediapipe as mp          # Pose/hand tracking
```

---

## 🎯 Próximos Pasos

1. Implementar sistema de detección de objetos en tiempo real
2. Calibrar cámaras estéreo para percepción de profundidad
3. Integrar reconocimiento facial con base de datos
4. Desarrollar fusión sensorial multimodal
5. Optimizar para ejecución en hardware embebido (Jetson Nano/Xavier)
