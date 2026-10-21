# CLAUDE.md — Círculo de Mejoras (mejoras)

Las reglas generales de trabajo están en el repo privado `lives-instrucciones` (CLAUDE.md). Este archivo solo describe esta herramienta.

## Qué hace
Seguimiento del **Círculo de Mejoras**: reunión semanal donde unas 16 áreas proponen ideas de mejora y se les da seguimiento hasta cerrarlas. Cada registro es una **mejora**: código generado por la base, área, idea, avance, responsable, fecha comprometida de cierre, categoría A/B/C, tipo de ahorro (Costo o Tiempo) con su monto o tiempo, situación antes, resultado y evidencias del antes y del después.
- `index.html` — **panel de gestión** con pestañas Mejoras y Reporte (la pestaña Tablero, que muestra el dashboard dentro de la página, queda oculta por la limpieza).
  - Escala de avance: 0 no iniciado, 0.3 solicitud realizada, 0.5 pedido en gestión, 0.7 confirmado por proveedor, 1 entregado o cerrado.
  - Filtros: área, texto, año/mes/semana sobre la fecha de cierre (incluye "sin fecha"), estado (todas, pendientes, cerradas, "por revisar esta semana"), categoría y tipo de ahorro, con conteos. Se ven de 50 en 50.
  - KPIs sobre lo filtrado: mostradas, avance (suma de avances ÷ mostradas), cerradas, vencidas (fecha de cierre pasada y avance < 1), ahorro en dinero (soles al mes, solo mejoras de tipo Costo) y ahorro en tiempo (horas:minutos al mes, solo tipo Tiempo).
  - Controles rápidos en la tarjeta (categoría, tipo de ahorro, monto o tiempo) que guardan al instante. Ficha completa para crear o editar: idea obligatoria, avance, responsable, fecha, categoría, comentarios, antes y después con fotos y archivos (las evidencias se suben después de guardar). Quitar la marca "por revisar" de las migradas.
  - Eliminar una mejora no la borra de verdad: queda archivada en la base con sus archivos.
  - Reporte para correo o PDF: mejoras pendientes (con y sin fecha) y cerradas del año, con "Descargar PDF" (imprimir) y "Copiar para el correo".
- `dashboard.html` — **tablero** de solo lectura, con filtro por área. Meta de avance 100 %, semáforo (≥ 100 verde, ≥ 80 ámbar, < 80 rojo). Pestañas Panorama, Áreas, Riesgo (las más atrasadas, vencidas por área y reprogramaciones, que empiezan a contar desde ahora), Evidencia (% de ideas por área con al menos un archivo) y Detalle (regla 500). Imprime en A4.
- Evidencias: imágenes (se comprimen en el equipo), PDF, Word, Excel, CSV, PowerPoint, texto, zip, correos; hasta 20 MB cada una; se pueden pegar con Ctrl+V o tomar con la cámara.
- Excel: solo el bloque LIVES, no tiene exportación propia.
- Guarda una copia en el equipo (`lives_mejoras_v2` y `lives_evid_v2`) para abrir al instante; sin red muestra lo último guardado.

## Base de datos (Supabase lives-datos)
- Leer: `mejoras_listar` y `mejoras_evidencias_listar`.
- Registrar: `mejoras_crear`, `mejoras_actualizar`, `mejoras_borrar` (archiva), `mejoras_evidencia_agregar` y `mejoras_evidencia_borrar`.
- Tablas: `mejoras`, `mejoras_areas`, `mejoras_evidencias`, `mejoras_cambios` (historial). Al 21/10/2026: 592 mejoras y 219 evidencias.
- Archivos: bucket privado `mejoras` (`<id de la mejora>/<marca de tiempo>-<aleatorio>.<ext>`), con enlaces firmados de 24 horas.
- Ya no hay Apps Script ni hoja de Google. Las 630 ideas iniciales se migraron del Excel original el 28/09/2026.

## Quién la usa
No aparece en el registro de entradas del portal de los últimos 60 días (al 21/10/2026), aunque tiene registros guardados.

## Quién puede registrar
- Lo decide la base: `mejoras_puede_leer_` y `mejoras_puede_escribir_` (esta última también protege la subida de archivos). El nombre de quien registra lo toma la base de la sesión del portal.
- A Sistemas: esas dos funciones son las piezas que reemplazan con su seguridad.

## Pendientes vistos al escribir esto (21/10/2026)
- La pestaña Tablero del panel existe en el código, pero la limpieza la oculta.
- Un mensaje de error del panel nombra a una persona con texto fijo: debe pasar a "Datos e IA".
- Subir un archivo son dos pasos (almacén y luego registro): si falla el segundo puede quedar un archivo suelto en el almacén.
- Quedan nombres heredados (`jsonp()`, textos "archivo Excel original") que en realidad usan la base.
