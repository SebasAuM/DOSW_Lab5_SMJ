
#  Requerimientos del Sistema

## 1. Sistema

* Nombre del sistema: Bankify - Sistema de Gestion de Cuentas Bancarias 
* Objetivo: El sistema tiene como objetivo gestionar de manera centralizada las cuentas bancarias de los clientes de Bankify,permitiendo el regustro validado de cuentas , consultas de saldos, realizacion de depósitos controlados y generación de reportes tributarios tanto para clientes como para la DIAN, ganarantizando el cumplimiento de las reglas de negocio.

## 2. Problema a resolver

Actualmente Bankify no cuenta con un sistema centralizado que permita registra:
*  Registra cuentas bancarias de manera validada segun las reglas de negocio.
*  Consultar el saldo de las cuentas de forma segura.
*  Realizar depósitos de dinero de forma controlada a través de PSE.
*  Generar reportes tributarios personalizados para los clientes en formato PDF.
*  Enviar reportes tributarios consolidados a la DIAN en formato JSON.
  
El sistema debe garantizar que las cuentas creadas cumplan con las reglas específicas del negocio (números de cuenta de 10 dígitos, validación de banco asociado) y que los clientes puedan interactuar con ellas de forma sencilla y segura mediante autenticación controlada por roles.

## 3. Diagrama de Contexto

### 3.1 Diagrama
<img width="4930" height="2475" alt="Diagrama de contexto LAB4 DOS" src="https://github.com/user-attachments/assets/8a81b85f-784f-4896-8381-7dcb5b123c2f" />

Relacionar imagen del diagrama de contexto realizado

### 3.2 Actores

<En el siguiente cuadro, mapee los actores o roles identificados del sistema>


| Actor / Rol | Descripción |
|-------------|-------------|
| Usuario final / Cliente | Cliente del sistema de Bankify que consulta saldos, realiza depósitos, inactiva sus propias cuentas y genera reportes tributarios personales. |
| Asesor | Empleado de Bankify que gestiona todas las operaciones sobre cuentas bancarias (crear, actualizar, activar, inactivar). |
| Supervisor | Empleado de Bankify que gestiona la información de los clientes (crear, actualizar, activar, inactivar y eliminar clientes). |
| Gerente Financiero | Empleado de Bankify responsable de generar reportes tributarios consolidados de todas las cuentas para enviarlos a la DIAN. |


### 3.3 Sistemas externos

<En el siguiente cuadro, mapee los sistemas externos que interactúan con el sistema de Bankify>

| Sistema | Descripción |
|---------|-------------|
| PSE | Sistema de pagos electrónicos que procesa los depósitos realizados a las cuentas bancarias del sistema Bankify. |
| DIAN | Entidad gubernamental que recibe los reportes tributarios consolidados en formato JSON de todas las cuentas registradas en el sistema. |



## 4. Alcance del sistema
   
### 4.1 Dentro del sistema

Funciones que el sistema SÍ realiza:

* Autenticación de usuarios con usuario y contraseña (clientes, asesores, supervisores, gerente financiero).
* Gestión de clientes: crear, actualizar, activar, inactivar y eliminar clientes.
* Gestión de cuentas bancarias: crear, actualizar, activar e inactivar cuentas.
* Validación de números de cuenta (10 dígitos, solo números, validación de banco).
* Consulta de saldos de cuentas por parte de clientes.
* Registro de depósitos realizados a través de PSE.
* Generación de reportes tributarios individuales en formato PDF para clientes.
* Generación de reportes tributarios consolidados en formato JSON para la DIAN.



### 4.2 Fuera del sistema

Funciones que NO realiza:

* Procesamiento real de transacciones de pago (lo hace PSE).
* Realizar retiros de dinero de las cuentas.
* Transferencias entre cuentas.
* Gestión de préstamos o créditos.
* Cálculo automático de impuestos (solo genera reportes con información de las cuentas).
* Notificaciones por correo electrónico o SMS.
* Aplicación móvil nativa.
* Integración con otros sistemas bancarios externos.
