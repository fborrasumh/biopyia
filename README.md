# BioPyIA

Bioestadística con Python y casos clínicos. Aplicación web de un solo fichero (`index.html`), continuación de PyMedIA.

**Idiomas:** español (por defecto), inglés y portugués; selector en la barra superior.

## Qué hace

- **30 misiones** que siguen los 26 temas de los módulos 2 a 4 del proyecto UNIDIGITAL-SIMUSTAT (temas 160 a 430): procesamiento de datos con pandas, análisis exploratorio, visualización, probabilidad, distribuciones, inferencia (intervalos y contrastes), datos categóricos y cuantitativos, no paramétricos y regresión lineal simple. Cada tema enlaza a su cuaderno de Colab y a su vídeo.
- **Datos clínicos sintéticos** (glucemias, presiones, ensayos, pruebas diagnósticas, analíticas…). Ningún dato es de un paciente real.
- **Python real en el navegador** (Pyodide 0.27.7 en un Web Worker): NumPy 2.0.2, pandas 2.2.3, SciPy 1.14.1, matplotlib 3.8.4 y statsmodels 0.14.4. No hay servidor ni nada que instalar.
- **Cada ejercicio se genera con una semilla**: cada estudiante recibe datos distintos y la misma semilla da siempre el mismo ejercicio.
- **El código corrige; la IA no.** Cada misión se comprueba ejecutando una solución de referencia con los mismos datos y con **casos ocultos** (otros datos), de modo que escribir el resultado «a mano» no basta. Se aceptan **otras formas válidas** de resolver el ejercicio (por ejemplo, `smf.ols` en lugar de `linregress`).
- **Diagnóstico por recálculo.** Los errores típicos de la bioestadística (`np.std` con `ddof=0` en una muestra, `cdf` en vez de `sf`, p-valor bilateral sin duplicar, t en vez de z, error estándar combinado en un intervalo, OR confundido con RR, Student en vez de Welch, comparar pares sin ajustar, etc.) se declaran como variantes de la solución; si la salida del estudiante coincide con una, la app explica el fallo.
- **Refuerzo**, estrellas, puntos, niveles, racha y repaso espaciado (1, 3, 7 y 21 días con datos nuevos), como en PyMedIA.
- **Pistas fijas** por misión y **tutor de IA opcional** (OpenAI, Gemini o Claude, con la clave de cada persona) que nunca recibe la solución; su respuesta se filtra por código y antes del primer envío se muestra lo que sale.
- **Informe del estudiante** (Word, JSON, CSV) con registro encadenado SHA-256.
- **Profesorado:** verificación de informes recalculando cada solución con su semilla y **exámenes individualizados** (HTML, claves en CSV y preguntas cloze de Moodle).

## Privacidad

El código, el progreso y el informe se guardan solo en el navegador (IndexedDB). No hay servidor. Solo si se pide una pista a la IA salen el enunciado y el código del estudiante (con correos, DNI y teléfonos enmascarados), previo aviso con la muestra del envío. La clave de IA se guarda solo en el navegador.

## Límites

- **Necesita internet la primera vez.** Pyodide (≈ 14 MB sin comprimir) y los paquetes se descargan del CDN jsDelivr y después quedan en la caché del navegador. Pesos medidos de los paquetes: NumPy + pandas ≈ 9,5 MB; con SciPy ≈ 29 MB; statsmodels añade ≈ 31 MB y solo se carga en las misiones de ANOVA (410) y regresión (430); matplotlib y sus dependencias ≈ 9 MB.
- **Las soluciones de referencia viajan dentro del fichero**: quien lea el código fuente de la página puede verlas. Las pruebas ocultas y la verificación con semilla limitan el valor de copiarlas, pero no lo impiden. No es un sistema de examen con vigilancia.
- **El registro encadenado detecta ediciones del fichero; no es una prueba definitiva.** Lo importante es que el profesorado recalcule las soluciones con la semilla.
- **Tiempo máximo de ejecución: 10 s.** Un bucle infinito se corta y se explica.
- **Tolerancia al redondeo:** el corrector compara con tolerancias muy estrictas; en los ejercicios con cálculos encadenados el enunciado pide usar valores sin redondear en los pasos intermedios.
- **Temas no incluidos:** la web del proyecto contiene también los temas 240 (Seaborn), 320 (Monte Carlo), 440 (regresión múltiple) y 450 (regresión logística), que no forman parte de este esquema. Tampoco están los temas del Módulo 1 (véase PyMedIA).
- Los datos, las fórmulas y los umbrales son **didácticos**; no sustituyen a las guías clínicas ni al criterio estadístico del análisis de un estudio real.
- Los consejos del tutor de IA pueden equivocarse; la corrección del código la hace siempre el motor. No se ha probado con una clave real de IA (solo con respuestas simuladas, incluidas respuestas que intentan revelar la solución).
- La verificación de un informe supone la misma versión de la app y de Pyodide (se avisa si difieren).

## Pruebas realizadas

- **Motor (CPython con las versiones exactas de Pyodide):** 30 misiones × 100 semillas. La solución de referencia, sus casos ocultos y las 7 soluciones alternativas válidas pasan siempre; cada error típico se diagnostica (algunos, en menos del 100 % de las semillas por no cambiar el resultado en esos casos) y el resultado escrito a mano se rechaza.
- **Navegador (Chromium con Pyodide real y la CSP de producción):** 59 comprobaciones: ejecución con pandas, SciPy, matplotlib y statsmodels, errores típicos, bucle infinito, tutor de IA con respuestas que intentan filtrar la solución, informe, verificación del profesorado (incluido un fichero manipulado), exámenes reproducibles, idiomas y móvil.

## Autoría

Fernando Borrás Rocher (Universidad Miguel Hernández de Elche).

Ejercicios originales que siguen la secuencia de los módulos 2 a 4 («Procesado inicial de datos», «Probabilidad» y «Generalización de conclusiones») del proyecto UNIDIGITAL-SIMUSTAT (cuadernos de F. Borrás, F. Botella, I. Hernández, Mª A. Martínez Mayoral, J. Moltó y J. Morales; licencia CC BY-SA 4.0). No se reutiliza su texto, código ni cuestionarios; el esquema de temas y los enlaces a los cuadernos y vídeos son los de su web (https://unidigitalsimustat.umh.es/).

ORCID: Fernando Borrás Rocher [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573)

## Cómo citar

Borrás Rocher, F. (2026). *BioPyIA* (v1.0.0) [Software]. DOI: [10.5281/zenodo.23198314](https://doi.org/10.5281/zenodo.23198314)

## Desarrollo y pruebas

```bash
python3 build.py                                       # monta index.html desde src/ y forja/
ONLY='^m200-' python3 tests/logic_test.py 100          # motor: misiones × semillas (usar un entorno con las versiones de Pyodide)
PYODIDE_DIR=/ruta/pyodide NODE_MODULES=/ruta/node_modules python3 tests/browser_test.py   # navegador (Playwright)
python3 tests/gen_i18n.py && node tests/extrae_claves.js   # diccionarios en/pt y cobertura de claves
```

## Licencia

MIT. Véase [LICENSE](LICENSE).
