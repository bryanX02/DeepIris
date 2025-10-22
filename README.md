# DeepIris
**Trabajo de Fin de Grado de Ingeniería de Datos e Inteligencía Aritifical. Bryan Xavier Quilumba Farinango**

**Título:** DeepIris. Desarrollo de una aplicación Android con IA, para la detección de contenido específico en medios digitales. 

**Tutores:** Luis Javier García Villalba y Ana Lucila Sandoval Orozco.

**Wiki:** El desarrollo del proyecto puede serguirse con los articulos que subo a la [Wiki del repositorio](https://github.com/bryanX02/DeepIris/wiki).


### Resumen
El objetivo de este proyecto es el desarrollo de una aplicación móvil Android que utiliza algoritmos de *machine learning* para detectar contenido sensible, potencialmente ilegal, o contenido especificado por el usuario.

La solución se centrará en aplicar técnicas avanzadas de:
* Procesamiento de Lenguaje Natural (NLP) para texto.
* Visión por Computador para imágenes y vídeos.

Adicionalmente, se investigará la viabilidad de integrar la herramienta con aplicaciones de mensajería como Telegram o Signal.

### Tecnologías (plan provisional)

El proyecto se dividirá en dos grandes áreas tecnológicas: el entrenamiento de los modelos y el desarrollo de la aplicación móvil.

1. Entrenamiento de modelos (Python Stack): El desarrollo, entrenamiento y evaluación de los modelos de machine learning se realizará en Python. El stack tecnológico principal incluirá:

* TensorFlow y Keras: Para construir y entrenar las redes neuronales profundas (CNNs, Transformers).
* Hugging Face Transformers: Para implementar modelos NLP de última generación como BERT o RoBERTa.
* OpenCV: Para el preprocesamiento de imágenes y la extracción de fotogramas de vídeo.
* Scikit-learn: Para las métricas de evaluación de los modelos y tareas de machine learning clásicas.
* Pandas y NumPy: Para la manipulación y preprocesamiento de los datasets.

2. Aplicación móvil (Android Stack): La aplicación se desarrollará de forma nativa para Android utilizando Android Studio.

* Lenguaje: Kotlin, por ser el lenguaje moderno y preferido para el desarrollo en Android.
* Inferencia en dispositivo: TensorFlow Lite (TFLite), para cargar y ejecutar los modelos entrenados (.tflite) de forma eficiente y local en el dispositivo móvil.
* Base de datos local y externa: SQLite, para persistir las configuraciones del usuario o los resultados de los análisis. Y Firebase para el mantenimiento de usuarios.
* APIs externas: Se explorará el uso de Retrofit para la comunicación con APIs de mensajería (Telegram) si la integración resulta viable.

**[Arquitectura simple provisional](https://github.com/bryanX02/DeepIris/wiki/Arquitectura_simple)**

```mermaid
graph TD
    %% --- Definición de Estilos (Alto Contraste) ---
    classDef blockPipeline fill:#FFF8E1,stroke:#D84315,stroke-width:2px,color:#333
    classDef blockApp fill:#E1F5FE,stroke:#0288D1,stroke-width:2px,color:#333
    classDef blockCloud fill:#E8F5E9,stroke:#388E3C,stroke-width:2px,color:#333
    classDef io fill:#f0f0f0,stroke:#555,stroke-width:2px,color:#000
    
    %% --- Sub-elementos con Estilos ---
    classDef ml fill:#FFEB3B,stroke:#FBC02D,stroke-width:2px,color:#333
    classDef db fill:#B3E5FC,stroke:#0288D1,stroke-width:2px,color:#333
    classDef cloudDB fill:#FFCC80,stroke:#F57C00,stroke-width:2px,color:#333
    classDef cloudAuth fill:#FFCDD2,stroke:#D32F2F,stroke-width:2px,color:#333
    classDef cloudAPI fill:#D1C4E9,stroke:#512DA8,stroke-width:2px,color:#333
    classDef keras fill:#FFA726,stroke:#FB8C00,stroke-width:2px,color:#fff
    classDef huggingface fill:#A5D6A7,stroke:#388E3C,stroke-width:2px,color:#fff
    classDef opencv fill:#64B5F6,stroke:#1976D2,stroke-width:2px,color:#fff

    %% --- 1. Inputs Externos ---
    UserInput["INPUT <br> Usuario"]
    OutputDisplay["OUTPUT <br> Resultados en Pantalla"]

    %% --- Bloque 1: Pipeline de Entrenamiento (Python) ---
    subgraph B1 ["Bloque de Entrenamiento"]
        direction TB
        TF_Keras["TensorFlow / Keras <br> (CNNs)"]
        HF_Transformers["Hugging Face / Transformers <br> (NLP)"]
        OpenCV_Node["OpenCV <br> (Preprocesamiento de Imágenes y Vídeos)"]
        TF_Keras <--> HF_Transformers <--> OpenCV_Node
    end

    %% --- Bloque 2: Aplicación Android (On-Device) ---
    subgraph B2 ["Bloque de App Android"]
        direction TB
        App_UI["UI <br> (XML, Activities/Fragments)"]
        App_TFLite["Inferencia Local <br> (TensorFlow Lite)"]
        App_DB["Base de Datos Local <br> (Room/SQLite)"]

        App_UI --> App_TFLite
        App_TFLite --> App_DB
    end

    %% --- Bloque 3: Cloud Services (Backend) ---
    subgraph B3 ["Bloque de Cloud Services"]
        direction TB
        Cloud_Auth["Firebase Authentication"]
        Cloud_DB["Cloud Firestore"]
        Cloud_API["API Externas (Retrofit)"]

        Cloud_Auth <--> Cloud_DB <--> Cloud_API
    end

    %% --- Conexiones Verticales ---
    UserInput -->|Usa la App| App_UI
    B1 -->|Produce Modelo .tflite| App_TFLite
    App_UI -->|Sincroniza Datos| B3
    App_DB -->|Muestra Resultados| OutputDisplay

    %% --- Aplicación de Estilos ---
    class B1 blockPipeline
    class B2 blockApp
    class B3 blockCloud
    class UserInput,OutputDisplay io
    class TF_Keras keras
    class HF_Transformers huggingface
    class OpenCV_Node opencv
    class App_TFLite ml
    class App_DB db
    class Cloud_Auth cloudAuth
    class Cloud_DB cloudDB
    class Cloud_API cloudAPI

