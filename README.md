# DBS · Catálogo de Químicos & VIERNES

Aplicación web con el catálogo de químicos de Diversified Building Services y el asistente técnico VIERNES.

## Proyecto

🔗 **En vivo:** https://dansabio02.github.io/dbs-catalogo-quimicos/

## Estructura

- `index.html` — página principal (catálogo + chat VIERNES)
- `config.js` — tu API key de Groq (local, no se sube a GitHub)
- `config.example.js` — plantilla para copiar
- `images/` — fotos de productos y logo

## Visión IA (fotos de manchas)

El botón 📷 del chat permite tomar o subir una foto de una mancha.
VIERNES la analiza con **Gemini 2.5 Flash** (con fallback a `gemini-flash-latest`) y recomienda el producto DBS ideal.

1. Obtén una API key gratis en <https://aistudio.google.com/apikey>
2. En `config.js` descomenta y pega:
   `window.GEMINI_API_KEY_OVERRIDE = "tu_key";`
3. Listo — la foto se analiza en el chat

> ⚠️ **Seguridad:** la versión pública usa `gemini-public.js` (key ofuscada en
> base64, recuperable con devtools). Crea una key **aparte** en Google AI Studio,
> restringida al dominio `dansabio02.github.io`, y con cuota baja. Tu key real
> de Gemini queda solo en `config.js` (local).

- **Local:** usa `config.js` (no se sube a GitHub)
- **Público:** usa `groq-public.js` (key ofuscada en base64)
- **Modelos activos:** `openai/gpt-oss-120b` y `openai/gpt-oss-20b` (verificados con tu key)

⚠️ **Seguridad:** la key pública está ofuscada pero es recuperable por cualquier visitante.
Recomendación: crear una API key aparte en Groq solo para el sitio público, con límites de
uso bajos, y pegarla en `groq-public.js` en lugar de la actual.

1. Obtén una API key en <https://console.groq.com/keys>
2. Copia `config.example.js` como `config.js` y pega tu key
3. Abre `index.html` en el navegador (o visita la URL en vivo)

## Seguridad (auditoría y protecciones aplicadas)

**Protecciones implementadas en `index.html`:**

- **Anti-XSS:** sanitizer con allowlist (`limpiarHTML`) en toda respuesta de IA (Groq/Gemini) y búsqueda web; elimina `<script>`, `on*` handlers, `javascript:` y URLs peligrosas. Escape del input del usuario (`escaparHTML`) antes de renderizar.
- **API keys nunca pasan por proxies:** si la petición lleva `Authorization`, solo se usa conexión directa — la clave no se envía a corsproxy.io/allorigins.
- **Gemini con key en header** (`x-goog-api-key`), no en la URL — evita fugas en historial, logs y extensiones.
- **CSP (Content-Security-Policy):** bloquea `<object>/<embed>`, scripts remotos inyectados, `base-uri` y `form-action` restrictivos.
- **Anti-clickjacking:** la página no puede embeberse en iframes ajenos.
- **Referrer policy** estricta + `rel="noopener noreferrer"` en enlaces externos.
- `config.js` (keys reales) fuera de git (`.gitignore`).

**Pendiente (requiere acción del dueño — no se puede hacer desde el código):**

- [ ] Groq: crear una key **dedicada** en <https://console.groq.com/keys> para el sitio público y reemplazarla en `groq-public.js`
- [ ] Gemini: crear una key en Google AI Studio **restringida al referer** `dansabio02.github.io` y reemplazarla en `gemini-public.js`
- [ ] Ideal (futuro): backend proxy (Cloudflare Workers gratis) para no exponer keys en el navegador

> ℹ️ Las keys públicas están ofuscadas en base64, pero **cualquier visitante puede decodificarlas**
> con devtools. La ofuscación es disuasión, no seguridad real — las claves dedicadas/restringidas
> son la mitigación práctica en un sitio 100% estático.

## Flujo del asistente

1. Respuesta local (base de conocimiento) si hay confianza alta
2. Groq (IA) si la pregunta no está cubierta localmente
3. Mensaje amigable si la IA no está disponible

## Historial

- `41aec79` Versión inicial optimizada
