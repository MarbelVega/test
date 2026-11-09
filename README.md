# Test - Kahoot Estilo OpenSource

**Test** es una aplicación web de tipo "quiz" estilo Kahoot, diseñada para funcionar en GitHub Pages. Los estudiantes pueden participar directamente sin necesidad de un docente cargar el examen.

## 📌 Características principales

- **Acceso directo:** El test se carga automáticamente desde `test.csv` al abrir la página. No requiere configuración del docente.
- **Pregunta 0 - Nombre:** Al iniciar, los estudiantes ingresan su nombre que se mantendrá durante todo el test.
- **Temporizador de 10s:** Conteo regresivo de 10 segundos que se reinicia con cada nueva pregunta. Si el tiempo se acaba, la pregunta se guarda como incorrecta (0 puntos) y pasa automáticamente a la siguiente.
- **Podio y Ranking con validación:** Después de cada pregunta se muestra el podium con los 3 mejores puntajes. Al final del test, ranking completo. **Validación:** Los aciertos de cada estudiante están limitados a la cantidad total de preguntas (no puede haber más aciertos que preguntas existentes).
- **Exportar CSV:** Al finalizar, se puede descargar un archivo con los resultados de todos los participantes.
- **Una sola sesión activa:** Los datos se reinician al recargar la página, asegurando un test limpio cada vez.

## 📄 Formato del CSV

El archivo `test.csv` debe tener este formato (una pregunta por línea):

```
pregunta,opción1,opción2,opción3,opción4,indice_correcto
```

- `indice_correcto`: **0-based** (0 para la primera opción, 1 para la segunda, etc.). También se acepta **1-based** (1-4), la app lo normaliza automáticamente.
- Ejemplo (archivo `test.csv` incluido):

```
¿Cuál es la capital de Francia?,París,Londres,Berlín,Madrid,0
¿Cuánto es 2+2?,3,4,5,6,1
¿Qué planeta es conocido como el "Planeta Rojo"?,Marte,Vénus,Júpiter,Saturno,0
¿Quién escribió "Don Quijote de la Mancha"?,Miguel de Cervantes,William Shakespeare,Literato Gómez,Nikolái Gogol,0
¿Cuál es el elemento químico con símbolo "O"?,Oxígeno,Osmio,Oro,Plata,0
En qué año llegó el hombre a la luna?,1969,1970,1965,1972,0
¿Cuál es el animal más rápido?,Peregrino,Falco,Guepardo,Léon,0
¿Quién pintó la Mona Lisa?,Leonardo da Vinci,Pablo Picasso,Vincent van Gogh,Rembrandt,0
¿Cuál es el océano más grande?,Pacífico,Atlántico,Índico,Artico,0
¿Cuántos huesos tiene el adulto?,206,212,198,220,0
¿Qué país tiene más población?,China,India,Estados Unidos,Indonesia,0
```

## 🚀 Despliegue en GitHub Pages

1. **Crea un repositorio** en GitHub (puedes llamar `test`).
2. **Sube estos archivos**: `index.html`, `README.md` y el archivo `test.csv` (obligatorio - el test no cargará sin él).
3. **Configura GitHub Pages:**
   - Ve a *Settings* → *Pages*.
   - Fuente: rama `main`, carpeta `/root` (o `/(root)`).
   - Guarda. Tu sitio estará en `https://<usuario>.github.io/test/`.
4. Al entrar a la URL, el test se cargará automáticamente.

## 🎮 Cómo usan los estudiantes

1. Abren la URL de GitHub Pages.
2. **Ingresan su nombre** en el campo que aparece al inicio (Pregunta 0).
3. El **timer de 10s** comenzará automáticamente.
4. Responden cada pregunta de opción múltiple (botones A, B, C, D).
5. **Si el tiempo se acaba** (llegue a 0), la pregunta se guarda como incorrecta y pasa a la siguiente automáticamente.
6. Después de responder, el timer vuelve a 10s para la siguiente pregunta.
7. Ven el **podio** con los 3 mejores después de cada pregunta.
8. Al finalizar, clic en **"Exportar resultados CSV"** para descargar.

## 🛠️ Tecnologías

- HTML5, CSS3, JavaScript puro (sin dependencias externas).
- `localStorage` para persistencia en el cliente (los datos se reinician al recargar).
- Canvas para animación de fondo estrellado sutil.
- Diseño responsive, funciona en móviles y desktop.

## ⚠️ Limitaciones

- Al recargar la página o abrir en otro dispositivo, los datos se reinician (diseño cliente-side).
- El CSV usa parsing simple por coma; si las preguntas tienen comas, escríbelas entre comillas o evítalas.
- Si el timer llega a 0, la respuesta se guarda como incorrecta automáticamente.

---

## 🎨 Esquema de colores

La aplicación utiliza una **celeste y azul** tipo "azure" para crear un ambiente fresco y atractivo:

- **Fondo principal:** `#f0f8ff` (Alice Blue - muy claro)
- **Gradiente cielo:** `#87ceeb` a `#ffffff` (Sky Blue a Blanco)
- **Color de texto:** `#2c3e50` (Dark Blue Navy)
- **Timer (urgente):** `#e74c3c` (Red Coral - alto contraste cuando va bajando)
- **Botones accent:** `#e74c3c` (Coral naranja para acción)
- **Correcto:** `#27ae60` (Esmeralda verde)
- **Incorrecto:** `#e74c3c` (Coral rojo)
- **Cards/Contenedores:** `#ffffff` (Blanco puro)
- **Fondo estrellado:** `#e0f7fa` (Cyan muy claro)
- **Fondo preguntas:** `#ebf5fb` (Azul muy claro)

La combinación crea una experiencia visual agradable, fácil de leer y con suficiente contraste para usar en cualquier dispositivo.

---

**Estructura del repositorio:**

```
/test/
├── index.html      # Aplicación completa (HTML + CSS + JS)
├── README.md       # Instrucciones y descripción
└── test.csv        # CSV de preguntas (cargado automáticamente - OBLIGATORIO)
```

## 🔧 Personalización rápida

Para cambiar la cantidad de preguntas o el tiempo:

1. **Modificar `test.csv`:** Agrega o quita preguntas en el formato `pregunta,op1,op2,op3,op4,indiceCorrecto`
2. **Cambiar el tiempo:** En `index.html`, busca `const TIME_LIMIT = 10;` y cambia el número (en segundos)
3. **Modificar colores:** En `index.html`, busca `:root { ... }` y cambia los valores `var(--bg)`, `var(--accent)`, etc.

¡Listo! Los estudiantes pueden participar inmediatamente. Cuando el timer llega a 0, la respuesta se guarda automáticamente como incorrecta y continúa con la siguiente pregunta.