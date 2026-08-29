# Análisis de sueldos en IT en Argentina

¿Qué factores explican cuánto gana una persona que trabaja en tecnología en Argentina? Este es un proyecto personal donde intento responder esa pregunta con datos reales, en vez de con las cosas que uno escucha en el ambiente.

Lo hice siendo estudiante de Ingeniería en Sistemas, como forma de aprender análisis de datos de punta a punta: desde bajar un dataset crudo hasta sacar conclusiones que se puedan defender.

## De qué se trata

Partí de una pregunta general —qué mueve el sueldo en IT— y la bajé a seis hipótesis concretas y testeables (por ejemplo: ¿pesa más el seniority o la experiencia?, ¿cuánto influye cobrar en dólares?, ¿hay brecha de género?). Después fui comprobando cada una con estadística, y al final armé un modelo que mira todos los factores juntos.

## Los datos

Usé la **Encuesta de Sueldos de sysarmy / openqube (edición 2026.1)**, que releva sueldos del sector IT en Argentina. Son 4.939 respuestas.

- Fuente: https://sysarmy.com/blog/posts/resultados-de-la-encuesta-de-sueldos-2026-1/
- El CSV crudo no está en el repo (es dato de sysarmy, se baja de la fuente). Sí está la versión ya procesada en `data/processed/`.

## Qué hice

1. **Exploración:** entender el dataset (60 columnas) y ver con qué contaba para cada hipótesis.
2. **Limpieza:** seleccionar variables, manejar valores faltantes y preparar la columna de lenguajes (que venía con varios por celda).
3. **Análisis y estadística:** visualizaciones + un test para cada hipótesis, eligiendo el test adecuado según el caso.
4. **Modelo:** una regresión lineal para estimar el efecto de cada factor controlando los demás.

## Hallazgos principales

- **Cobrar en dólares hace una diferencia grande.** Los sueldos dolarizados tienen una mediana bastante más alta, y el efecto se sostiene incluso comparando gente del mismo seniority y experiencia.
- **El salto salarial más grande es llegar a Senior.** La diferencia se agranda al subir.
- **Hay brecha de género.** Los varones cis ganan más, y una parte de esa diferencia persiste aun controlando puesto y experiencia.
- **La experiencia importa, pero no lo explica todo.** Se asocia al sueldo, aunque más débilmente de lo que uno esperaría: hay gente con los mismos años ganando cosas muy distintas.
- **Los lenguajes mejor pagos son los menos comunes** (Go, Kotlin), probablemente más por el perfil de quien los usa que por el lenguaje en sí.

Una aclaración que atraviesa todo el proyecto: encontrar que dos cosas van juntas no significa que una cause la otra. Traté de mantener esa distinción en cada conclusión.

## Estructura del repo

```
analisis-sueldos-it/
├── data/
│   ├── raw/          # dato crudo (no versionado)
│   └── processed/    # dato limpio
├── notebooks/        # exploración, limpieza y análisis
├── visualizations/   # gráficos generados
├── requirements.txt
└── README.md
```

## Cómo correrlo

```bash
# Clonar el repo
git clone https://github.com/LautaroFlores47/analisis-sueldos-it.git
cd analisis-sueldos-it

# Crear entorno e instalar dependencias
python -m venv .venv
.\.venv\Scripts\Activate.ps1   # en Windows
pip install -r requirements.txt

# Bajar el CSV de la fuente y ponerlo en data/raw/
# Después abrir los notebooks con: jupyter lab
```

## Limitaciones

- Los datos son de una encuesta voluntaria, así que no son una muestra perfectamente representativa del sector.
- La parte de nivel educativo se analizó sobre el subconjunto que respondió esa sección (~36%).
- El análisis identifica asociaciones, no relaciones de causa-efecto.
- Los sueldos en dólares están convertidos a pesos, y el valor del dólar tomado puede variar entre respuestas.

---

Proyecto hecho con fines de aprendizaje. Cualquier comentario o corrección es bienvenido.
