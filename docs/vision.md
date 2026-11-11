# Visión del proyecto — App del Clan de la Culebra

> Documento vivo. Recoge el *qué* y el *por qué* de la app. El *cómo* técnico está en [`constitution.md`](constitution.md) y en las specs de cada sección.

## 1. Contexto

**Lakuerter** es la feria ibera anual de Andorra (Teruel). Se celebra **el segundo fin de semana de noviembre**, de viernes a domingo. Unos 12 clanes participan, cada uno con su carpa decorada al estilo ibero, dispuestas alrededor de una gran hoguera central en un recinto habilitado por el ayuntamiento. Uno de los "clanes" es una legión romana, que hace de antagonista.

El **Clan de la Culebra** tiene unos **140 miembros**, organizados en **peñas** (cuadrillas de amigos del pueblo). La peña es la unidad organizativa básica:

- La **junta** tiene representantes de cada peña.
- Las tareas del fin de semana de la feria se **reparten por peñas**, no por personas, de modo que se cumplen sin depender de individuos concretos.

Del clan se eligen cuatro **personajes**: guerrero, sacerdotisa, sabio y portaestandarte.

### Actos de la feria

- Presentación y cierre de la feria.
- Bautizos y bodas iberas.
- Meriendas y aperitivos ofrecidos por clanes.
- Actuación (peleas de gladiadores u otra historia ibera).
- Juegos iberos: competición entre clanes en la plaza de toros.
- Desfile de todos los clanes por las calles del pueblo.
- Actos propios de cada clan y actos comunes.

## 2. Problemas a resolver

### 2.1 Montaje y desmontaje (el dolor principal)

Se hace aproximadamente la semana anterior y la posterior a la feria. Incluye:

- Montar **tres carpas** y decorarlas (telas, cañizos, hiedras y otros elementos).
- Hacer el montaje eléctrico.
- Traer y devolver material de la **cochera**, incluidos elementos muy pesados.

Dificultades:

- Cuesta conseguir suficientes voluntarios.
- Hace falta mucho conocimiento implícito: dónde está cada cosa y cómo se monta.

### 2.2 Inventario de la cochera

Todo el material, desde las carpas hasta los cubiertos de plástico, se guarda durante el año en una cochera.

- Material que debería desecharse se conserva por no saber qué hacer con él.
- Se compran cosas que ya se tenían por no saber que existían.

### 2.3 Tareas durante la feria

Turnos repartidos por peñas: abrir el clan a primera hora (debe haber alguien cuando ya hay actividad en el poblado), poner las mesas en comidas y cenas, recogerlas, servir comidas, organizar actividades (tatuajes iberos, competición de chapas iberas…).

### 2.4 Gestión durante el año

Reuniones de la junta, reparaciones de material dañado, compra de material nuevo, participación en el consejo de clanes y encargo de comida para el fin de semana.

### 2.5 Comunicación y asistencia

Avisos de la junta a los socios, y confirmaciones de asistencia e inscripciones a comidas y cenas.

## 3. Usuarios y niveles de acceso

| Nivel | Quién | Cómo accede | Qué puede hacer |
|---|---|---|---|
| **Anónimo** | Cualquiera con la app | Sin registro | Leer contenido no sensible (noticias, agenda) |
| **Socio** | Miembros del clan | Código de invitación (por email o WhatsApp) | Lo anterior + inscribirse, confirmar asistencia, marcar tareas de su peña |
| **Junta** | Miembros de la junta | Login completo | Lo anterior + publicar noticias, crear encuestas, gestionar inventario y tareas |

Principios:

- **El login no es obligatorio**: la mayoría de secciones son accesibles sin usuario.
- **Funciona sin conexión**: el contenido se puede consultar offline.

## 4. Visión de la app

Al abrir la app aparece un **portal de novedades** con los posts de la junta. Un **menú lateral ocultable** da acceso a secciones independientes:

| Sección | Descripción |
|---|---|
| Novedades | Noticias publicadas por la junta |
| Agenda / tareas de la feria | Turnos por peña y actos del fin de semana |
| Montaje | Instrucciones y tareas de montaje y desmontaje |
| Inventario | Qué hay, cuánto, dónde está y en qué estado |
| Encuestas e inscripciones | Asistencia, comidas, cenas |

*(Pablo tiene más ideas de secciones; se añadirán aquí a medida que se concreten.)*

## 5. Modelo de dominio (borrador)

- **Socio** — pertenece a una *Peña*; tiene un *rol* (junta / general); puede tener un *Personaje*.
- **Peña** — grupo de socios; unidad de asignación de tareas.
- **Personaje** — guerrero, sacerdotisa, sabio, portaestandarte.
- **Objeto** — material del clan: cantidad, *estado* (bien / dañado / desechar), instrucciones de montaje y desmontaje.
- **Ubicación** — zona o estantería de la cochera, o "en el recinto".
- **Tarea** — franja horaria, asignada a una *Peña* (feria) o a voluntarios (montaje, reparaciones); tiene un estado.
- **Evento** — acto de la feria, propio del clan o común.
- **Noticia** — publicada por la junta.
- **Encuesta / Inscripción** — asistencia, comidas, cenas.

## 6. Calendario

- **Feria 2026:** ya celebrada (6–8 de noviembre de 2026).
- **Próxima feria:** segundo fin de semana de noviembre de 2027 (fecha exacta por confirmar).
- **Objetivo:** beta usable por la junta con margen suficiente para preparar el montaje de 2027, sobre todo el inventario.

## 7. Orden de desarrollo propuesto

1. **Esqueleto** — proyecto, menú lateral, base de datos local, sincronización básica, portal de novedades en solo lectura.
2. **Inventario y ubicaciones** — el mayor valor; debe estar listo antes del próximo montaje.
3. **Tareas por peña y montaje.**
4. **Encuestas e inscripciones.**
5. Resto de secciones.

## 8. Fuera de alcance (por ahora)

- Versión iOS publicada (no hay Mac disponible; el código la dejará preparada).
- *Propuesto, por confirmar:* gestión económica (cuotas, pagos) y uso por otros clanes.

## 9. Preguntas abiertas

- ¿Qué otras secciones tiene en mente Pablo?
- ¿Qué datos de los socios son imprescindibles (nombre, peña, contacto…)?
- ¿Quién mantiene el inventario: solo la junta o también voluntarios?
- ¿Cómo se organiza hoy físicamente la cochera (zonas, estanterías)?
- ¿Qué actos y horarios de la feria son públicos y cuáles internos?
