# Constitución del proyecto

> Principios no negociables que toda spec, plan e implementación debe respetar. Si una spec necesita romper uno, primero se modifica este documento, de forma explícita y razonada.
>
> Cuando se inicialice la herramienta de SDD (Spec Kit, Forge…), este contenido se copia o enlaza en su fichero de constitución o contexto (p. ej. `.specify/memory/constitution.md` o `CLAUDE.md`).

## I. Plataforma y lenguaje

1. **Kotlin Multiplatform (KMP)** para toda la lógica: modelos, repositorios, sincronización y casos de uso viven en `shared/commonMain`.
2. **Compose Multiplatform** para la UI, compartida entre plataformas.
3. **Android primero.** El target iOS se declara desde el inicio y debe compilar en cuanto haya un Mac, pero no se prueba ni se publica por ahora.
4. El código específico de plataforma (`expect`/`actual`) se limita a lo imprescindible: almacenamiento, cámara/QR, notificaciones.

## II. Offline-first

1. **La UI lee siempre de la base de datos local**, nunca directamente de la red. La red solo alimenta la base local.
2. **Toda la lectura funciona sin conexión**: noticias, agenda, inventario, instrucciones de montaje.
3. **Escritura offline solo donde la spec lo pida explícitamente** (p. ej. marcar una tarea como hecha, mover un objeto de ubicación). Se usa una cola de operaciones pendientes que se envía al recuperar la conexión.
4. **Resolución de conflictos: gana la última escritura** (*last-write-wins*), salvo que una spec justifique otra estrategia.
5. La UI muestra claramente el estado de sincronización (sin conexión / pendiente de enviar / sincronizado).

## III. Arquitectura

1. Capas: **UI (Compose) → ViewModel → Repositorio → {base local, API remota}**.
2. Flujo de datos unidireccional: la UI observa estado inmutable (`StateFlow`) y emite eventos.
3. **Cada sección del menú es un módulo de funcionalidad independiente.** Una sección no depende de las internas de otra; solo del dominio compartido.
4. El modelo de dominio de [`vision.md`](vision.md) §5 es la referencia. Los cambios en él se reflejan primero allí.

## IV. Backend y datos

1. **Backend gestionado: Supabase** (Postgres, autenticación y almacenamiento), con **servidor en la UE**.
2. **Los permisos se aplican en el servidor** mediante Row Level Security. La app nunca es la única barrera: ocultar un botón no cuenta como seguridad.
3. Las migraciones de esquema están versionadas en el repositorio.

## V. Acceso y privacidad

1. Tres niveles: **anónimo**, **socio** (código de invitación por email o WhatsApp) y **junta** (login completo). Ver [`vision.md`](vision.md) §3.
2. **El login nunca es obligatorio** para las secciones de lectura pública.
3. **RGPD:**
   - Datos mínimos: no se guarda un dato personal si ninguna spec lo necesita.
   - Los datos personales de socios (nombres, contactos) **no son visibles para usuarios anónimos**.
   - Hay un aviso de privacidad accesible desde la app.
   - Un socio puede pedir el borrado de sus datos.
4. Nunca se suben al repositorio secretos (claves de API, contraseñas). Van en configuración local excluida de git.

## VI. Proceso de desarrollo (SDD)

1. **Nada se implementa sin spec.** Ciclo: spec → plan → tareas → implementación → verificación.
2. Una spec describe el *qué* y el *por qué*, con criterios de aceptación comprobables. El *cómo* va en el plan.
3. Si durante la implementación se descubre un hueco en la spec, **se corrige la spec**, no solo el código.
4. Excepción: arreglos triviales (erratas, ajustes de pocas líneas) no necesitan spec.
5. **El autor aprende mientras construye:** los planes explican las decisiones no obvias de Android/KMP/Compose en vez de solo aplicarlas.

## VII. Calidad

1. La lógica de dominio y los repositorios tienen **tests unitarios** en `commonTest`.
2. Cada criterio de aceptación de una spec se verifica con un test o con una comprobación manual documentada.
3. El proyecto compila y los tests pasan antes de cada commit a `main`.
4. Commits pequeños, con mensajes descriptivos, preferiblemente uno por tarea.

## VIII. Idioma

1. **Interfaz, documentación y specs en español.**
2. Código (identificadores, comentarios técnicos) en inglés, salvo términos del dominio sin traducción natural (`Pena`, `Clan`…), que se decidirán en la spec del esqueleto.
3. Los textos de la UI van en recursos de cadenas, no incrustados en el código, para facilitar una futura traducción.
