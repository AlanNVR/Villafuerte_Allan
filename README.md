# Evaluación Unidad IV — Ingeniería de Requisitos (ISR-401)

Repositorio de entrega de la **Evaluación de la Unidad IV** de la asignatura
Ingeniería de Requisitos. Contiene el documento fuente en LaTeX, los diagramas
UML elaborados en TikZ y las capturas del cuestionario del Sistema de Gestión
Académica (SGA).

---

## Datos de la entrega

| Campo | Detalle |
|---|---|
| **Universidad** | Universidad Técnica Estatal de Quevedo |
| **Facultad** | Facultad de Ciencias de la Computación |
| **Asignatura** | Ingeniería de Requisitos |
| **Evaluación** | Unidad IV — Modelado, especificación, validación y gestión de requisitos |
| **Alumno** | Villafuerte Rosero Allan Noe |
| **Curso** | 4to Software "A" |
| **Docente** | Ing. Guerrero Ulloa Gleiston Cicerón |
| **Repositorio** | https://github.com/AlanNVR/Villafuerte_Allan |

---

## Estructura del repositorio

```
Villafuerte_Allan/
├── Evaluacion_Unidad_IV.tex    # Documento fuente principal (LaTeX)
├── Evaluacion_Unidad_IV.pdf    # Documento compilado (6 páginas)
├── README.md                   # Este archivo — instrucciones de compilación
└── Figuras/
    ├── Imagen1.png             # Captura: resumen del cuestionario del SGA
    └── Imagen2.png             # Captura: revisión del intento en el SGA
```

> La carpeta `Figuras/` **debe** conservarse junto al archivo `.tex`, ya que las
> rutas de las imágenes están declaradas de forma relativa
> (`Figuras/Imagen1.png`, `Figuras/Imagen2.png`).

El PDF compilado se incluye en el repositorio para consulta directa, sin
necesidad de compilar. Aun así, se documenta a continuación el procedimiento
completo de compilación desde el código fuente.

---

## Contenido del documento

| Sección | Actividad | Técnica empleada |
|---|---|---|
| Carátula | Datos institucionales y URL del repositorio | — |
| Capturas | Evidencias del cuestionario del SGA | `graphicx` |
| **P1** | Modelo de datos — Diagrama de clases UML | TikZ (`shapes.multipart`) |
| **P2** | Modelo funcional — Diagrama de actividades | TikZ (carriles de responsabilidad) |
| **P3** | Modelo de comportamiento — Máquina de estados | TikZ (`fit`, `backgrounds`) |
| **P4** | Consistencia entre las tres perspectivas | Tabla de verificación cruzada |
| **P5** | Especificación con esquema de atributos | Tablas + ISO/IEC 25010 |
| **P6** | Priorización MoSCoW | Tabla justificada |

Los tres diagramas UML están construidos **íntegramente en TikZ**, es decir, se
generan como código vectorial durante la compilación; no se importan imágenes
externas para ellos. Las únicas imágenes del documento son las dos capturas del
SGA alojadas en `Figuras/`.

---

## Requisitos previos

Se necesita una distribución de LaTeX que incluya el soporte de idioma español:

| Sistema | Distribución recomendada | Instalación |
|---|---|---|
| Windows | MiKTeX o TeX Live | https://miktex.org / https://tug.org/texlive |
| Linux (Debian/Ubuntu) | TeX Live | `sudo apt install texlive-full` |
| macOS | MacTeX | https://tug.org/mactex |

### Paquetes utilizados

`inputenc`, `fontenc`, `babel` (español), `mathptmx`, `geometry`, `graphicx`,
`array`, `longtable`, `ragged2e`, `enumitem`, `caption`, `float`, `fancyhdr`,
`hyperref` y `tikz` con las librerías `shapes.geometric`, `shapes.multipart`,
`shapes.misc`, `arrows.meta`, `positioning`, `calc`, `fit` y `backgrounds`.

En una instalación mínima de TeX Live, el soporte de español debe añadirse
por separado:

```bash
sudo apt install texlive-lang-spanish
```

En MiKTeX los paquetes faltantes se descargan automáticamente durante la
primera compilación.

---

## Compilación

### Opción 1 — Línea de comandos (recomendada)

Clonar el repositorio y compilar con **dos pasadas** de `pdflatex`, necesarias
para resolver correctamente las referencias cruzadas y los contadores de
figuras y tablas:

```bash
git clone https://github.com/AlanNVR/Villafuerte_Allan.git
cd Villafuerte_Allan
pdflatex Evaluacion_Unidad_IV.tex
pdflatex Evaluacion_Unidad_IV.tex
```

El resultado sobrescribe el archivo `Evaluacion_Unidad_IV.pdf` en el directorio
raíz.

### Opción 2 — latexmk (automatiza las pasadas)

```bash
latexmk -pdf Evaluacion_Unidad_IV.tex
```

Para limpiar los archivos auxiliares generados (`.aux`, `.log`, `.out`, `.toc`):

```bash
latexmk -c
```

### Opción 3 — Editores gráficos

| Editor | Procedimiento |
|---|---|
| **Overleaf** | Subir el repositorio como proyecto (*New Project → Upload Project*), fijar `Evaluacion_Unidad_IV.tex` como documento principal y compilar con **pdfLaTeX** |
| **TeXstudio** | Abrir `Evaluacion_Unidad_IV.tex`, seleccionar pdfLaTeX como compilador y pulsar `F5` |
| **VS Code** | Con la extensión *LaTeX Workshop*, usar la receta `latexmk (pdflatex)` |

---

## Solución de problemas frecuentes

| Mensaje de error | Causa | Solución |
|---|---|---|
| `Unknown option 'spanish'` en babel | Falta el soporte de idioma español | Instalar `texlive-lang-spanish` (Linux) o permitir la descarga automática en MiKTeX |
| `File 'Figuras/Imagen1.png' not found` | La carpeta `Figuras/` no está junto al `.tex` | Verificar que se clonó el repositorio completo, sin mover archivos |
| `I do not know the key '/tikz/...'` | Falta una librería de TikZ | Comprobar que el bloque `\usetikzlibrary{...}` del preámbulo está íntegro |
| Numeración de figuras incorrecta | Solo se ejecutó una pasada | Ejecutar `pdflatex` una segunda vez o usar `latexmk` |

---

## Verificación de la compilación

Una compilación correcta produce un PDF de **6 páginas**, sin mensajes de error,
con la siguiente distribución:

| Página | Contenido |
|---|---|
| 1 | Carátula institucional |
| 2 | Capturas del cuestionario del SGA |
| 3 | P1 — Diagrama de clases |
| 4 | P2 — Diagrama de actividades |
| 5 | P3 — Máquina de estados y P4 — Consistencia entre perspectivas |
| 6 | P5 — Especificación de requisitos y P6 — Priorización MoSCoW |

El PDF resultante debe coincidir con el `Evaluacion_Unidad_IV.pdf` incluido en
el repositorio.

---

## Licencia

Trabajo académico de carácter evaluativo. Uso restringido a fines educativos.
