---
aliases--:
---
---

## 🧱 Estructura básica de Markdown

### 1. **Títulos (Headings)**

Usa `#` para crear jerarquías de títulos:

`# Título principal (H1) ## Subtítulo (H2) ### Sección (H3) #### Subsección (H4) ##### Detalle (H5) ###### Nota (H6)`

💡 Consejo: Usa máximo 3 niveles para apuntes claros.

---

### 2. **Listas**

**Listas con viñetas:**

`- Elemento 1  - Sub-elemento    - Sub-sub-elemento`

**Listas numeradas:**

`1. Paso uno 2. Paso dos 3. Paso tres`

**Listas de tareas (checkboxes):**

`- [ ] Pendiente - [x] Completado`

---

### 3. **Resaltado de texto**

`**negrita** *itálica* ~~tachado~~ ==resaltado (con plugin de Highlight)==`

> 💡 _El resaltado (==texto==) requiere el plugin “Markdown Highlight” o “Obsidian syntax highlighter” activado._

---

### 4. **Citas y bloques**

`> Esto es una cita. >> Cita dentro de una cita.`

**Bloque de código:**

` ```python print("Hola mundo") ``` `

**Bloque de texto literal (sin formato):**

`` `texto corto o comando` ``

---

## 🧭 Organización y vinculación

### 5. **Enlaces y notas**

- **Enlace interno:**  
    `[[Nombre de la nota]]` → enlaza otra nota de Obsidian.  
    También puedes enlazar una sección:  
    `[[Nombre de la nota#Sección específica]]`
    
- **Enlace externo:**  
    `[Texto del enlace](https://ejemplo.com)`
    

---

### 6. **Etiquetas (tags)**

Sirven para clasificar y buscar notas:

`#filosofía #apuntes #tareas`

💡 Puedes combinar etiquetas con carpetas para crear una jerarquía mental.

---

## 🧩 Bloques avanzados

### 7. **Separadores**

`---`

(Crea una línea horizontal para separar secciones)

---

### 8. **Tablas**

`| Concepto | Descripción | Ejemplo | |-----------|--------------|----------| | Neurona | Unidad del cerebro | 🧠 | | Sinapsis | Conexión entre neuronas | ⚡ |`

---

### 9. **Llamadas visuales (Callouts)**

Usa el formato especial de Obsidian (requiere versión reciente):

`` > [!note] Nota > Esto es una nota informativa.  > [!tip] Consejo > Usa atajos para mayor velocidad.  > [!warning] Advertencia > No cierres el archivo sin guardar.  > [!example] Ejemplo > `python print("Hola")` ``

Tipos comunes: `note`, `tip`, `warning`, `example`, `info`, `quote`, `abstract`, `faq`.

---

## ⌨️ Productividad en Obsidian

### 10. **Atajos útiles (Windows / macOS)**

|Acción|Atajo|
|---|---|
|Crear nueva nota|`Ctrl + N` / `Cmd + N`|
|Buscar nota|`Ctrl + O` / `Cmd + O`|
|Abrir búsqueda global|`Ctrl + Shift + F`|
|Vista dividida|`Ctrl + Shift + S`|
|Enlace rápido|`[[`|
|Panel de comandos|`Ctrl + P`|
|Comentario inline|`%% texto oculto %%`|

---

### 11. **Bloques especiales (para plugins)**

Algunos plugins permiten usar:

` ```dataview TABLE file.mtime AS "Última modificación" FROM #apuntes SORT file.mtime DESC `

`💡 Esto crea una tabla automática de tus notas si tienes el plugin **Dataview**.  ---  ### 12. **Enlaces a archivos, imágenes y multimedia** ```markdown ![[imagen.png]]        → muestra la imagen [[archivo.pdf]]        → enlace a PDF ![[audio.mp3]]         → reproduce audio`

Puedes usar rutas relativas: `![[carpeta/imagen.png]]`

---

## 🧠 Consejos para apuntes efectivos

- Usa **una nota por tema** y enlázalas con `[[ ]]`.
    
- Añade una sección final tipo:
    
    `## Resumen - Punto clave 1 - Punto clave 2`
    
- Crea una nota índice o "Mapa mental" con enlaces a tus temas más importantes.
    
- Usa `#pendiente` o `#revisar` para marcar cosas que necesiten atención.
    
- Aprovecha el plugin **Templater** para crear plantillas de apuntes con fecha y formato automático.
