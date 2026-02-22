# 📄 Planeación del Sistema

## Desglose de trabajo parte 2: Épicas, Historias de Usuario y Tareas

La implementación de los requerimientos identificados de Bankify se desglosa de la siguiente manera:

### 1. Épica:

| Campo | Descripción |
|--|----|
| **ID** | EP-05 |
|**Titulo**| *Consulta de saldo*|
| **Descripción** | *Permitir que un cliente autenticado visualice sus cuentas asociadas y consulte el saldo e información básica de una cuenta activa, manejando casos de cliente sin cuentas, cuenta inactiva y fallos de consulta, y dejando registro en auditoría.* |
| **Stakeholder** | *El cliente*|

### 2. Historias de usuario:

| Campo | Descripción |
|-|----|
| **ID** | HU-01 |
|**Titulo**| *Visualizar mis cuentas*|
| **Descripción** | *Como Cliente quiero ver la lista de mis cuentas asociadas para seleccionar una cuenta y consultar su saldo.* |
| **Prioridad** | *[Alta]* |
| **Estimación** | *Puntos de historia* |

| Campo | Descripción |
|-|----|
| **ID** | HU-02|
|**Titulo**| *Consultar saldo de una cuenta activa*|
| **Descripción** | *Como Cliente quiero seleccionar una cuenta activa y ver su saldo e información básica para conocer el estado de mi dinero.* |
| **Prioridad** | *[Alta]* |
| **Estimación** | *Puntos de historia* |

| Campo | Descripción |
|-|----|
| **ID** | HU-03|
|**Titulo**| *Validaciones y mensajes de consulta*|
| **Descripción** | *Como Cliente quiero recibir un mensaje claro si no tengo cuentas, si la cuenta está inactiva o si ocurre un fallo en la consulta para entender qué pasó y qué hacer.* |
| **Prioridad** | *[Media]*|
| **Estimación** | *Puntos de historia* |

| Campo | Descripción |
|-|----|
| **ID** | HU-04|
|**Titulo**| *Registrador de auditoría de consulta*|
| **Descripción** | *Como Sistema (Bankify) quiero registrar en auditoría cada consulta de saldo para mantener trazabilidad y control.* |
| **Prioridad** | *[Media]*|
| **Estimación** | *Puntos de historia* |

### 3. Tareas:

## HU-01 — Visualizar mis cuentas

| Campo                             | Descripción                                                                                                                                                |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **IDENTIFICACIÓN**                    | TR-01                                                                                                                                                      |
| **Título**                            | Crear modelo y repositorio para cuentas del cliente                                                                                                        |
| **ID de la Historia de Uso asociada** | HU-01                                                                                                                                                      |
| **Descripción**                      | Como Desarrollador quiero crear las clases de dominio y el repositorio para consultar las cuentas asociadas a un cliente autenticado para poder listarlas. |
| **Tareas requisito**                  |                                                                                                                                                            |


| Campo                             | Descripción                                                                                                                                           |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **IDENTIFICACIÓN**                    | TR-02                                                                                                                                                 |
| **Título**                            | Implementar serviciolistarCuentas(clienteId)                                                                                                          |
| **ID de la Historia de Uso asociada** | HU-01                                                                                                                                                 |
| **Descripción**                       | Como Desarrollador quiero implementar un servicio que liste las cuentas del cliente autenticado para soportar el flujo de “listar cuentas asociadas”. |
| **Tareas requisito**                  | TR-01                                                                                                                                                 |

| Campo                             | Descripción                                                                                                                                                                   |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **IDENTIFICACIÓN**                    | TR-03                                                                                                                                                                         |
| **Título**                            | Crear pruebas JUnit del listado y caso “sin cuentas” (A1)                                                                                                                     |
| **ID de la Historia de Uso asociada** | HU-01                                                                                                                                                                         |
| **Descripción**                       | Como Equipo quiero validar con pruebas JUnit el listado de cuentas y el escenario donde el cliente no tiene cuentas para asegurar el comportamiento del flujo alternativo A1. |
| **Tareas requisito**                  | TR-01, TR-02                                                                                                                                                                  |

## HU-02 — Consultar saldo de una cuenta activa

| Campo                             | Descripción                                                                                                                         |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **IDENTIFICACIÓN**                    | TR-04                                                                                                                               |
| **Título**                            | Implementar servicioconsultarSaldo(cuentaId)                                                                                        |
| **ID de la Historia de Uso asociada** | HU-02                                                                                                                               |
| **Descripción**                       | Como Desarrollador quiero implementar la lógica que obtiene el saldo e información básica de una cuenta para retornarla al cliente. |
| **Tareas requisito**                  | TR-01                                                                                                                               |

| Campo                             | Descripción                                                                                                                                   |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **IDENTIFICACIÓN**                    | TR-05                                                                                                                                         |
| **Título**                            | Exponer operación/controlador para “Consultar saldo”                                                                                          |
| **ID de la Historia de Uso asociada** | HU-02                                                                                                                                         |
| **Descripción**                       | Como Cliente autenticado quiero ejecutar la operación “Consultar saldo” sobre una cuenta seleccionada para ver su saldo e información básica. |
| **Tareas requisito**                  | TR-04                                                                                                                                         |

| Campo                             | Descripción                                                                                                                           |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **IDENTIFICACIÓN**                    | TR-06                                                                                                                                 |
| **Título**                            | Pruebas JUnit del flujo principal de consulta                                                                                         |
| **ID de la Historia de Uso asociada** | HU-02                                                                                                                                 |
| **Descripción**                       | Como Equipo quiero verificar con pruebas JUnit que la consulta de una cuenta activa retorna saldo e información básica correctamente. |
| **Tareas requisito**                  | TR-04, TR-05                                                                                                                          |

## HU-03 — Validaciones y mensajes de consulta

| Campo                             | Descripción                                                                                                                                   |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **IDENTIFICACIÓN**                    | TR-07                                                                                                                                         |
| **Título**                            | Validar que la cuenta esté activa antes de consultar (A2)                                                                                     |
| **ID de la Historia de Uso asociada** | HU-03                                                                                                                                         |
| **Descripción**                       | Como Sistema quiero impedir la consulta si la cuenta está inactiva y devolver un mensaje/resultado adecuado para cumplir el flujo alterno A2. |
| **Tareas requisito**                  | TR-04                                                                                                                                         |

| Campo                             | Descripción                                                                                                            |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **IDENTIFICACIÓN**                    | TR-08                                                                                                                  |
| **Título**                            | Manejo de fallos de consulta (A3) con excepción controlada                                                             |
| **ID de la Historia de Uso asociada** | HU-03                                                                                                                  |
| **Descripción**                       | Como Sistema quiero manejar fallos de consulta devolviendo un error claro al cliente para cumplir el flujo alterno A3. |
| **Tareas requisito**                  | TR-04, TR-05                                                                                                           |

| Campo                             | Descripción                                                                                                                                 |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **IDENTIFICACIÓN**                    | TR-09                                                                                                                                       |
| **Título**                            | Pruebas JUnit de A2 (inactiva) y A3 (fallo)                                                                                                 |
| **ID de la Historia de Uso asociada** | HU-03                                                                                                                                       |
| **Descripción**                       | Como Equipo quiero cubrir con pruebas JUnit los escenarios de cuenta inactiva y fallo de consulta para asegurar el comportamiento esperado. |
| **Tareas requisito**                  | TR-07, TR-08                                                                                                                                |

## HU-04 — Auditoría de consulta

| Campo                             | Descripción                                                                                                 |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **IDENTIFICACIÓN**                    | TR-10                                                                                                       |
| **Título**                            | Crear componente de auditoría (modelo + repositorio/DAO)                                                    |
| **ID de la Historia de Uso asociada** | HU-04                                                                                                       |
| **Descripción**                       | Como Sistema quiero persistir un registro de auditoría por consulta de saldo para mantener la trazabilidad. |
| **Tareas requisito**                  |                                                                                                             |

| Campo                             | Descripción                                                                                                                                           |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **IDENTIFICACIÓN**                    | TR-11                                                                                                                                                 |
| **Título**                           | Registrar auditoría en consultarSaldo(éxito)                                                                                                          |
| **ID de la Historia de Uso asociada** | HU-04                                                                                                                                                 |
| **Descripción**                       | Como Sistema quiero registrar la consulta (cliente, cuenta, marca de tiempo, resultado) cuando la consulta sea exitosa para cumplir la postcondición. |
| **Tareas requisito**                  | TR-04, TR-10                                                                                                                                          |

| Campo                             | Descripción                                                                                                                           |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **IDENTIFICACIÓN**                    | TR-12                                                                                                                                 |
| **Título**                            | Pruebas JUnit de auditoría (se genera registro al consultar saldo)                                                                    |
| **ID de la Historia de Uso asociada** | HU-04                                                                                                                                 |
| **Descripción**                       | Como Equipo quiero verificar con pruebas JUnit que cada consulta de saldo genere su registro de auditoría para asegurar trazabilidad. |
| **Tareas requisito**                  | TR-11                                                                                                                                 |
