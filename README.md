# Generador de entrevistas estructuradas por competencias

Aplicación web para recruiters y profesionales de Recursos Humanos. A partir de la información de una vacante, genera una guía de entrevista estructurada con preguntas de comportamiento basadas en la metodología STAR (situación, tarea, acción y resultado).

## Funcionalidades

- Formulario completo de la vacante: puesto, departamento, seniority, descripción, competencias, formación, conocimientos, duración e información adicional.
- Ocho competencias predefinidas y posibilidad de añadir competencias personalizadas.
- Entre 5 y 20 preguntas principales, distribuidas de forma equilibrada entre las competencias.
- Para cada pregunta: objetivo, entre 2 y 4 preguntas de profundización e indicadores de respuesta sólida e insuficiente.
- Escala homogénea de evaluación de 1 a 5.
- Campos de notas y puntuación para utilizar la guía durante la entrevista.
- Descarga de la guía en Markdown y TXT.
- Validación del formulario, salida estructurada y mensajes de error comprensibles.
- La clave de API se lee desde los secretos de Streamlit o desde una variable de entorno; nunca aparece en la interfaz.

## Requisitos

- Python 3.10 o posterior.
- Una clave de la API de OpenAI con acceso a un modelo compatible con salidas estructuradas.

## Instalación

1. Crea y activa un entorno virtual:

   **Windows (PowerShell)**

   ```powershell
   python -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

   **macOS o Linux**

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

2. Instala las dependencias:

   ```bash
   pip install -r requirements.txt
   ```

3. Crea el archivo local de secretos a partir del ejemplo:

   **Windows (PowerShell)**

   ```powershell
   Copy-Item .streamlit/secrets.toml.example .streamlit/secrets.toml
   ```

   **macOS o Linux**

   ```bash
   cp .streamlit/secrets.toml.example .streamlit/secrets.toml
   ```

4. Edita `.streamlit/secrets.toml` e introduce tu clave:

   ```toml
   OPENAI_API_KEY = "sk-tu-clave-real"
   OPENAI_MODEL = "gpt-4.1-mini"
   ```

   También puedes definir `OPENAI_API_KEY` y `OPENAI_MODEL` como variables de entorno. Los secretos de Streamlit tienen prioridad.

## Ejecución

Desde la carpeta del proyecto, ejecuta:

```bash
streamlit run app.py
```

Streamlit abrirá la aplicación en el navegador. Si no lo hace automáticamente, utiliza la dirección local que aparezca en la terminal, normalmente `http://localhost:8501`.

## Uso

1. Completa el nombre y la descripción del puesto.
2. Selecciona al menos una competencia o añade una personalizada.
3. Elige el número de preguntas y la duración disponible.
4. Pulsa **Generar entrevista**.
5. Revisa la guía antes de usarla y descárgala en Markdown o TXT si necesitas compartirla.

El número de preguntas debe ser igual o superior al número de competencias seleccionadas, ya que la aplicación genera al menos una pregunta por competencia.

## Configuración del modelo

El modelo se configura con `OPENAI_MODEL`; por defecto se utiliza `gpt-4.1-mini`. Puedes sustituirlo por otro modelo de tu cuenta que admita salidas estructuradas. La aplicación usa la API Responses y valida la respuesta con modelos Pydantic.

Consulta la [documentación oficial sobre salidas estructuradas](https://developers.openai.com/api/docs/guides/structured-outputs?api-mode=responses) para conocer la compatibilidad actual de modelos.

## Seguridad y uso responsable

- No subas `.streamlit/secrets.toml` al repositorio. Ya está incluido en `.gitignore`.
- Evita incluir datos personales innecesarios en los campos del formulario.
- Revisa siempre la guía generada antes de utilizarla.
- Evalúa evidencias relacionadas con el puesto y aplica la misma estructura a todas las personas candidatas.
- La herramienta apoya la preparación de la entrevista; no debe tomar decisiones de contratación de forma autónoma.

## Estructura

```text
.
├── app.py
├── requirements.txt
├── README.md
├── .gitignore
└── .streamlit/
    └── secrets.toml.example
```

