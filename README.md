# Test - Kahoot Estilo OpenSource

**Test** es una aplicación web de tipo "quiz" estilo Kahoot, diseñada para funcionar en GitHub Pages. Los estudiantes pueden participar directamente sin necesidad de un docente cargar el examen.

## 📌 Características principales

- **Acceso directo:** El test se carga automáticamente desde `test.csv` al abrir la página. No requiere configuración del docente.
- **Pregunta 0 - Nombre:** Al iniciar, los estudiantes ingresan su nombre que se mantendrá durante todo el test.
- **Temporizador de 30s:** Entre cada pregunta hay un conteo regresivo de 30 segundos que avanza automáticamente.
- **Podio y Ranking:** Después de cada pregunta se muestra el podium con los 3 mejores puntajes. Al final del test, ranking completo.
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
```

## 🚀 Despliegue en GitHub Pages

1. **Crea un repositorio** en GitHub (puedes llamar `test`).
2. **Sube estos archivos**: `index.html`, `README.md` y el archivo `test.csv` (obligatorio).
3. **Configura GitHub Pages:**
   - Ve a *Settings* → *Pages*.
   - Fuente: rama `main`, carpeta `/root` (o `/(root)`).
   - Guarda. Tu sitio estará en `https://<usuario>.github.io/test/`.
4. Al entrar a la URL, el test se cargará automáticamente.

## 🎮 Cómo usan los estudiantes

1. Abren la URL de GitHub Pages.
2. **Ingresan su nombre** en el campo que aparece al inicio (Pregunta 0).
3. El **timer de 30s** comienza automáticamente.
4. Responden cada pregunta de opción múltiple (botones A, B, C, D).
5. Después de responder, el timer vuelve a 30s para la siguiente pregunta.
6. Ven el **podio** con los 3 mejores después de cada pregunta.
7. Al finalizar, clic en **"Exportar resultados CSV"** para descargar.

## 🛠️ Tecnologías

- HTML5, CSS3, JavaScript puro (sin dependencias externas).
- `localStorage` para persistencia en el cliente (los datos se reinician al recargar).
- Canvas para animación de fondo estrellado.
- Diseño responsive, funciona en móviles y desktop.

## ⚠️ Limitaciones

- Al recargar la página o abrir en otro dispositivo, los datos se reinician (diseño cliente-side).
- El CSV usa parsing simple por coma; si las preguntas tienen comas, escríbelas entre comillas o evítalas.
- La primera versión no incluye persistencia entre sesiones diferentes.

---

**Estructura del repositorio:**

```
/test/
├── index.html      # Aplicación completa (HTML + CSS + JS)
├── README.md       # Instrucciones y descripción
└── test.csv        # CSV de preguntas (cargado automáticamente)
```

¡Listo! Los estudiantes pueden participar inmediatamente sin necesidad de configuración previa.