
# EV CHARGE - API REST

## ⚡ Descripción
El sistema titulado como EV Charge, esta centrado en convertir la movilidad electrica en algo mas factible haciendo que sea mejor la recarga de los vehiculos electricos
a nivel Colombia guiando a los usuarios a mas puntos de recarga como lo son las electrolineras, el mayor objetivo es poder llegar a expandir nuestro servicio a profundidad globalmente.
El sistema busca eliminar los problemas de compatibilidad de conectores, permitiendo a los usuarios ubicar puntos de carga disponibles en tiempo real, filtrar por tipo de conector, 
gestionar reservas, registrar vehículos y consultar historiales de consumo, ofreciendo a su vez trazabilidad operativa y analítica para los operadores.


--- 

## 🛠️ Tecnologías Utilizadas

* **Lenguaje:** Python 3.12+
* **Framework Principal:** FastAPI (Alto rendimiento y documentación automática)
* **Servidor Web:** Uvicorn (Motor Asíncrono de Ejecución)
* **Base de Datos / ORM:** PostgreSQL / SQLAlchemy
* **Seguridad:** JWT (JSON Web Tokens) + Bcrypt / Python-Multipart (Encriptación de credenciales)

---

## 📂 Estructura del Proyecto

```text
Avanze-react-native-main/
├── J-K/                          ← Backend + frontend web (EV Charge)
│   ├── app/                      ← Backend FastAPI (Python)
│   │   ├── main.py               ← Punto de entrada: CORS, routers, creación/ajuste de tablas
│   │   ├── config/database.py    ← Conexión SQLAlchemy (PostgreSQL)
│   │   ├── models/               ← Tablas: usuario, vehiculo, reserva, carga, compra,
│   │   │                           calificacion, favorito, metodo_pago, notificacion,
│   │   │                           reporte, contacto, estacion_propia, estacion_cargador,
│   │   │                           estado_estacion
│   │   ├── schemas/              ← Esquemas Pydantic (validación de entrada/salida)
│   │   ├── controllers/          ← Lógica de negocio por módulo
│   │   ├── routes/               ← Endpoints (auth, admin, mapa, reservas, pagos,
│   │   │                           asistente, olvidar contraseña, etc.)
│   │   ├── services/             ← asistente_service, email_service, tarifas_service
│   │   ├── middleware/           ← error_handler.py
│   │   ├── utils/                ← jwt, security, response, content_filter
│   │   └── img/                  ← logo e imagen
│   │
│   ├── frontend/                 ← SPA React + TypeScript + Vite
│   │   ├── index.html
│   │   ├── vite.config.ts, tsconfig*.json, package.json
│   │   ├── public/               ← HTML/CSS originales (admin, dashboard, mapa) e imágenes
│   │   └── src/
│   │       ├── main.tsx, App.tsx
│   │       ├── routes/AppRouter.tsx   ← Rutas con lazy loading + RutaPrivada / RutaAdmin
│   │       ├── context/AuthContext.tsx
│   │       ├── api/              ← Un cliente por módulo + httpClient (axios)
│   │       ├── components/       ← AuthModal, ModalPago, AsistenteChat,
│   │       │                       GlobalNotifications, MetodoPagoForm, Productos...
│   │       ├── features/         ← admin, dashboard, dashboard-usuario (calificaciones,
│   │       │                       favoritos, metodos-pago, reservas, vehiculos),
│   │       │                       mapa, productos, landing, auth
│   │       ├── styles/           ← CSS por sección (admin, dashboard, mapa, responsive)
│   │       ├── utils/contentFilter.ts
│   │       └── types/, layouts/
│   │
│   ├── .github/workflows/ci.yml
│   ├── requirements.txt
│   ├── .env.example
│   └── README.md, LOGIN_RESERVAS_GUIDE.md, PROFILE_FEATURE_GUIDE.md
│
└── mobile/                       ← App Expo (SDK 57) + React Native 0.86
    ├── index.ts, App.tsx, app.json
    ├── package.json
    ├── .env, .env.example
    ├── CLAUDE.md, AGENTS.md, .claude/settings.json
    ├── assets/                   ← Iconos, splash, imágenes de productos y secciones
    └── src/
        ├── screens/HomeScreen.tsx
        ├── components/           ← Header, Hero, About, Services, Categories, Stats,
        │                           Faq, Contact, Footer (secciones de la landing),
        │                           AuthModal, MapPreviewModal
        ├── api/                  ← auth, contacto, mapa, notificaciones + httpClient
        ├── context/AuthContext.tsx
        ├── theme/                ← colors.ts, spacing.ts
        └── types/index.ts
---
🚀 Guía de Instalación y Despliegue
## 1. Clonar el Repositorio

Abre tu terminal y descarga el proyecto en tu máquina:

```
git clone git@github.com:tu_usuario/ev-charge-backend.git
```

Ingresa a la carpeta raíz del proyecto:
Bash
```
cd ev-charge-backend
```
---
## 2. Configurar el Entorno Virtual (.venv)

    Nota: Nunca compartas ni arrastres carpetas .venv creadas en otros equipos. Constrúyelo desde cero localmente.

En Linux / Ubuntu:
Bash
```
python3 -m venv .venv
source .venv/bin/activate
```
En Windows (PowerShell / CMD):
Bash
```
python -m venv .venv
.venv\Scripts\activate
```
---
## 3. Instalar Dependencias

Con el entorno virtual activado ((.venv) visible en tu prompt), ejecuta:
Bash
```
pip install -r requirements.txt
```
---
## 4. Configurar Variables de Entorno (.env)

Crea un archivo llamado .env en la raíz del proyecto basándote en los datos de tu base de datos:
Fragmento de código
```
DB_HOST=127.0.0.1
DB_PORT=5432  # 3306 si usas MariaDB/MySQL
DB_NAME=ev_charge_db
DB_USER=postgres
DB_PASSWORD=tu_contraseña_segura
SECRET_KEY=tu_clave_secreta_para_jwt
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
```
---
## 5. Ejecutar la Aplicación

Lanza el servidor local en modo de desarrollo:
Bash
```
uvicorn main:app --reload --app-dir app
```

📡 Acceso y Consumo de la API

Una vez encendido el servidor, puedes interactuar con el backend desde los siguientes enlaces locales:

    Swagger UI (Interactiva): http://127.0.0.1:8000/docs (Ideal para probar métodos HTTP directamente).

    ReDoc (Documentación estática): http://127.0.0.1:8000/redoc

---
🚨 Solución de Problemas Frecuentes (Troubleshooting)
## 1. El entorno virtual no se activa o da error de rutas

    Causa: Intentaste reutilizar una carpeta .venv copiada de otra computadora, cambiando las rutas absolutas internas o el sistema operativo.

    Solución: Borra la carpeta por completo (rm -rf .venv) y vuelve al paso 2 del manual para generarla limpia.

## 2. Error 500 Internal Server Error al registrar o loguear usuarios

    Causa: Conflicto de compatibilidad entre la librería tradicional de bcrypt y las versiones más recientes de Python (como Python 3.12).

    Solución: Asegúrate de desinstalar bcrypt e instalar la variante compatible instalando passlib[bcrypt] o actualizando las dependencias nativas del entorno.

### 3. Error 401 Unauthorized constante en las rutas protegidas

    Causa: Estás olvidando enviar el token en la cabecera, expiró su tiempo de vida, o lo estás estructurando mal.

    Solución: En tu cliente HTTP (Thunder Client / Postman), ve a la pestaña Auth, selecciona Bearer Token y pega el access_token generado sin comillas ni espacios adicionales.

4. Error 422 Unprocessable Entity

    Causa: Los datos que estás enviando en el JSON (Body) no cumplen con las reglas estructuradas en los esquemas de Pydantic (ej: un correo mal escrito o un campo faltante).

    Solución: Revisa la pestaña de la respuesta para ver el detalle exacto del campo que falló la validación.
---
🔄 Flujo de Trabajo en Git

Si realizas cambios en el código o agregas nuevas librerías:
Bash

# Si instalaste una nueva librería, actualiza el archivo de requisitos:
pip freeze > requirements.txt

# Flujo estándar para subir tus cambios:
```
git status
git add .
git commit -m "feat: agrega validación de token a rutas de electrolineras"
git push origin tu_rama
```
---
👥 Equipo de Desarrollo (ADSO)

    Juan Esteban Campos Herrera

    Kevyn Andres Roa

    Julian Estiben Cruz

    Jhon Alexander Muñoz

    Nicolas Stiven Beltran
