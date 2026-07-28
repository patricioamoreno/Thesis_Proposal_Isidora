# Propuesta de Tesis — Proyecto LaTeX (Overleaf-ready)

## Cómo compilarlo
1. Sube esta carpeta completa a un proyecto nuevo de Overleaf (o clónala a tu GitHub y conéctala).
2. **Importante:** el compilador debe estar en **XeLaTeX** (no pdfLaTeX), porque se usa `fontspec`
   para la tipografía. En Overleaf: Menu → Settings → Compiler → XeLaTeX.
3. Overleaf compila automáticamente `main.tex` con `bibtex` para `references.bib` — no necesitas
   hacer nada adicional.

## Qué se hizo
- Se convirtió el documento completo (Word → LaTeX) desde el Capítulo 1 hasta el final de
  "Publishing Proposal" (todo el contenido antes de la lista de referencias).
- **Todas las citas del cuerpo se pasaron de formato autor-año a sistema numérico estilo IEEE**
  (`\cite{...}` con `\bibliographystyle{ieeetr}`, numeración por orden de aparición, ej. `[3,7,12]`).
- Los subtítulos 1.1–1.6, 1.3.1–1.3.3, etc. (que en el Word original eran texto en negrita/subrayado,
  no estilos de título reales) se convirtieron a `\subsection`/`\subsubsection` de verdad.
- La figura del Gantt (`image3.emf`, formato Windows no soportado por LaTeX) se convirtió a `.png`.

## Resultado de la prueba de páginas (Capítulo 1 → antes de referencias)

| Versión | Páginas |
|---|---|
| Word original (citas autor-año) | 12 |
| LaTeX con citas numeradas IEEE (sin recortes) | 11 |
| LaTeX + recortes de contenido administrativo/metodológico | 10 |
| + párrafo de síntesis, distinción DEM/continuo, hipótesis/objetivos reescritos | 11 |
| **+ ajuste de espaciado de títulos (`titlesec`, sin tocar texto)** | **10** ✅ |

Se aplicaron 4 recortes de contenido administrativo/metodológico (detalle de hardware, protocolo
PIV/PTV, mallado, redacción de 1.1) para llegar a 10 páginas. Luego, al incorporar las revisiones
de fondo (ver sección siguiente), el documento volvió a subir a 11 páginas; para recuperar las 10 sin
sacrificar ninguno de esos contenidos nuevos, se ajustó únicamente el espaciado antes/después de
los subtítulos (`\subsection`/`\subsubsection`, vía el paquete `titlesec`) — un cambio puramente de
layout, cero palabras eliminadas. Ningún recorte de contenido tocó la Hipótesis, los Objetivos
Específicos ni el contenido científico central de las secciones 1.3–1.6.

### Nota sobre la fuente
El Word original usa **Verdana 10pt** en el cuerpo (no 12pt como asumí al principio — lo corregí
tras medirlo directamente en el XML del docx). Verdana no está disponible en Overleaf/TeX Live, así
que usé **Liberation Sans** (clon métrico de Arial) como reemplazo más cercano. Si tu casa de
estudios exige una fuente específica, es un solo cambio en `main.tex` (línea `\setmainfont{...}`).

## Revisiones de contenido (revisión estilo comité doctoral)
Además de la conversión a LaTeX, se aplicaron las siguientes correcciones de fondo, surgidas de una
revisión crítica del Capítulo 1, la Hipótesis y los Objetivos:

1. **Párrafo de síntesis nuevo**, al cierre del Capítulo 1, que declara explícitamente la brecha
   única que ataca la tesis (antes había 4 brechas paralelas sin sintetizar).
2. **Distinción DEM vs. continuo** (nuevo párrafo, cierre de 1.5.2): se ubican explícitamente
   Chauchat (2013, modelo continuo Euler-Euler con reología µ(I)) y Maurin et al. (2015/2016,
   DEM acoplado a fluido 1D) como los dos enfoques existentes más cercanos, mostrando que ninguno
   mantiene ambos lados del acoplamiento resueltos con alta fidelidad simultáneamente — que es
   exactamente el aporte de esta tesis. Se agregaron ambas referencias completas al `.bib`.
3. **Hipótesis reescrita**: se separó la proposición causal/falsable (párrafo 1) de los valores
   numéricos esperados (párrafo 2, explícitamente etiquetados como "estimaciones de trabajo, no
   precondiciones"). El punto (iii) ya no depende de $u_\tau$ (que generaba una inconsistencia con
   el rango experimental de SO2) sino de $\phi_v$, consistente con (i) y (ii) y con el resto de la
   tesis.
4. **SO1 y SO2 reescritos** en modo "qué se busca saber" en vez de "qué se va a construir/medir" —
   el detalle metodológico que tenían ya vive en las secciones A2/A3 de Metodología.
5. **SO4 ajustado** para comprometerse explícitamente a determinar $\phi_v^{*}$ (el umbral crítico
   de la hipótesis (iii)), cerrando el círculo hipótesis→objetivo.
6. **SO5 reescrito sin "Bagnold"**: se reemplazó por el vocabulario de reología granular
   ($\mu(I)$) ya introducido en 1.1/1.2, evitando introducir un concepto nuevo sin desarrollo previo
   en el estado del arte.
7. **Sección de Novedad Científica condensada**, eliminando justificación que quedó redundante
   tras agregar el párrafo de síntesis.

Estos cambios se discutieron y decidieron en conversación antes de aplicarse; si quieres revertir
o ajustar alguno, dímelo y lo modifico directo en `body.tex`.


De todas las citas del cuerpo, **165 quedaron correctamente enlazadas** a una referencia con datos
completos (ya en `references.bib`). Pero **80 referencias únicas citadas en el texto no tenían
ficha bibliográfica** en ninguna de las dos listas del Word original (ni en el bloque numerado
[1]-[36] ni en el bloque APA de 52 ítems) — el propio documento decía "FALTAN INFINITAS", así que
esto era esperable.

Están marcadas en `references.bib` como `@misc{PEND_...}` con nota `TODO: completar`, y listadas
completas en **`REFERENCIAS_PENDIENTES.md`** (80 entradas, con la clave BibTeX exacta a usar).
No inventé ningún dato bibliográfico — hay que buscar cada una y completar autor/título/revista/DOI.

## Recortes aplicados (11 → 10 páginas) ✅
Ya apliqué los recortes en `body.tex`. Detalle de lo que se hizo:

1. **"Available Resources and Infrastructure"**: se quitó el listado de modelos exactos de
   CPU/GPU y se dejó solo la descripción funcional de cada recurso (equipos GPU propios,
   servidor del laboratorio, acceso a NLHPC, set óptico PIV/PTV).
2. **A3.1 PIV + A3.2 PTV**: se condensó el detalle operativo (parámetros de cámara, filtros,
   ventanas de interrogación, configuración de trackpy), manteniendo las decisiones
   metodológicas relevantes para un comité evaluador.
3. **A2.1 Computational model and meshing**: se resumió el párrafo de independencia de malla
   (conteos de celda de las 3 mallas) mantenimiento intacto el razonamiento científico sobre
   el parámetro $\Lambda$ y el esquema de acoplamiento semi-resuelto.
4. **1.1 Bedload transport**: ajuste de redacción en los dos párrafos finales, sin quitar
   ninguna cita ni afirmación.

No se tocó la Hipótesis, los Objetivos Específicos (SO1-SO5) ni el contenido científico central
de 1.3–1.6, que son los que más pesan frente al comité.

## Archivos
- `main.tex` — documento principal (portada + `\input{body.tex}` + bibliografía).
- `body.tex` — todo el contenido del Capítulo 1 a Publishing Proposal, ya con citas `\cite{}`.
- `references.bib` — 78 referencias resueltas + 80 pendientes (`PEND_...`).
- `figures/` — imágenes (logo, diagrama de metodología, Gantt convertido a PNG).
- `REFERENCIAS_PENDIENTES.md` — lista completa de las 80 referencias por completar.
