# Guía de Instalación y Primera Ejecución del Sistema Smart de Chatbot

Esta guía detalla los pasos necesarios para la instalación, configuración y primera ejecución de los componentes del Sistema Smart de Chatbot. Incluye requisitos de hardware y software, así como procedimientos para la ambientación del entorno de desarrollo y despliegue.

## 1. Requisitos del Sistema

### 1.1 Hardware Recomendado
Para un óptimo rendimiento y funcionalidad del sistema, se recomienda el siguiente hardware, probado en entornos Windows 10 y Linux:

*   **Memoria RAM**: 8 GB
*   **Espacio en Disco Duro**: 12 GB
*   **Procesador**: Intel Core i7 o equivalente

### 1.2 Software Requerido
El entorno de desarrollo y despliegue del chatbot requiere el siguiente software:

*   **Sistema Operativo**: Windows 10 o superior, o Linux Ubuntu
*   **Base de Datos**: MySQL 8.0, MongoDB Atlas
*   **Herramientas de Desarrollo**:
    *   Spring Tool Suite 4 (Eclipse)
    *   MySQL Workbench
    *   Apache Maven 6.6.3
    *   Java 11 o superior
*   **Contenedorización**: Docker
*   **Servidor de Lenguaje Extendido**: Ollama
*   **Monitoreo de GPU (Opcional)**: nvtop
*   **Servidor Web (para Frontend)**: Apache HTTP Server
*   **Cliente SSH**: Para acceso remoto a servidores.
*   **Control de Versiones**: Git
*   **Plataformas de Mensajería**: Telegram (para bot)
*   **Gestor de Contenido (Opcional)**: WordPress (para integración con plugin)

## 2. Ambientación del Entorno de Desarrollo

### 2.1 Configuraciones del Ambiente (Desarrollo Java)
Para la creación, desarrollo y ejecución de proyectos Java, es necesario instalar las siguientes herramientas:

#### Spring Tool Suite 4 (Eclipse)
Entorno de desarrollo integrado (IDE) completo para la creación de microservicios Spring Boot.
**Enlace de Descarga**: [https://spring.io/tools](https://spring.io/tools)
Descargue la versión 4.

#### Quitar Validadores Eclipse
Para optimizar el rendimiento del IDE, se recomienda deshabilitar validadores innecesarios en Eclipse. Acceda a `Window > Preferences > Validation` y deshabilite los validadores no requeridos para su proyecto.

#### Maven Windows Configuración
1.  **Descargar Maven**: Descargue la versión binaria de Apache Maven desde la página oficial: [https://maven.apache.org/download.cgi?.](https://maven.apache.org/download.cgi?.)
2.  **Descomprimir**: Extraiga el archivo ZIP en una ubicación de su preferencia, por ejemplo, `C:\Java\apache-maven-3.6.3`.
3.  **Variables de Entorno**: Configure las siguientes variables de entorno del sistema:
    *   `M2_HOME`: `C:\Java\apache-maven-3.6.3` (Ruta donde descomprimió Maven)
    *   `M2`: `%M2_HOME%\bin`
    *   `JAVA_HOME`: `C:\Java\jdk17.0.11` (Ruta de su instalación de Java Development Kit)
    *   `Path`: Agregue `%JAVA_HOME%\bin;%M2%;` al inicio de la variable `Path` existente.

    *Captura de pantalla de configuración de variables de entorno de Maven y Java* (Referencia: Imagen en el documento original)

#### Maven Dependencias
Configure el repositorio local de Maven donde se descargarán las librerías. Esto se realiza editando el archivo `settings.xml` de Maven (usualmente en `%M2_HOME%/conf/settings.xml`) para apuntar a un repositorio local o remoto si fuera necesario.

*Capturas de pantalla de configuración de dependencias de Maven* (Referencia: Imágenes en el documento original)

### 2.2 Cargar Proyectos desde GitHub
Para obtener el código fuente de los microservicios, clone los siguientes repositorios de GitHub. Acceda a la consola o terminal y ejecute el comando `git clone` para cada proyecto:

*   **Módulo de Seguridad**: `https://github.com/dijavaji/tec-framework-security.git`
*   **API del Chatbot**: `https://github.com/dijavaji/tec-chatbot-ws.git`
*   **API de Mensajes**: `https://github.com/dijavaji/tec-wa-message-ws.git`
*   **Aplicación de Chat (Frontend)**: `https://github.com/dijavaji/tec-chat-app.git`
*   **API de Exploración de Datos**: `https://github.com/dijavaji/tec-document-loader-ws.git`

Posteriormente, importe cada proyecto al IDE STS para su utilización. Utilice la opción de importar proyectos Maven existentes.

*Capturas de pantalla de clonación e importación de proyectos en STS* (Referencia: Imágenes en el documento original)

### 2.3 Compilar y Ejecutar Proyectos (Entorno Local)

Acceda a la ruta de cada proyecto en la consola y ejecute los siguientes comandos Maven:

1.  **Compilar y Generar el Proyecto (saltando tests)**:
    ```bash
    mvn clean install -Dmaven.test.skip=true
    ```
    *Captura de pantalla de la ejecución de mvn clean install* (Referencia: Imagen en el documento original)

2.  **Ejecutar la Aplicación en Local con Perfil `local`**:
    ```bash
    mvn spring-boot:run -Dspring-boot.run.profiles=local
    ```
    *Captura de pantalla de la ejecución de spring-boot:run* (Referencia: Imagen en el documento original)

Si la ejecución se realiza sin errores, podrá acceder a la documentación de la API Rest a través de Swagger UI:

*   **Swagger UI**: [http://localhost:8081/swagger-ui/index.html](http://localhost:8081/swagger-ui/index.html)

*Captura de pantalla de la interfaz de Swagger UI* (Referencia: Imagen en el documento original)

## 3. Configuración y Despliegue en Servidor

### 3.1 Configuración del Servidor de Pruebas CHATBOT (GCP)

El servidor de pruebas se encuentra configurado en Google Cloud Platform (GCP).

*   **Consola GCP**: [https://console.cloud.google.com/](https://console.cloud.google.com/)
*   **Aplicación (Frontend)**: [http://35.209.77.154/](http://35.209.77.154/) (IP de ejemplo, verificar la actual)
*   **Instancias VM (Compute Engine)**: `chat-bot-prx`, `microservicios-chatbot`
*   **Credenciales**: Usuario `admin@pbx.com`, Clave (solicitar al administrador)

Se requiere un navegador web y un cliente SSH para acceder a la consola de GCP y a las instancias VM.

*Capturas de pantalla de la consola GCP y las instancias VM* (Referencia: Imágenes en el documento original)

### 3.2 Procedimiento de Instalación del Frontend en Servidor Web Apache

Para desplegar la aplicación frontend (Reactjs) en un servidor web Apache:

1.  **Compilar la Aplicación Reactjs**: Navegue al directorio del proyecto `tec-chat-app` y ejecute:
    ```bash
    npm run build
    ```
    Esto generará los archivos estáticos optimizados en el directorio `build/`.
    *Capturas de pantalla de npm run build* (Referencia: Imágenes en el documento original)

2.  **Copiar Archivos Compilados**: Copie el contenido del directorio `build/` al directorio de despliegue de Apache, por ejemplo, `/var/www/html/tec-app/`:
    ```bash
    sudo cp -r build/* /var/www/html/tec-app/
    ```
    *Capturas de pantalla de la copia de archivos* (Referencia: Imágenes en el documento original)

3.  **Configurar Apache**: Edite el archivo de configuración de Apache para el sitio por defecto. Acceda al directorio:
    ```bash
    cd /etc/apache2/sites-available/
    ```
    Visualice el contenido del archivo de configuración:
    ```bash
    cat 000-default.conf
    ```
    Edite el archivo para modificar el `DocumentRoot` y apuntar a su aplicación. Por ejemplo, si su carpeta se llama `tec-app`:
    ```apache
    DocumentRoot /var/www/html/tec-app
    ```
    Guarde los cambios y reinicie Apache.
    *Capturas de pantalla de la configuración de Apache* (Referencia: Imágenes en el documento original)

### 3.3 Instalación de Java en el Servidor

Para instalar Java 11 o superior en el servidor, se recomienda utilizar `sdkman` para una gestión más sencilla de versiones. Si no está instalado, primero instale `sdkman`:

1.  **Instalar SDKMAN (si no está instalado)**:
    ```bash
    curl -s "https://get.sdkman.io" | bash
    source "$HOME/.sdkman/bin/sdkman-init.sh"
    ```
    *Capturas de pantalla de la instalación de SDKMAN* (Referencia: Imágenes en el documento original)

2.  **Instalar Java**: Utilice `sdkman` para instalar Java 11 (o la versión deseada):
    ```bash
    sdk install java 11.0.11-tem
    ```
    *Capturas de pantalla de la instalación de Java con SDKMAN* (Referencia: Imágenes en el documento original)

### 3.4 Instalación del Servidor Ollama

Ollama es un servidor de lenguaje extendido esencial para el funcionamiento del chatbot. Para su instalación y configuración, siga la guía oficial para Linux:

**Guía de Instalación**: [https://github.com/ollama/ollama/blob/main/docs/linux.md](https://github.com/ollama/ollama/blob/main/docs/linux.md)

1.  **Instalar Ollama**: Ejecute el comando proporcionado en la guía de instalación (ejemplo para Linux):
    ```bash
    curl -fsSL https://ollama.com/install.sh | sh
    ```
    *Captura de pantalla de la instalación de Ollama* (Referencia: Imagen en el documento original)

2.  **Descargar Modelos**: Descargue el modelo de lenguaje que utilizará el chatbot (ejemplo: `qwen2:0.5b`):
    ```bash
    ollama run qwen2:0.5b
    ```
    Esto iniciará la descarga del modelo si no está presente.

3.  **Verificar Modelos Instalados**:
    ```bash
    ollama list
    ```
    *Captura de pantalla de los modelos Ollama listados* (Referencia: Imagen en el documento original)

4.  **Iniciar Ollama**: Asegúrese de que el servicio Ollama esté corriendo.

5.  **Probar Ollama**: Realice una prueba de conexión y generación de respuesta:
    ```bash
    curl -X POST http://127.0.0.1:11434/api/generate -d '{ "model": "llama3", "prompt":"Por que el cielo es azul?", "stream": true}'
    ```

### 3.5 Instalación de nvtop (Opcional)

nvtop es un monitor de tareas de Linux que permite visualizar el uso de GPU de NVIDIA, AMD e Intel. Es útil para monitorear el rendimiento de los modelos de IA.

1.  **Actualizar Repositorios e Instalar nvtop**:
    ```bash
    sudo apt update
    sudo apt install nvtop
    ```

2.  **Ejecutar nvtop**: Una vez instalado, inicie la herramienta con:
    ```bash
    nvtop
    ```
    *Captura de pantalla de la interfaz de nvtop* (Referencia: Imagen en el documento original)

### 3.6 Procedimiento de Actualización de Versiones de Microservicios Docker al Servidor

Para actualizar las versiones de los microservicios docker en el servidor, siga estos pasos:

1.  **Pull de Nuevas Imágenes**: Obtenga las últimas imágenes de Docker para cada microservicio desde su registro de contenedores (ej. Docker Hub o Google Container Registry):
    ```bash
    docker pull technoloqie/tec-fwk-security-api:latest
    docker pull technoloqie/tec-chatbot-api:latest
    # ... para todos los microservicios
    ```
    *Capturas de pantalla de la actualización de imágenes Docker* (Referencia: Imágenes en el documento original)

2.  **Detener y Eliminar Contenedores Antiguos**: Detenga y elimine las instancias en ejecución de los microservicios antiguos:
    ```bash
    docker stop tec-fwk-security-api tec-chatbot-api # ...
    docker rm tec-fwk-security-api tec-chatbot-api # ...
    ```

3.  **Lanzar Nuevos Contenedores**: Inicie los nuevos contenedores con las imágenes actualizadas, asegurándose de configurar las variables de entorno y mapeos de puertos correctamente (usando `docker run` o `docker-compose up`).

### 3.7 Instalación de MySQL en Contenedor Docker

Para instalar MySQL 8.0 utilizando Docker:

1.  **Pull de la Imagen de MySQL**: Obtenga la imagen oficial de MySQL:
    ```bash
    docker pull mysql:8.0
    ```
    *Captura de pantalla del pull de la imagen MySQL* (Referencia: Imagen en el documento original)

2.  **Ejecutar Contenedor MySQL**: Inicie un contenedor MySQL, configurando la contraseña del usuario root y mapeando el puerto:
    ```bash
    docker run --name mysql-chatbot -e MYSQL_ROOT_PASSWORD=your_secure_password -p 3306:3306 -d mysql:8.0
    ```
    *Captura de pantalla de la ejecución del contenedor MySQL* (Referencia: Imagen en el documento original)

3.  **Acceder a MySQL (opcional)**:
    ```bash
    mysql -h 127.0.0.1 -u root -p
    ```
    Ingrese la contraseña configurada.
    *Captura de pantalla del acceso a MySQL* (Referencia: Imagen en el documento original)

### 3.8 Crear una Base de Datos en MongoDB Atlas

MongoDB Atlas es una base de datos en la nube (DBaaS) que se utilizará para almacenar datos del chatbot. Siga estos pasos para configurar una base de datos gratuita (M0 Sandbox):

1.  **Registrar una cuenta**: Vaya a [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) y regístrese con su dirección de correo electrónico.
    *Captura de pantalla de registro en MongoDB Atlas* (Referencia: Imagen en el documento original)

2.  **Crear un Nuevo Cluster**: Después de iniciar sesión:
    *   Llene los campos `Nombre de la organización` y `Nombre del proyecto`.
    *   Seleccione el lenguaje de programación preferido (ej. Java).
    *   Haga clic en `Crear un Cluster` debajo de `Shared Clusters` (la opción `M0 Sandbox` es gratuita).
    *   Deje la opción por defecto en `Cloud Provider & Region` (normalmente AWS).
    *   Deje la opción por defecto en `Cluster Tier` (`M0 Sandbox - 512 MB Storage`).
    *   Asigne un `Nombre del Cluster` o deje el valor por defecto (`Cluster0`).
    *   Haga clic en `Create Cluster`.
    Espere a que el cluster se aprovisione (1-3 minutos).
    *Capturas de pantalla del proceso de creación del cluster* (Referencia: Imágenes en el documento original)

3.  **Crear un Usuario de Base de Datos**:
    *   Especifique un `Nombre de usuario` y una `Contraseña` (o use la sugerida por Atlas).
    *   Haga clic en `Create Database User`.
    *Capturas de pantalla de la creación del usuario de base de datos* (Referencia: Imágenes en el documento original)

4.  **Configurar Lista de Acceso IP**:
    *   Agregue su dirección IP actual a la lista de acceso (`Add My Current IP Address`).
    *   Haga clic en `Finish and Close`.
    *   Finalmente, haga clic en `Go to Overview`.
    *Capturas de pantalla de la configuración de IP y finalización* (Referencia: Imágenes en el documento original)

### 3.9 Instalar Bot para Telegram

Para integrar el chatbot con Telegram, deberá crear un bot a través de BotFather y configurar los tokens necesarios.

1.  **Crear un Nuevo Bot con BotFather**: En Telegram, busque `@BotFather` y envíe el comando `/newbot`. Siga las instrucciones para nombrar su bot y obtener el `HTTP API Token`.
    *Captura de pantalla de la interacción con BotFather* (Referencia: Imagen en el documento original)

2.  **Configurar el Microservicio del Bot**: Actualice el microservicio de mensajes (`tec-messages-api`) con el token de su bot de Telegram y otras configuraciones específicas para la integración.

### 3.10 Instalar un Plugin de WordPress

Si desea integrar el chatbot como un widget en un sitio web de WordPress, puede instalar un plugin personalizado desde el panel de control de WordPress.

1.  **Acceder al Panel de Administración de WordPress**: Inicie sesión en su panel de administración de WordPress.
2.  **Ir a Plugins**: Navegue a `Plugins > Añadir nuevo`.
3.  **Subir Plugin**: Haga clic en `Subir Plugin` y seleccione el archivo `.zip` del plugin del chatbot que le fue proporcionado.
4.  **Instalar y Activar**: Haga clic en `Instalar ahora` y luego en `Activar Plugin`.

*Capturas de pantalla de la instalación del plugin de WordPress* (Referencia: Imagen en el documento original)
