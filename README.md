# laberinto-inundaciones-ia

Práctica 2 — *Cuando el camino más corto no es el mejor*. Simulación de rutas seguras ante una inundación: un agente debe llegar a un refugio sobre un terreno con niveles de riesgo y zonas bloqueadas, y se comparan **BFS**, **Dijkstra** y **A\***.

Todo el código está en un solo notebook: [`laberinto_inundaciones_ia.ipynb`](laberinto_inundaciones_ia.ipynb).

## Cómo reproducirlo

**En Google Colab:** abrir el notebook desde GitHub (*Archivo → Abrir cuaderno → GitHub*) y ejecutar *Entorno de ejecución → Ejecutar todo*.

**En local:**

```bash
pip install -r requirements.txt jupyter
jupyter notebook laberinto_inundaciones_ia.ipynb
```

Solo se necesita Python 3 y `matplotlib`. No hay datos externos: los terrenos se construyen en el propio notebook y los aleatorios usan **semillas fijas**, por lo que los costos, pasos y nodos expandidos son reproducibles. Solo el tiempo en milisegundos depende de la máquina.

## Contenido del notebook

| Parte | Qué contiene |
|---|---|
| 1 | Modelo del terreno (matriz 12 × 16, niveles de inundación 0–4, costos de entrada) y visualización |
| 2 | BFS, Dijkstra y A\* (Manhattan), función de costo con `peso_riesgo` y validador de rutas |
| 3 | Pruebas 1–6: ruta disponible, zona bloqueada, refugio inaccesible, riesgo modificado, camino corto ≠ conveniente, casos borde |
| 4 | Pruebas avanzadas 7–13 y comparación consolidada (ver abajo) |
| 5 | Decisiones de diseño y declaración de uso de IA |

### Parte 4: pruebas avanzadas

| Prueba | Qué verifica |
|---|---|
| 7 | El validador de rutas rechaza rutas vacías, con saltos, diagonales, por celdas bloqueadas o fuera del mapa |
| 8 | 240 terrenos aleatorios (de 10 × 10 a 22 × 28) contra un oráculo independiente (SPFA): optimalidad, accesibilidad, costo recalculado a mano y A\* ≤ Dijkstra en nodos expandidos. Incluye una prueba de la prueba con un A\* defectuoso |
| 9 | Barrido del peso del riesgo: el punto en que el sistema abandona la ruta corta se predice con una fórmula y se compara con lo que hace el algoritmo |
| 10 | Muro de 20 × 20 con dos puertas: ambas abiertas, una bloqueada, ambas bloqueadas |
| 11 | Muro en U que engaña a la heurística Manhattan |
| 12 | Inundación progresiva con replanificación frente a plan estático |
| 13 | Las búsquedas no modifican el terreno y son deterministas |

Las cifras de los textos de la Parte 4 se calculan al ejecutar; las afirmaciones se comprueban con `assert`.

## Equipo

| Integrante | Responsabilidad |
|---|---|
| 1 | Terreno, matriz y niveles de inundación |
| 2 | BFS y Dijkstra |
| 3 | A\* y costos de riesgo |
| 4 | Pruebas, comparaciones y documentación |
