# PromptVault AI — Deployment Guide (Railway)

## Estructura del proyecto

```
promptvault/
├── server.js          ← Express: sirve el frontend Y la API
├── package.json
├── .gitignore
└── public/
    └── index.html     ← Frontend (mismo servidor, sin CORS)
```

## Por qué ya no habrá problemas de conexión

El frontend es **servido por el mismo Express** que maneja la API.
Todas las llamadas usan rutas relativas (`/api/prompts`) → mismo origen → sin CORS.

---

## Pasos para desplegar en Railway

### 1. Sube el código a GitHub

```bash
cd promptvault
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/TU_USUARIO/promptvault.git
git push -u origin main
```

### 2. Crea el proyecto en Railway

1. Entra a [railway.app](https://railway.app) → **New Project**
2. Selecciona **Deploy from GitHub repo** → elige tu repo

### 3. Agrega PostgreSQL

1. En tu proyecto de Railway → **+ New** → **Database** → **Add PostgreSQL**
2. Railway crea la DB y **automáticamente** agrega `DATABASE_URL` como variable de entorno al servicio — no tienes que hacer nada más.

### 4. Verifica las variables de entorno

En el servicio de la app, ve a **Variables**. Deberías ver:
- `DATABASE_URL` → agregada automáticamente por Railway al conectar Postgres

Railway también inyecta `PORT` automáticamente.

### 5. Deploy

Railway hace el deploy automáticamente al hacer push. También puedes forzarlo con **Deploy** en el dashboard.

### 6. Listo ✅

Visita la URL que Railway te asigna. La tabla `prompts` se crea automáticamente al primer arranque.

---

## Migración desde la versión local (localStorage)

Si tenías prompts guardados en el navegador:
1. Abre la versión antigua → **Exportar** → Copia el JSON
2. En la nueva versión → **Importar** → Pega el JSON → Importar

---

## Variables de entorno necesarias

| Variable       | Descripción                          | Quién la pone        |
|----------------|--------------------------------------|----------------------|
| `DATABASE_URL` | Conexión a PostgreSQL                | Railway (automático) |
| `PORT`         | Puerto del servidor                  | Railway (automático) |

La API key de OpenRouter **no va al servidor** — se guarda en localStorage del navegador de cada usuario.
# promptvault
