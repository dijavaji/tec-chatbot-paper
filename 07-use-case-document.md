# Documentación de Diagrama de Casos de uso - Sistema Smart de Chatbot

## Introducción

A continuación se presenta la descripción técnica del **Diagrama de Casos de Uso del Sistema Smart de Chatbot**

---

# 1. Diagrama de Casos de Uso

<div class="mxgraph" style="max-width:100%;border:1px solid transparent;" data-mxgraph="{&quot;highlight&quot;:&quot;#0000ff&quot;,&quot;lightbox&quot;:false,&quot;nav&quot;:true,&quot;resize&quot;:true,&quot;page&quot;:2,&quot;dark-mode&quot;:&quot;light&quot;,&quot;toolbar&quot;:&quot;pages zoom layers tags&quot;,&quot;edit&quot;:&quot;_blank&quot;,&quot;url&quot;:&quot;https://drive.google.com/uc?id=11qEmWJ0ir9RmQVn_2lMrIeYkJvzS8wEo&amp;export=download&quot;}"></div>
<script type="text/javascript" src="https://viewer.diagrams.net/embed2.js?&fetch=https%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D11qEmWJ0ir9RmQVn_2lMrIeYkJvzS8wEo%26export%3Ddownload"></script>

## 1.1 Descripción General

El diagrama de casos de uso representa las funcionalidades principales del **Sistema Smart de Chatbot**, así como la interacción entre los actores externos y los servicios proporcionados por la plataforma.

El sistema contempla dos actores principales:

* **Usuario del sitio (Site User)**, quien interactúa con el chatbot para consultar información y acceder a los servicios de conversación.
* **Administrador (Admin)**, responsable de la gestión del conocimiento, mantenimiento de la plataforma y actualización de la información utilizada por el modelo de inteligencia artificial.

El objetivo principal del sistema es ofrecer respuestas automáticas mediante técnicas de Inteligencia Artificial, utilizando una base de conocimiento previamente administrada por el personal autorizado.

---

# 1.2 Actores del Sistema

## Usuario del Sitio (Site User)

Representa cualquier usuario que accede al chatbot desde la aplicación web para consultar información.

### Responsabilidades

* Registrarse en la plataforma.
* Iniciar sesión.
* Enviar consultas al chatbot.
* Recibir respuestas generadas por la inteligencia artificial.
* Consultar su historial de conversaciones.

---

## Administrador (Admin)

Representa al personal encargado de administrar el funcionamiento del sistema y mantener actualizada la base de conocimiento.

### Responsabilidades

* Autenticarse en el sistema.
* Gestionar usuarios.
* Cargar documentos hacia la base de conocimiento.
* Administrar el CMS.
* Ejecutar procesos de aprendizaje automático.
* Supervisar el procesamiento de datos.

---

# 1.3 Descripción de los Casos de Uso

---

## CU-01. Registrar Usuario

### Objetivo

Permitir que un nuevo usuario cree una cuenta dentro del sistema para acceder a las funcionalidades del chatbot.

### Actor Principal

Usuario del Sitio.

### Descripción

El usuario proporciona la información requerida por el formulario de registro. Posteriormente, el sistema valida los datos y almacena la información del nuevo usuario.

### Flujo Principal

1. El usuario selecciona la opción de registro.
2. El sistema solicita los datos personales.
3. El usuario completa la información requerida.
4. El sistema valida los datos.
5. El sistema registra la nueva cuenta.
6. Se confirma el registro exitoso.

### Relación

**Incluye**

* Enviar datos del usuario (Send User Data).

---

## CU-02. Enviar Datos del Usuario

### Objetivo

Procesar y almacenar la información ingresada durante el registro.

### Actor Principal

Sistema.

### Descripción

Este caso de uso es invocado durante el proceso de registro y permite validar la integridad de la información antes de almacenarla en la base de datos.

---

## CU-03. Iniciar Sesión

### Objetivo

Permitir que un usuario autenticado acceda a los servicios del sistema.

### Actor Principal

Usuario del Sitio.

### Descripción

El sistema verifica las credenciales ingresadas y concede acceso únicamente cuando la autenticación es exitosa.

### Flujo Principal

1. El usuario ingresa correo y contraseña.
2. El sistema valida las credenciales.
3. Se ejecuta el proceso de autenticación.
4. Se concede acceso al sistema.

### Relaciones

**Es extendido por**

* Autenticación y autorización.

**Es incluido por**

* Consultar historial de conversaciones.

---

## CU-04. Autenticación y Autorización del Usuario

### Objetivo

Validar la identidad del usuario y determinar los permisos disponibles dentro del sistema.

### Actor Principal

Sistema.

### Descripción

Este proceso verifica la autenticidad de las credenciales y asigna el rol correspondiente para controlar el acceso a las funcionalidades disponibles.

---

## CU-05. Consultar Historial de Conversaciones

### Objetivo

Permitir que el usuario visualice las conversaciones previamente realizadas con el chatbot.

### Actor Principal

Usuario del Sitio.

### Descripción

El sistema recupera todas las conversaciones asociadas al usuario autenticado y las presenta ordenadas cronológicamente.

### Relación

**Incluye**

* Iniciar sesión.

---

## CU-06. Enviar Mensaje

### Objetivo

Permitir al usuario realizar consultas al chatbot.

### Actor Principal

Usuario del Sitio.

### Descripción

El usuario escribe una pregunta o solicitud y el sistema la envía al motor de inteligencia artificial para su procesamiento.

### Flujo Principal

1. El usuario escribe un mensaje.
2. El sistema recibe la consulta.
3. El mensaje es enviado al motor de IA.
4. Se inicia el procesamiento semántico.
5. Se genera una respuesta.

### Relaciones

**Incluye**

* Responder mensaje.

**Es extendido por**

* Motor de Machine Learning / Inteligencia Artificial.

---

## CU-07. Responder Mensaje

### Objetivo

Generar una respuesta automática basada en la información almacenada dentro de la base de conocimiento.

### Actor Principal

Sistema.

### Descripción

El motor de IA interpreta la consulta utilizando procesamiento del lenguaje natural y devuelve la respuesta más adecuada al usuario.

### Relaciones

**Es extendido por**

* Machine Learning / Inteligencia Artificial.

---

## CU-08. Cargar Base de Conocimiento / CMS

### Objetivo

Permitir al administrador incorporar nueva información al repositorio documental utilizado por el chatbot.

### Actor Principal

Administrador.

### Descripción

El administrador carga documentos o recursos mediante el CMS para ampliar la base de conocimiento utilizada por el sistema de inteligencia artificial.

### Flujo Principal

1. El administrador selecciona un documento.
2. El sistema valida el formato.
3. El documento es almacenado.
4. Se inicia el proceso de actualización del conocimiento.

---

## CU-09. Machine Learning / Inteligencia Artificial

### Objetivo

Procesar la información disponible para generar respuestas inteligentes y mantener actualizado el modelo de conocimiento.

### Actor Principal

Sistema.

### Descripción

Este constituye el núcleo funcional del chatbot. El módulo integra algoritmos de Inteligencia Artificial encargados de interpretar consultas, recuperar contexto, procesar información y generar respuestas precisas.

Asimismo, este componente administra el procesamiento de datos derivados de la carga documental realizada por el administrador.

### Relaciones

**Incluye**

* Ejecutar procesos ETL.
* Visualizar análisis e insights.

**Extiende**

* Enviar mensaje.
* Responder mensaje.

---

## CU-10. Ejecutar ETL

### Objetivo

Extraer, transformar y cargar la información proveniente de la base documental hacia el modelo de aprendizaje.

### Actor Principal

Sistema.

### Descripción

Este proceso normaliza la información recibida desde el CMS para que pueda ser utilizada por los algoritmos de aprendizaje automático y recuperación de conocimiento.

---

## CU-11. Visualización de Datos e Insights

### Objetivo

Mostrar información analítica relacionada con el desempeño del sistema y el procesamiento de datos.

### Actor Principal

Administrador.

### Descripción

El sistema genera indicadores que permiten supervisar el comportamiento del chatbot, el volumen de consultas, el procesamiento documental y la eficiencia del modelo de inteligencia artificial.

---

# 1.4 Relaciones entre Casos de Uso

El modelo incorpora relaciones **«include»** y **«extend»**, utilizadas para representar dependencias funcionales entre los distintos procesos.

### Relaciones «include»

Las relaciones de inclusión representan funcionalidades obligatorias que forman parte del flujo principal de otro caso de uso.

| Caso de Uso           | Incluye                           |
| --------------------- | --------------------------------- |
| Registrar Usuario     | Enviar Datos del Usuario          |
| Enviar Mensaje        | Responder Mensaje                 |
| Consultar Historial   | Iniciar Sesión                    |
| Machine Learning / IA | Ejecutar ETL                      |
| Machine Learning / IA | Visualización de Datos e Insights |

### Relaciones «extend»

Las relaciones de extensión representan funcionalidades opcionales o complementarias que enriquecen el comportamiento de un caso de uso principal.

| Caso de Uso Base  | Extensión                    |
| ----------------- | ---------------------------- |
| Iniciar Sesión    | Autenticación y Autorización |
| Enviar Mensaje    | Machine Learning / IA        |
| Responder Mensaje | Machine Learning / IA        |

---

# 1.5 Consideraciones Arquitectónicas

El diagrama evidencia una arquitectura funcional basada en la separación de responsabilidades entre los procesos de interacción, autenticación, administración del conocimiento y procesamiento inteligente de la información. El componente de **Machine Learning/IA** actúa como el núcleo del sistema, integrando las consultas del usuario con una base de conocimiento enriquecida mediante procesos ETL administrados desde el sistema.

Esta organización favorece la escalabilidad, el mantenimiento y la evolución del sistema, al desacoplar la gestión documental, el procesamiento de datos y la generación de respuestas. Asimismo, la incorporación de mecanismos de autenticación y autorización garantiza la seguridad en el acceso a funcionalidades sensibles, mientras que la visualización de indicadores proporciona soporte para el monitoreo y la mejora continua del desempeño del chatbot.
