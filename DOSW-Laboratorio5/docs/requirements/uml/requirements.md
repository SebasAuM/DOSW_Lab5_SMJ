# Bankify - Requirements

## 1. Contexto del sistema 
Bankify es un sistema para la gestión básica de cuentas bancarias que permite a clientes consultar saldos y realizar depósitos. Roles internos (Asesor, Supervisor y Gerente Financiero) administran cuentas/clientes y gestionan reportes tributarios. Bankify integra un proveedor externo de pagos (PSE) para el procesamiento de depósitos y envía reportes tributarios a la DIAN en formato JSON; adicionalmente genera reportes tributarios en PDF para el cliente.

---

## 2. Requerimientos funcionales (RF)
RF-01. El sistema debe permitir autenticación con usuario y contraseña para Cliente, Asesor, Supervisor y Gerente Financiero.  
RF-02. El sistema debe permitir al Supervisor crear, actualizar, activar, inactivar y eliminar clientes.  
RF-03. El sistema debe permitir al Asesor crear, actualizar, activar e inactivar cuentas bancarias.  
RF-04. El sistema debe validar que el número de cuenta tenga exactamente 10 dígitos, sea numérico y que el banco (primeros 2 dígitos) esté registrado.  
RF-05. El sistema debe permitir al Cliente consultar el saldo de sus cuentas activas.  
RF-06. El sistema debe permitir al Cliente realizar depósitos a una cuenta propia o autorizada e integrarse con PSE para procesar la operación y recibir confirmación.  
RF-07. El sistema debe generar reportes tributarios del cliente en formato PDF.  
RF-08. El sistema debe permitir al Gerente Financiero generar y enviar reportes tributarios en formato JSON a la DIAN.

---

## 3. Requerimientos no funcionales (RNF)
RNF-01 (Seguridad). Las contraseñas deben almacenarse usando hash con salt y nunca en texto plano.  
RNF-02 (Auditoría). El sistema debe registrar en auditoría operaciones sensibles como depósitos, activación/inactivación, eliminación de clientes y envío de reportes a DIAN.  
RNF-03 (Rendimiento). La consulta de saldo debe responder en menos de 2 segundos bajo condiciones normales.  
RNF-04 (Integridad). El depósito debe ser atómico: si PSE no confirma el pago, el sistema no debe actualizar el saldo.  
RNF-05 (Disponibilidad). El sistema debe tener disponibilidad mínima del 99% durante horario operativo.  
RNF-06 (Trazabilidad). Cada reporte enviado a DIAN debe quedar asociado a un identificador único y un estado (enviado/aceptado/rechazado).

---

## 4. Requerimientos funcionales detallados 


### RF-01 — Autenticación de usuarios

Objetivo: Permitir el acceso seguro al sistema a usuarios con rol Cliente, Asesor, Supervisor y Gerente Financiero.

Actores: Cliente, Asesor, Supervisor, Gerente Financiero.

Precondiciones:

El usuario está registrado en el sistema.

El usuario está activo (no bloqueado/inactivo).

Flujo principal:

1.El usuario selecciona la opción “Iniciar sesión”.

2.El usuario ingresa usuario y contraseña.

3.Bankify valida las credenciales.

4.Bankify identifica el rol del usuario.

5.Bankify inicia la sesión y muestra el panel principal según rol.

Flujos alternos / Excepciones:

A1. Credenciales inválidas → Bankify rechaza el acceso y muestra mensaje de error.

A2. Usuario inactivo/bloqueado → Bankify rechaza el acceso y notifica el estado.

A3. Fallo del sistema → Bankify informa error y registra el incidente.

Postcondiciones:

Sesión iniciada (o rechazada) y evento registrado para auditoría.

### RF-05 — Consulta de saldo

Objetivo: Permitir que el Cliente consulte el saldo de sus cuentas activas.

Actores: Cliente.

Precondiciones:

Cliente autenticado.

El cliente tiene al menos una cuenta registrada (idealmente activa).

Flujo principal:

1.El cliente selecciona “Consultar saldo”.

2.Bankify lista las cuentas asociadas al cliente.

3.El cliente selecciona una cuenta.

4.Bankify muestra el saldo y la información básica de la cuenta.

Flujos alternos / Excepciones:

A1. Cliente sin cuentas → Bankify muestra mensaje informativo (sin datos).

A2. Cuenta inactiva → Bankify no permite la consulta y notifica.

A3. Fallo de consulta → Bankify muestra error y registra el incidente.

Postcondiciones:

La consulta queda registrada en auditoría.

- link de los mockups: https://www.figma.com/design/ygIKa3N8NdOkMEcdnSU5FP/RF05_01-Mis-cuentas?node-id=2-53&p=f&t=HRnwKM8F16TczLYi-0

### RF-06 — Realizar depósito

Objetivo: Permitir que el Cliente realice un depósito a una cuenta propia o autorizada, integrándose con PSE para procesar el pago.

Actores: Cliente, PSE (sistema externo).

Precondiciones:

Cliente autenticado.

El cliente ingresa una cuenta destino y un monto.

PSE se encuentra disponible para procesar la operación.

Reglas de negocio aplicadas (del caso):

La cuenta destino debe tener exactamente 10 dígitos y contener solo números.

Los dos primeros dígitos representan el banco y deben corresponder a un banco registrado en el sistema.


Flujo principal:

1.El cliente selecciona “Realizar depósito”.

2.El cliente ingresa cuenta destino y monto.

3.Bankify valida el formato de cuenta y el banco.

4.Bankify valida que el monto sea mayor que 0.

5.Bankify solicita confirmación al cliente.

6.Bankify envía la solicitud de procesamiento a PSE.

7.PSE responde confirmando el resultado de la transacción.

8.Si la transacción fue exitosa, Bankify registra la transacción y actualiza el saldo.

9.Bankify notifica al cliente el resultado del depósito.

Flujos alternos / Excepciones:

A1. Cuenta inválida (no 10 dígitos / no numérica) → Bankify rechaza y notifica.

A2. Banco no registrado → Bankify rechaza y notifica.

A3. Monto inválido (<= 0) → Bankify rechaza y notifica.

A4. PSE rechaza transacción → Bankify no actualiza saldo y notifica rechazo.

A5. Falla de comunicación con PSE → Bankify no actualiza saldo, registra incidente y notifica.

A6. Error interno al actualizar saldo → Bankify revierte/compensa y registra incidente.

Postcondiciones:

Si se confirmó pago por PSE: transacción registrada y saldo actualizado.

Si no se confirmó: saldo no cambia y queda registro del intento.


## 5. Análisis de requerimientos (Punto 7)

### 7a) ¿Identifica algún requerimiento que deba detallarse más? ¿Cuál(es)?
Sí. El requerimiento de **depósitos (RF-06)** debe detallarse más, porque faltan reglas clave como: límites de monto, manejo de depósitos por “otros usuarios” (qué significa autorización), estados de la transacción (pendiente/aprobada/rechazada) y política de reversión/compensación ante fallas.
También el requerimiento de **reporte a DIAN (RF-08)** requiere mayor detalle: estructura exacta del JSON, validaciones, manejo de acuse o rechazo y trazabilidad (radicado/estado).

### 7b) ¿Existen requerimientos que se contradigan entre sí? ¿Cuál(es)?
No hay contradicciones directas, pero sí **ambigüedades**:
- “Depósito por parte del cliente propietario u otros usuarios” puede entrar en conflicto con seguridad si no se define quiénes son “otros usuarios” y cómo se autoriza.
- “Eliminar un cliente y sus cuentas asociadas” puede entrar en conflicto con trazabilidad/auditoría, ya que en contextos financieros normalmente se inactiva y se conserva historial. Si se elimina, debe definirse claramente qué ocurre con los registros históricos.

### 7c) Si tuviera que dar prioridad, ¿cuáles serían los 2 más importantes para una primera iteración?
1. **RF-01 Autenticación** (base para control de acceso y seguridad por roles).
2. **RF-05 Consultar saldo + RF-06 Realizar depósito** (operación principal del MVP).  
   Nota: si se deben escoger solo dos estrictos, se prioriza RF-01 y RF-06, porque el depósito valida el modelo de negocio y la integración con PSE.

### 7d) ¿Existe algún requerimiento que no debería realizarse?

Para una primera iteración, el envío de reportes a DIAN en JSON (RF-08) podría posponerse si no hay especificación clara del formato, ya que implica complejidad regulatoria y validaciones adicionales. En cambio, se puede iniciar con el reporte PDF al cliente (RF-07) y dejar RF-08 para una iteración posterior.

---



