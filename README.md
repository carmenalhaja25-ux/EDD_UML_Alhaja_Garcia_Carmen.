# EDD_UML_Alhaja_Garcia_Carmen.
1. Explicación técnica del proceso modelado.

El proceso comienza con el usuario interactuando con la interfaz "Finalizar Compra". Inmediatamente el sistema utiliza una decisión para optimizar el tiempo de respuesta:
- Verificación de Stock: Se consulta la disponibilidad de los artículos en Stock/Tiempo real.
- Verificación Validez de la Sesión: Se conifrma que el token del usuario siga activo y sea seguro.
- Sincronización: Otra descisión actúa como punto de reunión, el proceso no avanza hasta que ambas tareas finalizen con éxito.

Seguidamente, para controlar los errores, el flujo toma una decisión. Hay que evaluar el estado para verificar que las validaciones anteriores fueron correctas. Si falla lleva a un Error y el flujo termina en Error de Validación, en cambio, si es correcta, hay éxito y se pasa a la Pasarela de Pago Seguro. 

Una vez confirmado el pago, el sistema entra en una fase de concurrencian crítica en la que ejecuta tres servicios independientes de forma simultánea para mejorar la eficiencia del backend:
- Registro del pedido en la base de datos.
- Generación del PDF de la factura.
- Envío de notificación por correo electrónico.

Finalmente, tras sincronizar las tareas post-pago, el sistema muestra el mensaje de confirmación al cliente, alcanzando el estado final de "Confirmación mostrada".


2. Inserción de la imagen del diagrama.

<img width="1351" height="279" alt="DiagramaEEDD drawio" src="https://github.com/user-attachments/assets/7749ce8f-a96f-4cba-9324-fed9d39b828d" />


3. Justificación del uso de los nodos de sincronización.

- Nodos de Tareas(Rectángulos): Se usan para encapsular operaciones atómicas. Permiten la modularidad del código, facilitan el mantenimiento ya que cambian la lógica del inventario y no es necesario modificar la lógica de autenticidad de sesión.
- Nodos de división(Flujos concurrentes y desordenados): Marcan el inicio de flujos de actividades en paralelo, evita cmeter errores de enredos, esencialmente facilita el proceso.

4. Bibliografía utilizada siguiendo el estilo IEEE.
