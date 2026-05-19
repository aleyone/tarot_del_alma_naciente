# Tarot del Alma Naciente

Web de tiradas de tarot con interpretación por IA.

## Estructura del proyecto

```
tarot-alma-naciente/
├── index.html          # Frontend completo (HTML + CSS + JS)
├── vercel.json         # Configuración de despliegue
├── api/
│   └── interpret.js    # Serverless Function — proxy seguro Anthropic
└── cards/
    ├── 01_EL_MAGO.png
    ├── 02_LA_SACERDOTISA.png
    └── ... (22 cartas)
```

## Despliegue en Vercel

### 1. Subir a GitHub

```bash
git init
git add .
git commit -m "Initial commit — Tarot del Alma Naciente"
git remote add origin https://github.com/TU_USUARIO/tarot-alma-naciente.git
git push -u origin main
```

### 2. Conectar con Vercel

1. Entra en [vercel.com](https://vercel.com) y haz clic en **Add New Project**
2. Importa el repositorio de GitHub
3. Deja la configuración por defecto (Vercel detecta el `vercel.json`)
4. Haz clic en **Deploy**

### 3. Configurar la API key de Anthropic

Esto es lo más importante — la API key NUNCA debe estar en el código.

1. En el dashboard de Vercel, ve a tu proyecto
2. **Settings → Environment Variables**
3. Añade:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** `sk-ant-...` (tu clave de Anthropic)
   - **Environment:** Production + Preview + Development
4. Haz clic en **Save**
5. Ve a **Deployments** y haz **Redeploy** para que coja la variable

### 4. Verificar

Una vez desplegado, la URL de Vercel ya funciona. La ruta `/api/interpret` es el proxy serverless que guarda la API key en el servidor.

## Desarrollo local

Para probar en local con la API funcionando:

```bash
npm i -g vercel
vercel dev
```

Esto levanta un servidor local que emula el entorno de Vercel, incluyendo las serverless functions. Necesitarás tener la API key en un archivo `.env.local`:

```
ANTHROPIC_API_KEY=sk-ant-...
```

> ⚠️ Nunca subas `.env.local` a GitHub. Está en el `.gitignore` automáticamente con Vercel CLI.

## Actualizar cartas

Las imágenes de las cartas están en `/cards/`. Para reemplazar la carta 14 (La Templanza) cuando tengas la versión final:

1. Nombra el archivo `14_LA_TEMPLANZA.png`
2. Sustitúyelo en la carpeta `cards/`
3. Haz commit y push — Vercel redespliega automáticamente
