# DBS · Catálogo de Químicos & VIERNES

Aplicación web con el catálogo de químicos de Diversified Building Services y el asistente técnico VIERNES.

## Estructura

- `index.html` — página principal (catálogo + chat VIERNES)
- `images/` — fotos de productos (agregar aquí)

## Configuración

1. Obtén una API key en <https://console.groq.com/keys>
2. En `index.html`, reemplaza `PEGA_AQUI_TU_GROQ_API_KEY` por tu key
3. Abre `index.html` en el navegador

## Flujo del asistente

1. Respuesta local (base de conocimiento) si hay confianza alta
2. Groq (IA) si la pregunta no está cubierta localmente
3. Mensaje amigable si la IA no está disponible

## Historial

- `41aec79` Versión inicial optimizada
