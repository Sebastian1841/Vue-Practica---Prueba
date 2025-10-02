# 📌 Proyecto GPS-Vue

Este proyecto es una **aplicación web desarrollada con Vue 3, PrimeVue e Interact.js**, que permite **visualizar datos de GPS en tiempo real** mediante **tablas y gráficos dinámicos**. Además, los usuarios pueden **mover y redimensionar tarjetas (cards)** en el panel, y los cambios se guardan en un **backend desarrollado con Flask (Python)**.

---

## 🚀 Tecnologías utilizadas

### Frontend

* **Vue 3** → Framework principal.
* **PrimeVue** → Librería de componentes UI.
* **Chart.js** → Visualización de datos en gráficos.
* **Interact.js** → Hacer que las tarjetas sean **arrastrables y redimensionables**.
* **Mitt (eventBus)** → Comunicación global entre componentes.

### Backend

* **Flask** → API REST que sirve datos de GPS y gestiona las posiciones de las tarjetas.
* **Flask-CORS** → Permite comunicación entre frontend y backend.
* **Python (random, datetime)** → Generación de datos simulados.

---

## 📂 Estructura del proyecto

```
gps-vue/
│── public/                 # Archivos estáticos
│── src/
│   ├── components/          # Componentes reutilizables
│   │   ├── AppFooter.vue
│   │   └── AppHeader.vue
│   ├── layouts/             # Plantillas base
│   │   └── Default.vue
│   ├── router/              # Configuración de rutas
│   │   └── index.js
│   ├── Utils/               # Utilidades (EventBus)
│   │   └── eventBus.js
│   ├── Views/               # Vistas principales
│   │   ├── Home.vue
│   │   └── About.vue
│   ├── App.vue              # Componente raíz
│   └── main.js              # Punto de entrada
│
│── simulacion de datos/
│   └── simulacion.py        # Backend en Flask (API de GPS y cards)
│
│── package.json             # Dependencias del proyecto
│── vite.config.js           # Configuración de Vite
```

---

## ⚙️ Funcionalidades principales

### 🔹 **Frontend**

* **Menú de navegación** con rutas dinámicas (`Home` y `About`).
* **Panel de tarjetas (cards)**:

  * Cada tarjeta puede contener:

    * Una tabla con datos GPS (`DataTable` de PrimeVue).
    * Un gráfico de barras (`Chart.js`).
    * Contenido vacío.
  * Se pueden **mover y redimensionar** con `Interact.js`.
* **Modo edición**:

  * Botón "Editar" → habilita mover/redimensionar.
  * Botón "Cancelar" → deshabilita edición.
* **Persistencia de estado**:

  * Las posiciones y tamaños de las tarjetas se guardan en el backend (`/cards/reorder`).

### 🔹 **Backend (Flask)**

* **`/gps`** → Retorna datos simulados de GPS con:

  * Marca de tiempo.
  * ID de GPS (`GPS_1`, `GPS_2`, `GPS_3`).
  * Latitud y longitud.
  * Velocidad (km/h).
  * Dirección (NORTE, SUR, ESTE, OESTE, etc.).
* **`/cards`** → Retorna la configuración actual de las tarjetas.
* **`/cards/reorder`** → Guarda nuevas posiciones/tamaños de las tarjetas.

---

## ▶️ Instalación y ejecución

### 1. Clonar el repositorio

```bash
git clone https://github.com/usuario/gps-vue.git
cd gps-vue
```

### 2. Instalar dependencias del frontend

```bash
npm install
```

### 3. Ejecutar el frontend

```bash
npm run dev
```

El proyecto se levantará en:
👉 `http://localhost:5173`

### 4. Ejecutar el backend (Flask)

Ir a la carpeta `simulacion de datos` y correr el servidor:

```bash
cd "simulacion de datos"
python simulacion.py
```

El backend correrá en:
👉 `http://127.0.0.1:5000`

---

## 📊 Ejemplo de endpoints del backend

* **Obtener datos GPS**
  `GET http://127.0.0.1:5000/gps`

* **Obtener configuración de cards**
  `GET http://127.0.0.1:5000/cards`

* **Guardar nueva configuración**
  `POST http://127.0.0.1:5000/cards/reorder`
  (se envía el JSON con posiciones y tamaños)

---

## 🔮 Próximos pasos / mejoras

* Autenticación de usuarios.
* Historial de movimientos GPS.
* Personalización de dashboards por usuario.
* Persistencia en **base de datos** (actualmente en memoria).

---

## 👨‍💻 Autor

Proyecto desarrollado por Sebastián Suazo como práctica de **Vue.js + Python Flask**.
