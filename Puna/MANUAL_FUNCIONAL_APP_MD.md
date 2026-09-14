# Manual Funcional — Pilates Flow Portal

> Guía de uso paso a paso para personal de estudios de pilates/fitness que operan la app, y fuente de referencia estructurada para agentes de IA que necesiten responder preguntas sobre su funcionamiento.

**Última actualización:** 13/09/2026
**Idioma de la app:** Español (Argentina)
**Audiencia:** Personal de recepción/administración (staff), profesores (teacher), clientes finales, y agentes IA de soporte.

---

## Cómo usar este manual

- Está organizado por **módulo** (Clientes, Clases, Suscripciones, Reservas, Pagos).
- Dentro de cada módulo, los procesos siguen el orden **ABMR**: **A**lta → **B**aja → **M**odificación → **R**enovación (cuando el proceso aplica a ese módulo).
- Cada paso a paso está escrito para poder ejecutarse siguiendo la pantalla, sin conocimientos técnicos.
- Los bloques `> Nota` aclaran reglas de negocio o límites del sistema.
- Si sos un agente de IA: tratá cada encabezado `##`/`###` como una unidad de contexto independiente; los nombres de botones y campos están escritos tal como aparecen en la pantalla.

---

## Índice

1. [Introducción general](#1-introducción-general)
2. [Roles y navegación](#2-roles-y-navegación)
3. [Glosario de conceptos clave](#3-glosario-de-conceptos-clave)
4. [Módulo: Clientes](#4-módulo-clientes)
5. [Módulo: Clases](#5-módulo-clases)
6. [Módulo: Suscripciones](#6-módulo-suscripciones)
7. [Módulo: Reservas / Agendas](#7-módulo-reservas--agendas)
8. [Módulo: Pagos](#8-módulo-pagos)
9. [Flujo de ejemplo end-to-end](#9-flujo-de-ejemplo-end-to-end)
10. [Notas para agentes IA](#10-notas-para-agentes-ia)

---

## 1. Introducción general

Pilates Flow Portal es un sistema de gestión para estudios de pilates/fitness. Administra el ciclo completo de un cliente: alta, venta de planes (suscripciones), reserva de clases, asistencia y cobranza.

**Modelo de negocio de la app:**
- Es un software vendido como "white-label" a cada estudio (1 instalación por cliente/marca).
- **No es una tienda online**: el cliente final no compra ni paga con tarjeta desde la app. El personal del estudio (staff) es quien registra manualmente cada venta y cada cobro.
- No hay pasarela de pago integrada. "MercadoPago" puede aparecer como una etiqueta de método de pago, pero el pago no se procesa automáticamente — sigue siendo un registro manual del staff.

**Tres roles de usuario:**

| Rol | Quién es | Qué hace en la app |
|---|---|---|
| **Staff** | Personal administrativo/recepción del estudio | Gestiona clientes, clases, suscripciones, reservas y pagos. Acceso completo (según permisos). |
| **Teacher** (Profesor) | Instructor de clases | Ve sus clases asignadas, pasa asistencia, ve avisos y tareas. Acceso acotado. |
| **Cliente** | Alumno del estudio | Ve y reserva sus propias clases, consulta sus suscripciones, gestiona su ficha de salud. Sin acceso administrativo. |

---

## 2. Roles y navegación

La app no usa URLs distintas por pantalla: la navegación es por **pestañas de estado**, persistidas en el navegador. El contenido que ves depende de tu rol y de tus permisos configurados.

### 2.1 Menú del rol Staff

El staff tiene dos niveles de navegación:

**Nivel 1 — Secciones principales** (selector arriba de la pantalla):

| Sección | Qué contiene |
|---|---|
| **Avisos** | Tablero de notificaciones internas para staff/profesores |
| **Gestión** | Panel principal — acá vive la operación diaria (clientes, clases, suscripciones, reservas, pagos) |
| **Renovaciones (V1)** | Versión anterior de renovaciones (en desuso) |
| **Analítica** | Reportes y métricas del estudio |
| **Informes** | Campañas e informes personalizados |
| **Gestión de Personal** | Alta/gestión de usuarios internos (staff/profesores) |

**Nivel 2 — Menú lateral (sidebar), agrupado por bloque:**

- **Operación**
  - Tareas — pendientes internos del equipo
- **Gestión**
  - Clientes — alta, edición, búsqueda de clientes
  - Cambios — pedidos de cambio de horario pendientes de resolver
  - Suscripciones — ventas, modificaciones y detalle de planes vendidos
  - Clases — administración de clases y horarios (sub-tabs: Calendario / Lista)
  - Feriados — configuración de días/horarios sin clase
  - Proyección — proyección de ocupación futura
  - Historial de agendas — búsqueda histórica de reservas
  - Plantillas de agenda — plantillas para agendamiento masivo
  - Lista de espera — gestión de pedidos en espera de cupo
- **Pagos**
  - Facturación y Cobranzas (sub-tabs: Facturación / Cobranzas / Historial)
- **Renovaciones**
  - General — cockpit de renovaciones (V2)
  - Historial de renovaciones — renovaciones ya procesadas
- **Análisis**
  - Analítica
  - Campañas e Informes
- **Sistema**
  - Gestión de Personal
  - Configuración (sub-tabs: General, Productos, Facturación y Pagos, Motivos, Tareas, Alianzas, Campañas e Informes, Logs)
  - Manual — abre este tipo de documentación (configurable por el estudio en Configuración → Info de la Empresa)

> Nota: algunos ítems del menú solo aparecen si el usuario tiene el permiso correspondiente habilitado (ej. `sidebar.gestion.clients`). Es normal que dos usuarios staff vean menús distintos.

### 2.2 Menú del rol Cliente

El cliente ve pestañas horizontales simples, sin sidebar:

| Pestaña | Qué muestra |
|---|---|
| **Mis clases** | Próximas clases reservadas |
| **Reservar** | Calendario/buscador para reservar nuevas clases |
| **Mi salud** | Ficha de salud propia (lesiones, obra social, apto físico) |
| **Cancelaciones** | Historial de reservas canceladas |
| **Mis Suscripciones** | Planes activos/vencidos y sus créditos |

### 2.3 Menú del rol Profesor (Teacher)

| Pestaña | Qué muestra |
|---|---|
| **Avisos** | Notificaciones para profesores |
| **Mis Clases** | Clases asignadas, con lista de alumnos y registro de asistencia |
| **Tareas** | Pendientes asignados al profesor |

---

## 3. Glosario de conceptos clave

Conceptos que se repiten en todos los módulos y conviene tener claros antes de operar:

| Concepto | Qué significa |
|---|---|
| **Producto / Plan de suscripción** | Plantilla de venta que crea el estudio una sola vez (ej. "8 Clases Mensuales"). Vive en Configuración → Productos. Es el catálogo. |
| **Suscripción** | La compra concreta que hace un cliente de un producto (ej. "María compró el plan de 8 clases, vence el 30/09"). Es la venta real. |
| **Crédito** | Unidad que representa "una clase". Si un cliente compra 8 clases, tiene 8 créditos. Cada reserva consume 1 crédito (o los que indique la clase); cada cancelación con devolución lo repone. |
| **Actividad** | La disciplina que se dicta (Pilates, Yoga, Zumba, etc.). Se configura en Configuración → Actividades. |
| **Sala** | El espacio físico donde se dicta una clase (Sala 1, Estudio Principal, etc.). Evita que dos clases se solapen en el mismo lugar. |
| **Intensidad** | Nivel de dificultad de una clase (Baja/Media/Alta), con color asociado en las vistas. |
| **Feriado** | Fecha (u horario puntual) en la que no se dictan clases. Puede ser de día completo o de un rango horario específico. |
| **Plantilla (Template)** | Patrón guardado de horarios recurrentes de un cliente (ej. "lunes 9:00, miércoles 17:00"), usado para agendar o renovar en un clic. |
| **Tres tarjetas (Clases · Monto · Horarios y cupo)** | Forma estándar en que se presenta cualquier venta, modificación o renovación de suscripción: cuántas clases tiene, cuánto cuesta, y qué horarios/cupo ocupa. Ver detalle en el [módulo Suscripciones](#6-módulo-suscripciones). |
| **Estado de la suscripción** | ACTIVA, VENCIDA (EXPIRED), CANCELADA, etc. — indica si el plan está vigente. |
| **Estado de facturación** | PAGADO, PENDIENTE, PARCIAL, MORA (OVERDUE), PROMESA DE PAGO — indica cuánto se cobró de esa suscripción, es independiente del estado de la suscripción. |
| **ABMR** | Alta, Baja, Modificación, Renovación — el orden estándar en que se documentan y ejecutan los procesos de negocio en esta app. |

---

## 4. Módulo: Clientes

Gestión de la ficha de cada alumno del estudio: datos personales, contacto, salud y acceso a su cuenta.

### 4.1 Alta — Crear un cliente nuevo

1. Ir a **Gestión → Clientes**.
2. Hacer clic en **"+ Nuevo Cliente"**.
3. Completar el formulario (dividido en secciones):

   **Identidad y acceso** (obligatorios):
   - Nombre, Apellido
   - Correo electrónico — es el usuario de login del cliente; debe ser único, no puede repetirse.
   - Tipo de documento (DNI, Pasaporte, CUIT/CUIL, Otro) y Número de documento
   - Contraseña inicial (mínimo 6 caracteres) — solo se pide en el alta.

   **Contacto** (teléfono obligatorio; Instagram y fecha de nacimiento opcionales).

   **Emergencias** (opcional): contacto de emergencia, obra social/prepaga, número de credencial.

   **Salud y controles** (opcional):
   - Apto físico (checkbox)
   - Lesiones declaradas (checkbox + descripción libre si se marca)
   - BlackList (checkbox — excluye al cliente de campañas de marketing)

   **Palabra clave**: si el estudio tiene esta función habilitada, se genera sola (ej. `dorado.aguila`). Sirve como identificador adicional de privacidad, no reemplaza el login.

4. Hacer clic en **"Crear cliente"**. Si un campo obligatorio falta o el email ya existe, la app muestra el error puntual antes de guardar.

> Nota: solo Nombre, Apellido, Email, Tipo/Número de documento, Teléfono y Contraseña son obligatorios. Todo lo demás es opcional.

### 4.2 Baja — Eliminar o bloquear un cliente

Existen **dos caminos**, según si el cliente tiene historial o no:

**A) Eliminación permanente** (solo si el cliente NO tiene ninguna suscripción, reserva o plantilla asociada):
1. En la grilla de Clientes, columna Acciones, hacer clic en el ícono de **papelera roja**.
2. La app verifica automáticamente si el cliente tiene historial:
   - Si tiene → muestra **"Borrado bloqueado"** con el detalle (ej. "2 suscripciones, 5 reservas") y no permite continuar.
   - Si no tiene → abre un diálogo de confirmación con advertencia de acción irreversible.
3. Confirmar **"Eliminar Cliente"**. Se borra el registro y su acceso de login de forma permanente.

**B) Bloqueo** (forma recomendada cuando el cliente ya tiene historial — equivale a la "baja" habitual):
1. En Acciones, hacer clic en el ícono de **llave** ("Credenciales y Acceso").
2. Activar el interruptor **"Cuenta bloqueada"**.
3. Seleccionar un **motivo de bloqueo** obligatorio (ej. "Deuda pendiente", "Solicitud propia", "No se presenta a las clases" — lista configurable por el estudio).
4. Guardar cambios.

**Efecto del bloqueo:** el cliente no puede iniciar sesión, pero conserva todo su historial. Sigue visible en la grilla con estado "Bloqueado" (rojo) y el motivo en la columna correspondiente. Se puede desbloquear en cualquier momento apagando el mismo interruptor.

> Nota: no hay una tercera opción de "borrado suave" automático — el sistema obliga a elegir entre eliminar (sin historial) o bloquear (con historial).

### 4.3 Modificación — Editar un cliente existente

1. En Acciones, hacer clic en el ícono de **lápiz amarillo**.
2. Se abre el mismo formulario del alta, precargado.
3. Se puede editar: nombre, apellido, email, documento, teléfono, Instagram, fecha de nacimiento, contacto de emergencia, obra social, apto físico, lesiones, blacklist y palabra clave.
4. La contraseña y el estado de bloqueo **no se editan acá**: se gestionan desde "Credenciales y Acceso" (ver 4.2-B).
5. Guardar con **"Actualizar"**.

> Nota — email desalineado: si el email de la ficha queda distinto al del login real (Auth), aparece un banner rojo de advertencia con el botón **"Alinear con la ficha"** para sincronizarlos.

### 4.4 Búsqueda y otras acciones

**Grilla de clientes** — columnas: Acciones, Nombre, Estado, Motivo, Correo, Blacklist, Documento, Teléfono, Apto, Dolencias, Creado. Filtros: búsqueda libre (nombre/email/documento/teléfono), Estado (Activo/Bloqueado), Lista negra (Sí/No). Paginado de a 10, ordenable por columna.

**Otras acciones sobre un cliente** (columna Acciones):
- **Gestión Integral** (ícono azul): abre la vista 360° del cliente (historial, suscripciones, reservas, actividad).
- **Enviar Notificación** (ícono campana): envía una notificación push puntual.
- **Historial de Actividad**: registro cronológico de reservas, cambios de suscripción y modificaciones del cliente, filtrable por tipo de evento y fecha.

---

## 5. Módulo: Clases

Gestión de la oferta de clases del estudio: horarios, salas, profesores y cupos. (No aplica "Renovación" como proceso propio de este módulo — la renovación de horarios de un cliente se gestiona desde Suscripciones/Reservas).

### 5.1 Alta — Crear una clase nueva

1. Ir a **Gestión → Clases**.
2. Hacer clic en **"+ Nueva"**.
3. Elegir el tipo:
   - **Clase Única**: una sola clase, en una fecha y hora puntual.
   - **Serie Recurrente**: se repite automáticamente en los días de la semana que elijas.
4. Completar los campos comunes:

   | Campo | Detalle |
   |---|---|
   | Nombre | Se lo ven los clientes |
   | Descripción | Opcional, uso interno |
   | Actividad | Disciplina (Pilates, Yoga, etc.) |
   | Sala | Espacio físico |
   | Intensidad | Baja/Media/Alta |
   | Profesor | Instructor asignado |
   | Capacidad máxima | Cupo de alumnos |
   | Créditos requeridos | Cuántos créditos consume por reserva |
   | Fecha y hora | Cuándo empieza |
   | Duración | En minutos |

5. Si es **Serie Recurrente**, además: marcar los días de la semana (checkboxes L-D) y, opcionalmente, una fecha de fin (si se deja vacía, la app genera automáticamente 6 meses de clases).
6. Hacer clic en **"Crear Clase"** / **"Crear Serie"**. Las clases quedan disponibles de inmediato para reservar.

### 5.2 Baja — Cancelar o eliminar una clase

Hay dos operaciones distintas, no intercambiables:

- **Eliminar**: borra la clase de la base de datos, como si nunca hubiera existido. Solo recomendable si no tiene reservas (se pierde ese dato si las tuviera).
- **Cancelar**: marca la clase como "CANCELADA" sin borrarla, notifica a los clientes con reserva, y permite decidir si se les devuelven los créditos. Es la opción recomendada cuando ya hay gente anotada.

**Cancelar una clase puntual:**
1. Ubicarla en el calendario o la lista.
2. Hacer clic en el ícono de cancelar (🚫).
3. Completar: motivo (ej. "Profesor ausente", "Sala no disponible"), notas opcionales, y el checkbox **"¿Devolver créditos?"**.
4. Confirmar. La clase pasa a rojo/CANCELADA y se notifica a los clientes con reserva.

**Eliminar/cancelar una serie recurrente completa:**
- Para eliminar todas las clases futuras de una serie, usar la opción "Eliminar serie" desde cualquier clase de esa serie.
- Si la serie ya tiene reservas, conviene primero cancelar puntualmente esas clases (para devolver créditos y notificar) y recién después eliminar la serie, o usar **acciones en lote → "Cancelar en lote"** sobre el conjunto de clases de la serie.

> Nota: si reducís la capacidad de una clase por debajo del número de reservas ya confirmadas, el sistema bloquea el guardado.

### 5.3 Modificación — Editar una o varias clases

**Una clase puntual:**
1. Abrir la clase → ícono **✏️ editar**.
2. Modificar cualquier campo (nombre, profesor, sala, horario, duración, capacidad, créditos).
3. Guardar con **"Actualizar Clase"**.

**Varias clases a la vez (acciones en lote):**
1. Seleccionar varias clases con los checkboxes de la grilla/lista.
2. Elegir la acción en lote: cambiar profesor, cambiar capacidad, cambiar créditos requeridos, o correr el horario (±15/30/60 minutos).
3. Confirmar. Si alguna clase seleccionada quedaría con menos cupo que reservas existentes, la app avisa con un banner antes de aplicar.

### 5.4 Vistas disponibles

| Vista | Cuándo usarla |
|---|---|
| **Calendario** (semanal) | Ver de un vistazo la ocupación de la semana. Semáforo de colores: verde = disponible, amarillo = casi lleno (≥80%), naranja = lleno, rojo = cancelada. |
| **Lista** | Ver datos tabulares detallados, ordenar/filtrar/paginar, y aplicar acciones en lote. |
| **Timeline** | Línea de tiempo por día, útil con muchas clases o en pantallas angostas. |

Todas las vistas comparten filtros: rango de fechas, actividad, profesor, estado y búsqueda por nombre.

### 5.5 Feriados

Un feriado bloquea clases automáticamente en una fecha (día completo o un rango horario puntual).

1. Ir a **Gestión → Feriados → "+ Nuevo feriado"**.
2. Completar: fecha, nombre, hora desde/hasta (dejar 00:00–23:59 para día completo), notas opcionales.
3. Guardar.

Efecto: las clases recurrentes no se generan en fechas de feriado completo; si hay clases manuales que caen en ese rango, la app avisa; los clientes no pueden reservar en un horario bloqueado.

---

## 6. Módulo: Suscripciones

Es el módulo comercial central: catálogo de planes, ventas a clientes, modificaciones sobre planes activos y renovaciones. Sigue el ciclo **ABMR completo**.

### 6.0 Dos conceptos que no hay que confundir

- **Producto/Plan** (catálogo, se configura una sola vez en Configuración → Productos): nombre, precio estándar, cantidad de créditos, ciclo de renovación, actividad asociada, métodos de pago aceptados, si requiere plantilla de horarios fijos.
- **Suscripción** (la venta concreta a un cliente, se gestiona en Gestión → Suscripciones): cliente, producto elegido, precio realmente pagado, créditos otorgados, descuentos aplicados, vigencia (inicio/fin), horarios asignados, estado de pago y estado de la suscripción.

### 6.1 Las "tres tarjetas" (marco visual común a Alta, Modificación y Renovación)

Toda pantalla de venta, modificación o renovación presenta la información en 3 bloques fijos, siempre en el mismo orden:

1. **Clases** — cuántas clases/créditos tiene la suscripción (plan base + extras).
2. **Monto** — el precio final, solo de lectura (desglose de precio estándar, descuentos e IVA). Para cambiar el precio hay que editar el producto/descuento, no el monto directamente.
3. **Horarios y cupo** — los días/horarios asignados (chips) y el veredicto de disponibilidad de cupo.

### 6.2 Alta — Vender una suscripción nueva

1. Abrir el **cotizador** (Ventas / "+ Venta Rápida", o desde la ficha del cliente → Nuevo).
2. **Paso 1 — Cliente y producto**: elegir el cliente y el plan a vender. La app calcula automáticamente precio estándar, vigencia (ej. 30 días) y créditos totales.
3. **Paso 2 — Ajustes** (opcional): modificar cantidad de clases, aplicar descuentos (fijo, porcentaje o alianza comercial) y, si el producto usa horarios fijos, asignar la plantilla de horarios.
4. **Paso 3 — Pago**: elegir método de pago y cuenta, y marcar si se cobra en el momento o queda pendiente.
5. **Paso 4 — Confirmación**: se muestra el resumen con el ID de suscripción creada. Si el plan tiene horarios fijos, se ofrece agendar automáticamente todas las clases del período (agendamiento masivo).

> Resultado: se crea el registro de suscripción, se generan las reservas si correspondía, y el cliente ya puede empezar a usar sus créditos.

### 6.3 Baja — Cancelar una suscripción

1. Abrir la suscripción del cliente (Gestión → Suscripciones → seleccionar).
2. Hacer clic en **"Cancelar Suscripción"**.
3. La app verifica si hay pagos registrados sobre esa suscripción:
   - Si hay pagos activos → bloquea la cancelación hasta que se reviertan primero (ver [módulo Pagos](#8-módulo-pagos)).
   - Si no hay pagos pendientes de revertir → permite continuar.
4. Completar **motivo de cancelación** (obligatorio, ej. "Cliente se va", "Mudanza") y notas opcionales.
5. Confirmar (suele requerir escribir una palabra de confirmación para evitar bajas accidentales).

**Efecto:** la suscripción pasa a CANCELADA, se cancelan automáticamente todas sus reservas futuras y se cierran los créditos restantes.

### 6.4 Modificación — Cambiar una suscripción activa

1. Abrir la suscripción → **"Modificar"**.
2. Elegir la **intención** del cliente (no una operación técnica), por ejemplo:

   | Intención | Efecto |
   |---|---|
   | Upgrade de plan | Sube la cantidad de clases y recalcula el precio |
   | Downgrade de plan | Baja la cantidad de clases y recalcula el precio |
   | Regalo de clases | Suma clases sin cambiar el precio |
   | Quitar clases | Resta clases sin devolver dinero |
   | Cambiar horarios | Modifica los días/horas fijos asignados |
   | Se va de viaje | Pausa temporal entre dos fechas |
   | Agendar libre | Saca la plantilla fija y deja que agende clase por clase |
   | Corregir precio | Ajusta descuentos sin tocar la cantidad de clases |
   | No renueva / Sí renueva | Activa o desactiva la renovación automática |
   | Transferir a otro cliente | Cambia el titular de la suscripción |

3. Completar los campos que pida esa intención (cantidad de clases, fechas de ausencia, motivo, etc.).
4. La app muestra una comparación **Antes → Después** sobre las tres tarjetas (Clases, Monto, Horarios y cupo), con alertas si corresponde (ej. "cobertura insuficiente", "hay reservas futuras que se van a perder").
5. Confirmar con **"Guardar Modificación"**. Si el cambio afecta horarios, se ofrece re-agendar automáticamente las clases restantes.

**Ajuste manual de créditos:** desde el detalle de la suscripción, botón "Ajuste de Créditos" → sumar/restar créditos con motivo obligatorio, o pedir un recálculo automático que compara los créditos guardados contra las reservas activas y corrige discrepancias.

### 6.5 Renovación — Renovar una suscripción al vencer

1. Ir a **Renovaciones → General** (cockpit de renovaciones).
2. Filtrar por mes de vencimiento, estado o actividad para ubicar al cliente.
3. Abrir la suscripción a renovar (se abre un panel lateral).
4. **Pestaña Propuesta**: la app propone renovar con el mismo producto y condiciones; se puede cambiar plan, vigencia, descuentos o sumar clases adicionales. Se muestra la comparación Antes → Después.
5. La app avisa de riesgos comunes: sin plantilla de horarios, sin cupo en los horarios deseados, cliente en lista de espera, o descuentos por vencer.
6. **Pestaña Confirmar**: revisar el resumen y ejecutar con **"Ejecutar Renovación"**.

**Efecto:** se crea una nueva suscripción vinculada como renovación de la anterior (que queda marcada como "renovada"), y se ofrece agendar automáticamente las clases del nuevo período.

**Renovación anticipada:** un cliente puede renovar antes de la fecha de vencimiento; el proceso es el mismo, y la app puede encadenar varios ciclos de renovación de una vez.

**Renovación automática:** cada suscripción tiene un indicador "¿Debe renovarse automáticamente?". Si está activado, al vencer se renueva sola con las mismas condiciones; si se desactiva, se pide un motivo (ej. "cliente de vacaciones").

### 6.6 Estados de una suscripción

| Estado | Significa | ¿Puede reservar clases? |
|---|---|---|
| ACTIVA | Vigente y en uso | Sí |
| PENDIENTE | Creada, aún sin confirmar pago | Depende de la configuración del estudio |
| POR VENCER | A pocos días de su fin | Sí, con aviso de renovación |
| VENCIDA (EXPIRED) | Pasó la fecha de fin sin renovar | No |
| CANCELADA | Dada de baja manualmente | No |

---

## 7. Módulo: Reservas / Agendas

Gestión de la ocupación puntual de cada clase: quién tiene un lugar reservado, listas de espera y asistencia. Sigue el ciclo **ABMR**.

### 7.1 Alta — Reservar una clase

**Reserva individual (staff):**
1. Abrir la clase deseada (Clases → detalle).
2. En la tabla de reservas, hacer clic en **"Reservar cliente"**.
3. Elegir cliente y, si tiene varias suscripciones activas, la suscripción a usar.
4. La app valida créditos disponibles, cupo libre y que no exista ya una reserva duplicada.
5. Confirmar. La reserva queda con estado "confirmada" (booked).

**Reserva individual (cliente, desde su panel):**
1. Ir a la pestaña **"Reservar"**.
2. Elegir una clase disponible (verde = con lugar) dentro del horizonte de reserva habilitado (ej. próximos 30-90 días).
3. Elegir la suscripción a usar si tiene más de una aplicable.
4. Confirmar. Se descuenta 1 crédito y se crea la reserva.

**Reserva masiva — un cliente, varias clases:**
1. Ir a **Agendamiento Masivo** (o desde Renovaciones).
2. Elegir cliente, ver sus créditos disponibles por actividad.
3. Filtrar clases por actividad, día, horario o profesor y marcar (tildar) las que se quieren agendar.
4. Validar (la app chequea créditos, cupo y duplicados) y confirmar. Se crean todas las reservas de una vez.

**Reserva masiva — varios clientes, varias clases:**
1. Ir a **Agendamiento Masivo** con selección de clientes (ej. lote de renovaciones).
2. Para cada cliente, elegir modo **Plantilla** (usa un patrón guardado y busca automáticamente esos horarios en el nuevo período) o **Manual** (tildar clase por clase).
3. Validar el lote completo (muestra resumen: clientes, clases, errores) y confirmar. Se procesa todo junto y al final se informa qué salió bien y qué falló.

**Plantillas:** se pueden guardar patrones de horarios recurrentes de un cliente con **"Guardar como plantilla"**, para reutilizarlos en próximas reservas o renovaciones con un clic.

### 7.2 Baja — Cancelar una reserva

**Cancelación individual (staff):**
1. En la tabla de reservas de la clase, hacer clic en **"Cancelar"** (ícono X) en la fila del cliente.
2. Elegir motivo (ej. "Cliente solicitó", "Inasistencia", "Problema de salud") y decidir si se devuelve el crédito (checkbox).
3. Confirmar. El cupo se libera de inmediato.

**Cancelación por el propio cliente:**
1. En "Mis clases", elegir la reserva a cancelar.
2. La app valida si todavía está dentro del plazo permitido (ej. no se puede cancelar el mismo día o dentro de las X horas previas a la clase).
3. Si está en plazo, confirmar cancelación; el crédito se devuelve automáticamente.

**Cancelación masiva:** al cancelar una clase completa (ver [5.2](#52-baja--cancelar-o-eliminar-una-clase)), todas sus reservas se cancelan en conjunto y se puede optar por devolver créditos a todos los afectados.

> Nota — devolución vs. pérdida de crédito ("forfeit"): por defecto se devuelve el crédito. El staff puede optar por no devolverlo (ej. inasistencia sin aviso), según la política del estudio.

### 7.3 Modificación — Reagendar una reserva

**Por el staff:**
1. Ubicar la reserva (desde la clase o desde "Historial de agendas").
2. Hacer clic en **"Reagendar"**.
3. En el modal aparece la clase origen (a la izquierda, con motivo obligatorio) y un buscador de clase destino (a la derecha, solo muestra clases con cupo disponible).
4. Elegir la clase destino. La app valida cupo, créditos suficientes y que no haya ya una reserva en esa clase; si el cliente tiene un descuento restringido a ciertos horarios, avisa (sin bloquear).
5. Confirmar. Se cancela la reserva original y se crea la nueva en un solo paso (si algo falla, revierte todo).

**Por el propio cliente:**
1. En "Mis clases", elegir **"Reagendarme"** sobre una reserva confirmada.
2. Buscar la clase destino filtrando por fecha y día de semana.
3. Confirmar, sujeto a las mismas validaciones (créditos, cupo, horizonte de reserva permitido, no reagendar a último momento).

### 7.4 Renovación — Renovar la agenda periódica

Cuando la suscripción de un cliente se renueva (ver [6.5](#65-renovación--renovar-una-suscripción-al-vencer)), su agenda se renueva junto con ella:

- Si el cliente tiene una **plantilla activa**, sus clases habituales se buscan automáticamente en el nuevo período y se agendan en bloque.
- Si no tiene plantilla, se usa agendamiento masivo manual para elegir las clases del nuevo período.

### 7.5 Lista de espera (waitlist)

Cuando una clase está llena:

1. El cliente (o el staff en su nombre) puede pedir un lugar: **"Pedir horario"**, indicando actividad/horario deseado y hasta cuándo vale el pedido.
2. El pedido queda en estado "esperando".
3. Si se libera un lugar (por una cancelación), el sistema identifica los pedidos en espera para esa clase y notifica al cliente.
4. El staff puede **"Convertir a reserva"** el pedido: se transforma en una reserva confirmada y se descuenta el crédito correspondiente.

### 7.6 Registro de asistencia

En el detalle de la clase, tabla de reservas, columna "Asistencia": staff y profesores pueden marcar **Presente** o **Ausente** por cada alumno (estado inicial: "sin confirmar"). El cliente puede ver su estado, pero no marcarlo él mismo.

---

## 8. Módulo: Pagos

Registro manual de cobros y su trazabilidad. No hay cobro automático ni pasarela online: todo pago lo carga el staff después de recibir el dinero por el medio que sea (efectivo, transferencia, tarjeta, etc.).

### 8.1 Alta — Registrar un pago nuevo

1. Ir a **Pagos → Cobranzas** (o desde la ficha del cliente → sección Pagos).
2. Ubicar la suscripción a cobrar y hacer clic en **"+ Registrar pago"**.
3. Completar:
   - **Método de pago*** (efectivo, tarjeta, transferencia, cheque, etc.)
   - **Cuenta** (opcional — ej. VISA, banco específico, si el método lo requiere)
   - **Monto*** (por defecto trae el saldo pendiente; se puede editar para un pago parcial)
   - **Fecha del pago*** (no puede ser futura)
   - **Notas** (opcional)
4. Confirmar con **"Registrar pago"**.

**Registro en lote:** en Cobranzas se pueden seleccionar varias suscripciones con checkbox y usar **"Registrar pagos masivos"** cuando el método/cuenta es el mismo para todas.

**Efecto automático:** el estado de facturación de la suscripción se recalcula solo (PAGADO si cubre el 100%, PARCIAL si cubre una parte) y queda un registro de auditoría (quién, cuándo, cuánto).

### 8.2 Baja — Revertir o reembolsar un pago

Los pagos **nunca se eliminan**; se documentan con una reversión, para mantener la trazabilidad.

1. En Cobranzas, ubicar la suscripción con el pago a revertir.
2. Abrir el menú de acciones → **"Revertir pago"**.
3. Completar:
   - **Motivo*** — Reembolso (se devolvió el dinero al cliente) o Cancelación (fue un error de carga).
   - Método y cuenta (deben coincidir con el pago original).
   - Monto (por defecto el total pagado; puede ser parcial).
   - Fecha.
4. Confirmar. El estado de facturación vuelve a PENDIENTE (reversión total) o PARCIAL (reversión parcial).

### 8.3 Modificación — "Editar" un pago

No existe edición directa de un pago ya registrado (por control de auditoría). Para corregir un error:
1. Revertir el pago incorrecto (motivo "Cancelación").
2. Registrar un nuevo pago con los datos correctos.

Quedan ambos movimientos en el historial, permitiendo reconstruir qué pasó.

### 8.4 Estados de facturación

| Estado | Significa |
|---|---|
| **PAGADO** | Se cobró el 100% del precio final |
| **PENDIENTE** | Todavía no se registró ningún pago |
| **PARCIAL** | Se cobró una parte, falta el resto |
| **MORA (OVERDUE)** | Venció el plazo y sigue sin estar pagado |
| **PROMESA DE PAGO** | El cliente se comprometió a pagar en una fecha; el staff lo marca manualmente desde Cobranzas → "Activar con promesa de pago" |

### 8.5 Recibos y comprobantes

Desde Pagos (o desde la ficha del cliente), cada pago tiene la acción **"Generar recibo"**, disponible en formato PDF o DOC, con los datos del estudio (logo, contacto) tomados de Configuración → General. También existe un generador de recibo personalizado para casos no vinculados a una suscripción del sistema.

### 8.6 Configuración: métodos y cuentas de pago

- **Método de pago** = el tipo general (Efectivo, Tarjeta, Transferencia, etc.). Se configura en Configuración → Métodos de Pago.
- **Cuenta de pago** = una subdivisión de un método (ej. "VISA 1234" dentro de Tarjeta). Se configura en Configuración → Cuentas de Pago.
- Opcionalmente, un producto de suscripción puede restringirse a aceptar solo ciertos métodos de pago (se define al editar el producto).

### 8.7 Grillas y reportes

- **Pagos**: historial completo de pagos (completados, reembolsados, cancelados), filtrable por fecha, cliente, método, cuenta y estado; exportable a Excel.
- **Cobranzas**: solo las suscripciones con saldo pendiente (PENDIENTE, PARCIAL, MORA, PROMESA), con columna de saldo y acceso directo a "Registrar pago"/"Revertir pago"; también exportable a Excel con totales.

---

## 9. Flujo de ejemplo end-to-end

Un ciclo típico, combinando los cinco módulos:

1. **Clientes** — Se da de alta a Juan (nombre, contacto, documento, contraseña inicial).
2. **Suscripciones** — Se le vende el plan "8 Clases Mensuales" (Alta), con horarios fijos lunes y miércoles 18:00.
3. **Reservas** — Al vender con plantilla, se agendan automáticamente sus clases del mes (Alta masiva).
4. **Pagos** — Se registra el cobro del plan (Alta de pago), quedando la suscripción en estado PAGADO.
5. **Clases** — Un miércoles el profesor falta: el staff cancela esa clase puntual (Baja de clase), devolviendo el crédito a todos los inscriptos, incluido Juan.
6. **Reservas** — Juan reagenda su clase perdida a otro horario disponible esa misma semana (Modificación de reserva).
7. **Suscripciones** — A fin de mes, el plan de Juan está por vencer: se lo renueva desde el cockpit de Renovaciones, con la misma plantilla de horarios (Renovación).
8. **Pagos** — Se registra el nuevo cobro del período renovado (Alta de pago).
9. **Clientes** — Meses después, Juan deja el estudio; como ya tiene historial, se lo **bloquea** con motivo "Solicitud propia" en lugar de eliminarlo (Baja de cliente).

---

## 10. Notas para agentes IA

- Este documento describe **comportamiento funcional observado en el código de la aplicación** (componentes de React/TypeScript), no un documento de marketing: los nombres de botones y campos citados intentan coincidir con los que ve el usuario en pantalla, pero pueden variar levemente entre versiones o entre estudios (white-label).
- El marco **ABMR** es el criterio de organización pedido para este manual; no todos los módulos tienen los cuatro procesos: **Clientes** y **Pagos** no tienen "Renovación" propia; **Clases** no tiene "Renovación" propia (la tienen las Suscripciones y, en consecuencia, las Reservas asociadas a ellas).
- Ante una pregunta de un usuario sobre "cómo hacer algo", identificar primero el módulo (Clientes/Clases/Suscripciones/Reservas/Pagos) y luego la etapa ABMR correspondiente (Alta/Baja/Modificación/Renovación) antes de responder.
- Si la pregunta involucra permisos o visibilidad de menú, recordar que el sidebar de Staff es dinámico y depende de permisos por usuario: la ausencia de una opción en pantalla no siempre es un bug, puede ser una restricción de permisos.
- Para dudas de implementación técnica (no funcionales), remitir a la documentación de `docs/estandares/` del repositorio, en particular el canon transaccional de Ventas/Modificaciones/Renovación.
