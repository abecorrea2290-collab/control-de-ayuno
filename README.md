# Control de Ayuno

PWA de seguimiento de ayuno intermitente con fases metabólicas y registro de peso.

## Stack

- **Frontend**: HTML + CSS + JavaScript (sin frameworks)
- **Auth**: Firebase Authentication (Google)
- **Base de datos**: Firestore (datos por usuario, acceso offline)
- **PWA**: Service Worker + Web App Manifest
- **Deploy**: Vercel

## Funcionalidades

- ⏱ **Tracker** — calcula horas de ayuno, fase metabólica actual y proyectada
- 📋 **Historial** — guarda y consulta todos tus ayunos anteriores
- ⚖ **Peso** — registra tu peso con fecha/hora, gráfica de evolución y varianza

## Configuración de Firebase

1. Ve a [console.firebase.google.com](https://console.firebase.google.com)
2. Crea un nuevo proyecto
3. Activa **Authentication → Google** como proveedor
4. Crea una base de datos **Firestore** en modo producción
5. En **Configuración del proyecto → Tus apps**, agrega una app web y copia el objeto `firebaseConfig`
6. Pégalo en `index.html` (busca `REEMPLAZA_CON_TU_API_KEY`)

### Reglas de Firestore

Copia el contenido de `firestore.rules` en la consola de Firebase (Firestore → Reglas):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

### Dominio autorizado en Firebase Auth

En Firebase → Authentication → Settings → Authorized domains, agrega tu dominio de Vercel:
```
tu-proyecto.vercel.app
```

## Deploy en Vercel

1. Importa este repositorio en [vercel.com/new](https://vercel.com/new)
2. Framework Preset: **Other**
3. Root Directory: `/` (raíz)
4. Haz click en **Deploy**

## Desarrollo local

Abre `index.html` directamente en el navegador, o usa un servidor local:

```bash
npx serve .
```

---

Abraham · 2025
