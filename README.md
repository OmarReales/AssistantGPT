# AssistantGPT

## Descripción

AssistantGPT es un asistente conversacional creado para ayudar a los estudiantes a comprender y aprender diversos temas. Este asistente utiliza el modelo Gemini de Google para generar respuestas claras, concisas y adaptadas al nivel del usuario. El asistente ofrece funcionalidades como explicaciones de temas y resúmenes de textos, diseñadas para facilitar el estudio y la comprensión.

## Requisitos Previos

Para ejecutar este notebook, necesitas lo siguiente:

- Python 3.8
- google-generativeai
- textwrap
- sys
- abc
- IPython

## Instalación de Dependencias

Puedes instalar las dependencias necesarias utilizando pip:

`pip install -U google-generativeai`

Otras dependencias deberían estar disponibles en tu entorno de Python por defecto. Si alguna falta, puedes instalarla con:

`pip install <nombre_biblioteca>`

## Instrucciones de Instalación

Para ejecutar este notebook, sigue estos pasos:
1. Clona el repositorio:
   `git clone https://github.com/OmarReales/AssistantGPT.git`
2. Navega al directorio del proyecto:
   `cd AssistantGPT`
3. Instala las dependencias necesarias:
   `pip install -U google-generativeai`
4. Abre el notebook AssistantAI.ipynb en Jupyter:
   `jupyter notebook AssistantAI.ipynb`
5. Asegúrate de configurar la clave API de Google en GOOGLE_API_KEY antes de ejecutar el notebook.

## Descripción del Código

1. **Configuración Inicial**
   Se importan las bibliotecas necesarias y se configura el modelo de Google Generative AI con la clave API del usuario.
   
   ```
      import google.generativeai as genai
      import textwrap
      import sys
      from google.colab import userdata
      from abc import ABC, abstractmethod
      from IPython.display import display, Markdown
      GOOGLE_API_KEY = userdata.get('GOOGLE_API_KEY')
      genai.configure(api_key = GOOGLE_API_KEY)
   ```

3. **Definición del Modelo**
  Se define el modelo de generación de contenido utilizando Gemini 1.5:

   ```
      generation_config = {
        "temperature": 0.5,
        "top_p": 0.95,
        "top_k": 64,
        "max_output_tokens": 8192,
        "response_mime_type": "text/plain",
      }
      model = genai.GenerativeModel(
        model_name="gemini-1.5-flash",
        generation_config=generation_config,
        system_instruction="Eres un asistente de estudio inteligente creado para ayudar a los estudiantes..."
      )
   ```

3. **Funciones Utilitarias**
   Funciones para formatear el texto en Markdown, manejar la entrada del usuario, y mostrar menús y opciones.
   - `to_markdown(text)`: Formatea texto para ser compatible con Markdown.
   - `cerrar()`: finaliza el programa
   - `continua(texto_pregunta)`: Pregunta al usuario si desea continuar.
   - `titulo(texto, largo)`: Genera un título centrado con guiones.
   - `isint(str_numero)`: Verifica si una cadena es un entero.
   - `leer_entero(mensaje, minimo, maximo)`: Lee un número entero dentro de un rango.

4. **Clase `studyAssistant`**
  Una clase abstracta que define el asistente de estudio:
   - `__init__()`: Inicializa el asistente con un nombre y opciones de menú
   - `consultar_asistente()`: Ofrece al usuario las opciones de estudiar un tema o generar un resumen.
   - `crear_resumen()`: Toma un tema y genera un resumen utilizando el modelo Gemini.
   - `explicar_tema()`: Explica un tema proporcionado por el usuario.
   - `consulta()`: Recibe la consulta del usuario.
   - `_interfaz()`: Muestra el menú principal y maneja las opciones seleccionadas.

5. **Función `main()`**
   La función principal del programa, que instancia el asistente y mantiene el flujo de interacción con el usuario.
   
   ```
   def main():
      asistente = studyAssistant()
      while True:
          print(titulo(f"Bienvenido a *{asistente.nombre()}*"))
          asistente.consultar_asistente()
          asistente._interfaz()
   ```
   
7. **Ejemplos de Uso**
   Para utilizar el asistente, ejecuta el script y sigue las instrucciones del menú. Puedes pedirle al asistente que te explique un tema o que genere un resumen de un texto     que le proporciones.
   
   `if __name__ == "__main__":
    main()
   `

## Contribución 
Para contribuir al proyecto:

1. Fork el repositorio.
2. Crea una nueva rama para tu función o corrección de errores (git checkout -b feature/nueva-funcionalidad).
3. Realiza tus cambios y haz commit (git commit -m 'Añadir nueva funcionalidad').
4. Empuja a la rama (git push origin feature/nueva-funcionalidad).
5. Abre un Pull Request en GitHub.

## Referencias

- Documentacion oficial de [Gemini API](https://ai.google.dev/gemini-api/docs?hl=es-419)
- Repositorio sobre generacion de prompts de [Ezequiel Tartaglia](https://github.com/EzequielTartaglia/Generacion-de-Prompts/tree/main)
