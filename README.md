# test

Kahoot open source, estático, para GitHub Pages. Sin backend: el docente actúa como anfitrión y los estudiantes se conectan directo (WebRTC con [PeerJS](https://peerjs.com), usando su servidor público solo para el apretón de manos inicial).

## Despliegue en GitHub Pages

1. Crea un repo llamado `test` y sube `index.html`.
2. Settings → Pages → Source: `main` / root.
3. Abre `https://<usuario>.github.io/test/`.

## Uso

**Docente**
1. "Soy docente" → carga el CSV y define una frase de paso.
2. Se genera un **código único de 6 caracteres** (y un enlace con `?c=CODIGO`). Compártelo.
3. Cuando estén todos, escribe la frase de paso y pulsa "Iniciar test".
4. Al final: podio, ranking y **Exportar resultados (CSV)**.

**Estudiante**: entra al enlace o escribe el código, pone su nombre y responde.

## Formato del CSV

```
pregunta,A,B,C,D,correcta,segundos
"¿Capital de Bolivia?",La Paz,Sucre,Cochabamba,Santa Cruz,B,20
```
`correcta` acepta A-D o 1-4. Se admiten 2 a 4 opciones. `segundos` es opcional (por defecto 20; rango 5-120). Separador `,` o `;`.

## Seguridad y límites (honestos)

- **Las respuestas correctas nunca salen del navegador del docente.** Los estudiantes reciben solo texto y opciones; el docente califica. No hay nada que descifrar en el cliente de ellos.
- El test se guarda cifrado (AES-GCM, clave derivada con PBKDF2 de 250 000 iteraciones) y solo se descifra en memoria al iniciar, con la frase de paso.
- **Un intento por estudiante**: nombres únicos por sala y un token por dispositivo; el token permite reconectar sin repetir el test. Quien borre el almacenamiento del navegador puede reconectar solo mientras la sala siga en el lobby; iniciada la partida se bloquea el ingreso de nuevos tokens. No impide que alguien use otro dispositivo en el lobby con otro nombre.
- Todo vive en la sesión: si el docente cierra o recarga la pestaña, la sala se pierde. Exporta el CSV antes de cerrar.
- Algunas redes (firewalls institucionales estrictos) pueden bloquear WebRTC sin servidor TURN.
- Los nombres exportados se neutralizan contra inyección de fórmulas en Excel.

Licencia sugerida: MIT.
