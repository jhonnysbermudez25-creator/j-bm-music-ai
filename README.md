# J-BM Music AI

Web app en Node.js + Express para crear canciones originales con el modelo `lyria-3.5` de Google Gemini API. Incluye interfaz en español, descarga de audio MP3, acceso con clave privada y un límite sencillo de generaciones por dirección IP.

## Qué incluye

- Generación de canciones completas con Lyria 3.5 mediante la API oficial Interactions.
- Opciones para estilo, ambiente, idioma, tempo, duración orientativa y modo instrumental.
- Campo para usar letras originales del usuario.
- Reproductor y descarga MP3.
- Clave privada de acceso a la web (`APP_ACCESS_CODE`).
- La API key de Google solo existe como variable privada del servidor (`GEMINI_API_KEY`).
- Máximo de 3 generaciones por IP en una ventana de 24 horas dentro de una misma instancia. Es una barrera básica, no un límite de facturación garantizado.

## Estructura

```text
j-bm-music-ai/
├── public/
│   ├── app.js
│   ├── index.html
│   └── styles.css
├── .env.example
├── .gitignore
├── package.json
├── render.yaml
├── README.md
└── server.js
```

## Importante sobre el coste y la cuenta de Google

Lyria 3.5 no tiene nivel gratuito en la tabla oficial consultada. Google publica un precio de **US$0.08 por canción generada**. El precio, disponibilidad y requisitos pueden cambiar. Revisa siempre la página oficial antes de activar el servicio.

Como el propietario del proyecto es menor de edad, un padre, madre o tutor debe revisar las condiciones, crear/administrar el proyecto de Google, activar la facturación si corresponde y controlar el uso. No introduzcas datos de pago en este repositorio ni compartas claves en chats.

Documentación oficial:
- Música con Lyria 3.5: https://ai.google.dev/gemini-api/docs/music-generation
- Precios de Gemini API: https://ai.google.dev/gemini-api/docs/pricing
- Claves de API: https://ai.google.dev/gemini-api/docs/api-key

## Despliegue en Render desde GitHub

1. Descarga y descomprime este proyecto.
2. Entra a tu repositorio de GitHub `jhonnysbermudez25-creator/j-bm-music-ai`.
3. Selecciona **Add file → Upload files** y sube el contenido de la carpeta descomprimida, respetando la carpeta `public/`. No subas el ZIP como único archivo: GitHub no lo descomprime automáticamente.
4. Confirma los cambios con **Commit changes** en la rama `main`.
5. En Render, abre el Dashboard y elige **New → Blueprint**. Conecta el repositorio y Render detectará el archivo `render.yaml`.
6. Render solicitará completar las variables secretas. Configura `GEMINI_API_KEY` y `APP_ACCESS_CODE` allí. No las escribas en `render.yaml`, `README.md`, ni en archivos de GitHub.
7. Aplica el Blueprint y espera a que termine el despliegue. El plan indicado en `render.yaml` es `free`, sujeto a los límites vigentes de Render.
8. Abre la URL `*.onrender.com` creada por Render. Introduce el `APP_ACCESS_CODE` que el administrador configuró.

También puedes crear un **New → Web Service** manualmente con estos valores:

- Repository: `jhonnysbermudez25-creator/j-bm-music-ai`
- Branch: `main`
- Runtime: `Node`
- Build command: `npm install`
- Start command: `npm start`
- Health check path: `/healthz`
- Plan: `Free` para probar, si está disponible en tu cuenta.

Luego agrega las dos variables secretas en **Environment** y despliega.

## Cómo crear las variables secretas

- `GEMINI_API_KEY`: clave de Gemini API creada y administrada por el adulto responsable en Google AI Studio. Usa una clave vigente del tipo que Google requiera actualmente.
- `APP_ACCESS_CODE`: contraseña aleatoria privada de al menos 16 caracteres. Esta es la contraseña de entrada a J-BM Music AI; no es la clave de Google.

En Render: abre el servicio → **Environment** → **Add Environment Variable**. Guarda las variables y vuelve a desplegar si Render no lo hace automáticamente.

## Ejecutar localmente (opcional)

Requiere Node.js 20 o superior.

```bash
npm install
cp .env.example .env
```

Edita `.env` y completa las dos variables, sin compartirlas. Después ejecuta:

```bash
npm start
```

Abre `http://localhost:3000`.

## Seguridad y límites

- Nunca pongas la clave de Google en `public/`, HTML, JavaScript del navegador ni archivos versionados.
- El acceso privado es una barrera básica para uso personal, no un sistema empresarial de cuentas.
- El límite de 3 canciones por IP es local a cada instancia y puede reiniciarse cuando el servicio se reinicia. No reemplaza límites o alertas de facturación de Google.
- Render Free puede apagar el servicio por inactividad; el primer acceso posterior puede tardar en despertar.
- No se guardan canciones en el servidor; descarga el MP3 antes de cerrar la página.
