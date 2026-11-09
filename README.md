# Test - Kahoot Estilo OpenSource

**Test** es una aplicación web de tipo "quiz" estilo Kahoot, diseñada para funcionar en GitHub Pages. Permite a docentes cargar exámenes de opción múltiple, y los estudiantes participan mediante un código único.

## Características

- **Modo Docente:** Carga un archivo CSV con preguntas y respuestas correctas, protegido por una passphrase (contraseña). Solo quien conoce la contraseña puede cargar el examen.
- **Modo Estudiante:** Los estudiantes ingresan con el código único generado al cargar el examen. Responden preguntas de opción múltiple.
- **Podio y Ranking:** Después de cada pregunta se muestra el podio con los tres mejores puntajes. Al final del test, se muestra el ranking final.
- **Exportar CSV:** Al finalizar, el docente puede exportar los resultados a un archivo CSV con los aciertos de cada estudiante.
- **Una sola carga a la vez:** Cada vez que el docente carga un nuevo examen, se borran los datos anteriores, asegurando que solo un test esté activo por sesión.

## Formato del CSV

El archivo CSV debe tener el siguiente formato (una línea por pregunta):

```
pregunta,opción1,opción2,opción3,opción4,indice_correcto
```

- `indice_correcto`: **0-based** (0 para la primera opción, 1 para la segunda, etc.). También se acepta **1-based** (1-4), la aplicación lo normaliza automáticamente.
- Ejemplo:

```
¿Cuál es la capital de Francia?,París,Londres,Berlín,Madrid,0
¿Cuánto es 2+2?,3,4,5,6,1
```

## Despliegue en GitHub Pages

1. **Crear un repositorio** en GitHub llamado `test` (o el nombre que prefieras).
2. **Subir los archivos** del proyecto: `index.html`, `README.md` (opcional) y cualquier otro recurso.
3. **Configurar GitHub Pages:**
   - Ve a la configuración del repositorio (Settings).
   - En la sección "Code and automation", selecciona "Pages".
   - Como fuente, elige la rama `main` y el folder `/root` (o `/(root)`).
   - Guarda. Tu sitio estará disponible en `https://<tu-usuario>.github.io/test/` (o el nombre del repositorio).
4. **Opcional:** Para usar un dominio personalizado, configura los registros DNS y habilita el dominio en la sección de Pages.

## Uso

### Docente

1. Accede a la URL de tu GitHub Pages.
2. Ingresa una **contraseña** en el campo "Contraseña". Esta será la passphrase para proteger la carga.
3. Sube un archivo CSV con el formato descrito arriba.
4. Al cargarse, se generará un **código de sesión** (ej. `A3F9B2`). Comparte este código con tus estudiantes.
5. Durante el test, después de cada pregunta aparecerá el **podio** con los tres mejores puntajes.
6. Al finalizar, haz clic en **"Exportar resultados CSV"** para descargar un archivo con los resultados de todos los participantes.

### Estudiante

1. Abre la misma URL y espera a que el docente cargue el test.
2. Ingresa tu **nombre** (apodo).
3. Ingresa el **código de sesión** que te dio el docente (o si ya está en la URL, solo presiona "Unirse").
4. Responde cada pregunta de opción múltiple seleccionando la opción correcta.
5. Al final, observa tu posición en el **podio final**.

## Tecnologías utilizadas

- HTML5, CSS3, JavaScript puros (sin dependencias externas).
- localStorage para persistencia de datos en el cliente.
- Canvas para animación de fondo estrellado.
- Sin servidor backend: todo funciona en el navegador del cliente.

## Limitaciones

- Al ser una aplicación cliente-side (solo HTML/JS), los datos se guardan en el navegador del usuario. Si los estudiantes limpian sus datos de navegador o usan otro dispositivo, perderán su progreso.
- La seguridad de la passphrase se basa en que no se revela la contraseña a los estudiantes. Para un uso más seguro en producción, se recomienda integrar un backend real (Firebase, Node.js, etc.).
- El CSV es de parsing sencillo; preguntas con comas en el texto deben evitarse o estar entre comillas (el parser actual divide solo por comas).