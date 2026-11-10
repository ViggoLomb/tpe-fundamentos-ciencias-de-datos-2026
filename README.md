# Trabajo Práctico Especial — Fundamentos de la Ciencia de Datos (2026)

**Análisis de Factores de Riesgo en la Población Argentina — ENFR 2018**  
**Grupo 28**:
- Santamarina, Alejo
- Lombardi, Viggo
- Centurión, Nicolás

**Ayudante Asignada:** Rosana Cepeda

---

## Descripción del Proyecto

Este repositorio contiene el desarrollo completo del Trabajo Práctico Especial de la materia *Fundamentos de la Ciencia de Datos* (Cursada 2026). El objetivo es realizar un análisis exploratorio detallado, operaciones de limpieza y validación rigurosa de 6 hipótesis estadísticas sobre la **4ª Encuesta Nacional de Factores de Riesgo (ENFR 2018)** elaborada por el INDEC y la Secretaría de Gobierno de Salud.

Dado que la ENFR posee un diseño muestral complejo (muestreo probabilístico, polietápico y estratificado por conglomerados con selección en 3 pasos), todas las estimaciones poblacionales, intervalos de confianza, contrastes de hipótesis y modelos lineales incorporan la técnica oficial de **pesos replicados mediante bootstrap** (200 réplicas por registro para los factores de expansión `wf1p`, `wf2p` y `wf3p`).

---

## Estructura del Repositorio

```text
.
├── TPE.ipynb                                    # Única notebook de Jupyter con todo el código y gráficos
├── Informe_TPE_Grupo28.pdf                     # Informe final detallado de hallazgos y conclusiones
├── requirements.txt                             # Dependencias del entorno de Python
├── README.md                                    # Instrucciones de instalación y ejecución local
├── .gitignore                                   # Archivos excluidos del control de versiones
├── ENFR2018_baseusuario.zip                     # Base de datos oficial de la ENFR 2018 (INDEC)
└── base_replicas_enfr2018.zip                   # Pesos replicados para estimación de varianza (INDEC)
```

---

## Requisitos del Sistema

- **Python:** Versión 3.10 o superior (recomendado Python 3.11 / 3.12).
- **Herramientas:** `pip` y `git`.

---

## Instrucciones para Clonar y Ejecutar Localmente Desde Cero

### 1. Clonar el repositorio
Abrir una terminal y clonar el repositorio:
```bash
git clone https://github.com/ViggoLomb/tpe-fundamentos-ciencias-de-datos-2026.git
cd tpe-fundamentos-ciencias-de-datos-2026
```

### 2. Crear y activar el entorno virtual aislado

- **En Linux / macOS:**
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```

- **En Windows (PowerShell):**
  ```powershell
  python -m venv venv
  .\venv\Scripts\Activate.ps1
  ```

- **En Windows (CMD):**
  ```cmd
  python -m venv venv
  .\venv\Scripts\activate.bat
  ```

### 3. Instalar dependencias
Con el entorno virtual activado:
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Manejo de los Datos

El repositorio ya contiene los datasets necesarios para que el trabajo sea 100% autosuficiente y ejecutable offline:
1. `ENFR2018_baseusuario.zip`: Base de usuarios principal (Paso 1, 2 y 3). La Celda 2 de la notebook la detecta automáticamente y la descomprime en la carpeta local `ENFR2018_datos/`.
2. `base_replicas_enfr2018.zip`: Contiene las 200 réplicas oficiales de los factores de expansión de los pasos 1, 2 y 3. La notebook lee las réplicas directamente desde el comprimido local. Si por algún motivo el archivo se borra, la Celda 36 cuenta con un mecanismo de descarga automática fallback desde el servidor oficial de INDEC:
   - URL: `https://www.indec.gob.ar/ftp/cuadros/menusuperior/enfr/base_replicas_enfr2018.zip`

### 5. Ejecutar el Trabajo

Podés ejecutar la notebook de dos formas:

#### Opción A: Interfaz visual (Jupyter Notebook / JupyterLab)
```bash
jupyter notebook TPE.ipynb
```
En el menú superior, seleccionar **Cell** $\rightarrow$ **Run All** (o **Kernel** $\rightarrow$ **Restart & Run All**).

#### Opción B: Ejecución automatizada sin interfaz gráfica (CLI)
Para correr todas las celdas y verificar la ejecución desde la línea de comandos:
```bash
jupyter nbconvert --to notebook --execute TPE.ipynb --output TPE_resultado.ipynb
```

---

## Correspondencia entre Secciones de la Notebook y el Informe

Cada sección del informe escrito referencia formalmente la sección correspondiente de la notebook:

| Sección Notebook | Sección Informe | Contenido del Análisis |
| :--- | :--- | :--- |
| **1. Análisis exploratorio inicial** | **1. Introducción y 2. Análisis exploratorio** | Origen de datos, dimensiones temáticas, imputaciones y códigos especiales |
| ↳ `1.1` a `1.3` | Sec. 1 y 2 | Carga de datos, lectura de metadatos y tratamiento de inválidos/nulos |
| ↳ `1.4` (1.4.1 y 1.4.2) | Sec. 2 | Exploración general, distribuciones y detección inicial de outliers |
| **2. Selección y preparación** | **2. Análisis exploratorio de los datos** | Recorte de base y preparación de submuestras por pasos |
| ↳ `2.1` | Sec. 2 | Selección de variables clave del estudio |
| ↳ `2.2` (2.2.1 a 2.2.3) | Sec. 2 | Valores atípicos, distribuciones cuantitativas y actividad física |
| ↳ `2.3` (2.3.1 a 2.3.3) | Sec. 2 | Filtros por submuestras (Pasos 1, 2 y 3) y factores de expansión asociados |
| **3. Planteo de hipótesis** | **3. Hipótesis y resolución** | Justificación teórica y formulación estadística ($H_0$ vs $H_1$) |
| **4. Validación de hipótesis** | **3. Hipótesis y resolución (Resultados)** | Contraste empírico, inferencia y gráficos |
| ↳ `4.1` | Sec. 3.1 (Hipótesis 1) | **Univariada propia:** Perímetro de cintura en mujeres adultas (>88 cm, Paso 2) |
| ↳ `4.2` | Sec. 3.2 (Hipótesis 2) | **Bivariada propia:** Presión sistólica según nivel de actividad física (Paso 2) |
| ↳ `4.3` | Sec. 3.3 (Hipótesis 3) | **Multivariada propia:** Consumo diario de frutas/verduras e IMC controlado por edad y actividad |
| ↳ `4.4` | Sec. 3.4 (Hipótesis 4) | **Cátedra:** Consumo de frutas y verduras vs. recomendación OMS de 5 porciones (Paso 1) |
| ↳ `4.5` | Sec. 3.5 (Hipótesis 5) | **Cátedra:** IMC por medición física según niveles de actividad física (Paso 2) |
| ↳ `4.6` | Sec. 3.6 (Hipótesis 6) | **Cátedra:** Relación lineal múltiple entre glucemia en ayunas, IMC, presión, cintura y edad (Paso 3) |
