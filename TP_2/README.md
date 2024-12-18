Repositorio de GitHub: https://github.com/flaibani/NLP.git

---------------------

El acceso a las carpetas que se detallan a continuación, se realiza  dentro del código, utilizando gdown_folder.

Carpetas que contiene los documentos utilizados como fuentes de datos: documents

 https://drive.google.com/drive/folders/1e-JD7z4DdPpQP5F4-KKyxNY6mPs82yfy?usp=sharing

Carpeta que contiene las bases de datos de grafos y tabular utilizadas como fuentes de contexto en el RAG:
context_data 

https://drive.google.com/drive/folders/1IS-kaXqyuyg77FF0n-bBmAObjG41cKmd?usp=sharing

Carpeta que contiene las bases de datos vectorial utilizada como fuentes de contexto en el RAG:
chroma_data 

https://drive.google.com/drive/folders/1syxhZGaejct7oC2FNNPSHvv_OuyrfUxU?usp=sharing

---------------------

Para la ejecución del código utilice su token de Hugging Face.

En el código, Sección: Configuraciones / HUGGINGFACE_TOKEN:

api = HUGGINGFACE_TOKEN
client = InferenceClient(api_key=api_key)

---------------------

Se puede ejecutar el código, evitando el costo de tiempo del procesamiento inicial de los datos, basta con correr las siguiente secciones:

RAG

* Instalaciones
* Librerías
* Configuraciones
* Generación de contexto
* Clasificadores
* Chatbot
* Interacción con el usuario
----------------
Agente ReAct

* Instalaciones
* Librerías
* Configuraciones
* Generación de contexto
* Agente


