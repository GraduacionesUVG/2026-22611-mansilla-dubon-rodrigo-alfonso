# Mecanismos de Focalización Adaptativa Guiados por Representación Interna en Arquitecturas PIKANs

Trabajo de graduación — Ingeniería en Ciencias de la Computación, Universidad del Valle de Guatemala, 2026.

## Descripción

Las redes de Kolmogorov–Arnold informadas por física (PIKAN) aproximan soluciones de ecuaciones diferenciales mediante funciones univariadas entrenables. Este proyecto estudia si las señales internas de esas redes permiten orientar la focalización adaptativa del entrenamiento y cómo distinguir una señal útil de una asociación que no se mantiene entre problemas.

El trabajo incluye:

- **Línea base de seis problemas:** calor, Burgers, Allen–Cahn, dos configuraciones de Navier–Stokes y un bimorfo piezoeléctrico. Usa redes RBF-PIKAN y controles con perceptrón multicapa.
- **Diagnóstico de 272 señales internas** en 248 estados guardados del entrenamiento.
- **Mecanismo de focalización y precondicionamiento por arista.** Redujo el número de condición efectivo entre 60 y 120 veces y el error de Allen–Cahn en las diez semillas de cada coeficiente de difusión.

Es un proyecto de investigación, no una aplicación con interfaz. Por eso las capturas son figuras de resultados de los experimentos y la "ejecución" consiste en verificar el repositorio y recalcular las cifras citadas en el informe.

El código de este repositorio es una copia del repositorio de investigación público [AF_PIKANs](https://github.com/Rodrimansidub14/AF_PIKANs). La estructura de esa copia se describe en `src/README.md` y en el anexo "Repositorio" del informe.

## Tecnologías Utilizadas

- Python 3.12
- PyTorch (entrenamiento de RBF-PIKAN y MLP)
- NumPy, SciPy, pandas, scikit-learn, SymPy
- scikit-fem (referencias por elementos finitos)
- Matplotlib y Altair (figuras)
- Weights & Biases (registro de corridas)
- Kaggle y Modal (cómputo en GPU: T4, A100, H100)
- pytest (pruebas)
- LaTeX (informe final)

## Requisitos Previos

- Python 3.12
- Git
- Opcional, solo para repetir entrenamientos: una GPU con CUDA y cuentas de W&B, Kaggle o Modal

## Instalación

1. Clonar el repositorio:

   ```bash
   git clone https://github.com/GraduacionesUVG/2026-22611-mansilla-dubon-rodrigo-alfonso.git
   cd 2026-22611-mansilla-dubon-rodrigo-alfonso/src
   ```

2. Crear un entorno e instalar dependencias:

   ```bash
   python -m venv .venv
   # Windows: .venv\Scripts\activate    Linux/macOS: source .venv/bin/activate
   pip install -r requirements.txt
   pip install torch==2.14.1 --index-url https://download.pytorch.org/whl/cpu
   ```

3. Configurar variables de entorno (solo si se van a lanzar corridas en W&B o Kaggle):

   ```bash
   cp .env.example .env
   # Editar .env con las credenciales correspondientes
   ```

## Ejecución

Todos los comandos se ejecutan desde `src/`. Estos cuatro verifican el proyecto sin repetir ningún entrenamiento:

```bash
python tools/setup_git.py          # filtro que guarda los notebooks sin salidas
python tools/check_repo.py         # nombres, registro, tamaños y secretos
python tools/reproduce_numbers.py  # recalcula las cifras citadas desde los datos guardados
python -m pytest tests -q          # pruebas del código
```

`python tools/build_trace.py` regenera `experiments/TRAZA.md`, que cruza cada experimento con su estado, sus corridas y sus notebooks. Para lanzar un experimento, consultar `docs/REPRODUCIR.md` y el `spec.md` de cada carpeta en `experiments/`.

## Capturas

Las capturas se encuentran en [`/capturas`](capturas/) (12 figuras, en orden de lectura):

| Archivo | Contenido |
|---|---|
| `captura-01.png` | Calor: línea base RBF-PIKAN y convergencia con L-BFGS |
| `captura-02.png` | Calor: control frente a muestreo adaptativo por residuo (RAD), pareado por semilla |
| `captura-03.png` | Burgers: error L2 por etapa (Adam / L-BFGS) |
| `captura-04.png` | Allen–Cahn: error L2 por etapa, MLP frente a RBF |
| `captura-05.png` | Navier–Stokes 2D (cilindro): error frente a COMSOL |
| `captura-06.png` | Navier–Stokes DFG: error de campo y de coeficiente de arrastre |
| `captura-07.png` | Bimorfo piezoeléctrico: error frente a FEM |
| `captura-08.png` | Diagnóstico: matriz señal × problema |
| `captura-09.png` | EXP-0028: efecto por problema y brazo |
| `captura-10.png` | EXP-0028: correlación entre efecto y propiedades del problema |
| `captura-11.png` | EXP-0030: error por hardware en el bimorfo |
| `captura-12.png` | EXP-0030: cuotas de la traza por grupo durante el entrenamiento |

## Demo

El video demostrativo se encuentra en [`/demo/demo.mp4`](demo/demo.mp4).

## Documentación

- El informe final del proyecto está disponible en [`/docs/informe_final.pdf`](docs/informe_final.pdf).
- El consentimiento de uso de foto y video firmado se encuentra en [`/docs/consentimiento_firmado.pdf`](docs/consentimiento_firmado.pdf).

## Autores

- Rodrigo Alfonso Mansilla Dubón - 22611

Asesor: Ing. Daniel González. Supervisor: Ph.D. Gabriel Barrientos.

## Licencia

Código: Apache-2.0 (`src/LICENSE`). Documentos y datos derivados: CC BY 4.0 (`src/LICENSE-docs.md`).
