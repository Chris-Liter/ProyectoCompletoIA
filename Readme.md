# PRÁCTICA APLICACIONES Y DEPLOYMENT

## Integrantes
- Sebastian Pesantez
- Martin Toledo
- Jorge Lituma
- Diego Loja
- Anthony Moya

## Descripción del Proyecto

El objetivo de este proyecto es desarrollar un sistema de chat bot dirigido a médicos y nutricionistas. Este sistema está compuesto por varios componentes de backend y frontend que colaboran para ofrecer una solución integral. A continuación, se detallan los componentes y su propósito.

## **Backend**

### API con Django
Esta API está diseñada para gestionar el modelo de predicción de inteligencia artificial que utilizará el chat bot de Telegram. La API se encuentra desplegada en una máquina virtual de Google Cloud (Compute Engine).

- **Tecnologías**: `pandas`, `numpy`, `scikit-learn`, `tensorflow`, `keras`, `django`, `djangorestframework`, `django-cors-headers`, `drf_yasg`, `django.shortcuts`, `awsebcli`.
- **Funcionalidad**: 
  - Procesamiento y predicción de datos ingresados por los usuarios.
  - Gestión de los modelos de IA y sus endpoints.

### API con Spring Boot
Esta API se encarga exclusivamente de la gestión de la base de datos PostgreSQL, proporcionando una interfaz segura y eficiente para las operaciones CRUD (Crear, Leer, Actualizar, Eliminar) requeridas por la aplicación frontend.

- **Tecnologías**: Spring Boot, PostgreSQL
- **Funcionalidad**: 
  - Gestión de usuarios (médicos y pacientes).
  - Gestión de turnos.
  - Integración con el frontend para asegurar una comunicación fluida y segura.
- **Despliegue**: La API está desplegada en `render.com`.

## **Frontend**

### Página Web en Angular
La página web está diseñada específicamente para ser utilizada por médicos y nutricionistas. Ofrece una interfaz amigable para gestionar pacientes, turnos, y visualizar los resultados y recomendaciones generadas por el modelo predictivo.

- **Tecnologías**: Angular, TypeScript, SCSS, HTML
- **Funcionalidad**: 
  - Autenticación y autorización de usuarios(Medico/Nutricionista).
  - Gestión de turnos.
  - Visualización de datos y resultados de las predicciones del modelo de IA.

### Script de Chat Bot en Python
Este script se encarga del funcionamiento del chat bot en Telegram, interactuando con los usuarios (pacientes) y utilizando la API de Django, y tambien la API de Google, `Speech to Text` para que los datos que el usuario diga en un audio de voz se conviertan a texto. Cuando el usuario otorga sus datos al chat, este realizara una predicción o un prediagnostico, para saber el grado de obesidad que el usuario podria tener, y este a su vez lo guarda en la misma base de datos PostgreSQL, donde el medico como tal podra ver los datos completos, incluyendo el prediagnostico que lo realiza el modelo de Redes Neuronales

- **Tecnologías**: Python, Librería de  `telegram` Bot, `telegram.ext`, Requests (para comunicación con la API), `google.cloud`, `google.oauth2`, `requests` entre otras más.
- **Funcionalidad**: 
  - Recepción y procesamiento de mensajes de los usuarios.
  - Conversion de voz a texto con la API de Speech to Text de Google
  - Comunicación con la API de Django para obtener respuestas predictivas.
  - Gestión de interacciones y respuestas automáticas.

## **Arquitectura del Sistema**

El sistema está diseñado para ofrecer una integración completa entre todos sus componentes, garantizando una experiencia fluida tanto para los usuarios finales (pacientes) como para los médicos y nutricionistas.

1. **Chat Bot (Telegram)**:
   - El usuario interactúa con el chat bot.
   - El chat bot envía los datos a la API de Django y esta predicción que haga se guardara en la base de datos.
   - La API de Django procesa los datos y devuelve la respuesta al chat bot, que luego se muestra al usuario.
   - El usuario podra elegir un medico con quien ajendar una cita, siempre y cuando el medico que elija, tenga turnos disponibles

2. **Aplicación Web (Angular)**:
   - Los médicos/nutricionistas acceden a la aplicación web.
   - La aplicación web se comunica con la API de Spring Boot para realizar operaciones en la base de datos.
   - Los datos de pacientes, turnos y resultados de predicciones se gestionan y visualizan en la interfaz web.

3. **API con Spring Boot**:
   - Gestiona todas las operaciones de base de datos.
   - Proporciona endpoints seguros para el frontend.

4. **API con Django**:
   - Gestiona el modelo de predicción de IA.
   - Proporciona endpoints para el chat bot.

## **Base de Datos**

La base de datos PostgreSQL se encuentra alojada en una máquina virtual de Google Cloud y contiene las siguientes tablas:

- **Usuarios**: Información de los usuarios (pacientes y médicos).
- **Médicos**: Nombre y Contraseña de los médicos/nutricionistas para poder Loguearse en el Sistema Web.
- **Turnos**: Información sobre las citas y turnos programados con cierto medico especificado.

## **Despliegue**

- **API con Django**: Desplegada en Google Cloud (Compute Engine).
- **API con Spring Boot**: Desplegada en render.com.
- **Base de Datos PostgreSQL**: Alojada en Google Cloud (Compute Engine).
- **Frontend Angular**: Desplegado en Firebase

## **Enfoque del Sistema**

Este sistema está diseñado para mejorar la interacción y gestión de pacientes por parte de médicos y nutricionistas. Al proporcionar una plataforma centralizada para la gestión de citas y el uso de inteligencia artificial para ofrecer recomendaciones predictivas, se busca optimizar el tiempo y los recursos de los profesionales de la salud, permitiendo un enfoque más eficiente y personalizado en el tratamiento de los pacientes.

## **Instrucciones de Uso**

### **Backend**

#### API con Django
1. Clonar el repositorio: https://github.com/Chris-Liter/API_IA
2. Simplemente ejecutar la imagen Docker para desplegar de forma rapida: https://hub.docker.com/repository/docker/chrisliter/proyectofinal/general
3. Descargada la imagen, simplemente ejecutar `docker run -d -it -p 8081:8001 chrisliter/proyectofinal`
4. O directamente entrar en la carpeta `miproyecto` y ejecutar el comando `python manage.py runserver 8001`

#### API con Spring Boot
1. Clonar el repositorio.
2. Instalar las dependencias: `mvn install`
3. Ejecutar la aplicación: `mvn spring-boot:run`
4. O tambien simplemente ejecutar la imagen docker, tambien subida en `DockerHub`: https://hub.docker.com/repository/docker/chrisliter/apiobesidadspringboot/general

### **Frontend**

#### Angular
1. Clonar el repositorio.
2. Instalar las dependencias: `npm install`
3. Ejecutar la aplicación: `ng serve`

### **Chat Bot**

#### Python
1. Clonar el repositorio.
2. Instalar las dependencias mencionadas en este README
3. Ejecutar el script del chat bot: `python botfinal.py`


Estos simples pasos para su ejecucion, pero como los servicios ya se encuentran desplegados, no es necesario realizar los pasos anteriormente mencionados.
Para probar los servicios, simplemente ingresar a https://t.me/obesidad_bot y ya se puede empezar a usar este ChatBot y agendar una cita medica si es que lo necesita.

## **Contribuciones**

Este archivo README proporciona una visión detallada del sistema, sus componentes y cómo se integran para ofrecer una solución completa y eficiente para la gestión de pacientes y el uso de inteligencia artificial en el campo de la salud.
