# entrega-final-automatizacion-ia
Sistema de soporte con IA: Make + Airtable + Claude + Gmail
Ecosistema de Automatización IA: Soporte IA

Autor: Santiago Moreno · Curso: Automatización con IA (Make) · Entrega Final

Sistema de triage y respuesta de tickets de soporte: cada email que llega a la casilla de soporte se clasifica con IA (prioridad, categoría y sentimiento), se redacta un borrador usando el historial del cliente, un humano lo aprueba y el sistema responde en el mismo hilo de Gmail.

Stack
Categoría	Tecnología
Orquestador	Make (escenario A: ingesta y clasificación · escenario B: aprobación y envío)
Base de datos	Airtable, base "Soporte IA" (Clientes, Tickets, Interacciones, Errores)
IA	Anthropic Claude Haiku 4.5 (salida JSON estructurada, memoria por cliente)
Canal de salida	Gmail (aviso de aprobación y respuesta en el hilo con Thread ID)
Enlaces
Base de datos (solo lectura): https://airtable.com/invite/l?inviteId=inv8j0nbUZY64ls7x&inviteToken=64733119e84e8834e3bfa3829af8678917d2dbe493cb7728d694d1afd7143090
Dashboard de control (Shared View): [PEGAR LINK]
Video demo (3 min): https://www.youtube.com/watch?v=-HM7mrUbiWM
Contenido del repositorio
docs/Entrega_Final_Documentacion.pdf: mapa de arquitectura, manual de datos y esquemas JSON, matriz de costos, seguridad y resiliencia, dashboard y pruebas.
docs/diagrama-arquitectura.pdf: diagrama del sistema.
blueprints/: blueprints exportados de los escenarios A y B de Make.
capturas/: evidencias de las ejecuciones (camino feliz, duplicado, datos incompletos, fallas de API y de JSON, aprobación y envío, falla de envío, memoria, dashboard).
Puntos clave
HITL: el sistema nunca contacta al cliente sin que un humano marque "Aprobado".
Resiliencia: error handlers con Resume (escenario A) y Retry (escenario B), registro de cada falla en la tabla Errores.
Anti-bucle y anti-duplicados: filtro por remitente y etiqueta, y búsqueda por Gmail Thread ID.
Prompt seguro: el email del cliente va aislado en etiquetas <email> (defensa contra prompt injection) y la IA solo puede devolver valores cerrados que coinciden con Airtable.
Costo medido: USD 0,000956 por ticket con Claude Haiku 4.5.
