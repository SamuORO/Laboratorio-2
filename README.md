# Laboratorio #2: Implementación del Login en Laravel

<p align="center">
  <img src="https://img.shields.io/badge/PHP-8.3.28-777BB4?logo=php&logoColor=white" alt="PHP">
  <img src="https://img.shields.io/badge/Laravel-13.37.0-FF2D20?logo=laravel&logoColor=white" alt="Laravel">
  <img src="https://img.shields.io/badge/MySQL-Database-4479A1?logo=mysql&logoColor=white" alt="MySQL">
  <img src="https://img.shields.io/badge/Bootstrap-Frontend-7952B3?logo=bootstrap&logoColor=white" alt="Bootstrap">
</p>

## 1. Introducción

Laravel es un framework de PHP que permite desarrollar aplicaciones web mediante una estructura organizada, facilitando la separación de responsabilidades y el mantenimiento del código. En este laboratorio se trabajó con el patrón Modelo-Vista-Controlador (MVC), utilizando las herramientas que ofrece Laravel para crear una aplicación web y configurar un sistema de autenticación.

El proyecto permitió conocer la estructura inicial de Laravel, configurar una base de datos MySQL, ejecutar migraciones y generar las vistas y rutas necesarias para el registro e inicio de sesión de usuarios. También se realizaron ajustes para adaptar los controladores de autenticación a la versión utilizada del framework.

El objetivo principal fue comprender cómo se relacionan las rutas, los controladores, las vistas y los modelos dentro de una aplicación Laravel, así como documentar el proceso de instalación, configuración y solución de los inconvenientes encontrados durante la práctica.

## 2. Objetivos

- Comprender la estructura de un proyecto Laravel y su relación con el patrón MVC.
- Instalar y configurar Laravel en un entorno de desarrollo local.
- Conectar la aplicación con una base de datos MySQL.
- Ejecutar migraciones para crear las tablas necesarias.
- Implementar las funcionalidades de registro e inicio de sesión mediante Laravel UI y Bootstrap.
- Identificar y resolver errores de configuración, migraciones y compatibilidad.
- Documentar los resultados obtenidos durante el laboratorio.

## 3. Requisitos previos

Para realizar el laboratorio se utilizaron las siguientes herramientas y tecnologías:

| Tecnología | Versión o configuración |
|---|---|
| Sistema operativo | Windows 11 |
| PHP | 8.3.28 |
| Composer | 2.10.3 |
| Laravel Installer | 5.32.0 |
| Laravel Framework | 13.37.0 |
| Laravel UI | 4.6.3 |
| Servidor local | WampServer (WAMP) |
| Base de datos | MySQL |
| Node.js y npm | Instalados en el equipo |
| Editor de código | Bloc de notas y terminal PowerShell |
| Navegador | Google Chrome |

### 3.1. Verificación de las herramientas

Antes de crear el proyecto se comprobaron las versiones de las herramientas mediante los siguientes comandos:

```powershell
php -v
composer -v
laravel -v
node -v
npm -v
```

Estas herramientas permiten ejecutar el código PHP, administrar las dependencias del proyecto, crear aplicaciones Laravel y compilar los recursos del frontend.

<img width="590" height="131" alt="Captura de pantalla 2026-10-22 172421" src="https://github.com/user-attachments/assets/5f6dcc52-0f9c-47cc-b30e-75d9ae7c8d8e" />

## 4. Instalación y creación del proyecto

### 4.1. Instalación de Laravel Installer

Se utilizó Composer para instalar el instalador de Laravel de forma global:

```powershell
composer global require laravel/installer
```
<img width="633" height="212" alt="Captura de pantalla 2026-10-22 172459" src="https://github.com/user-attachments/assets/851bb22d-69a5-4efd-b800-a459ec17a22c" />

Este comando permite utilizar la herramienta `laravel` desde la terminal para crear nuevos proyectos.

### 4.2. Creación del proyecto

Se accedió al directorio de trabajo de WAMP:

```powershell
cd C:\wamp64\www
```

Luego se creó el proyecto con el nombre `LaravelLab`:

```powershell
laravel new LaravelLab
```
<img width="588" height="196" alt="Captura de pantalla 2026-10-22 172715" src="https://github.com/user-attachments/assets/95bab258-00c6-4b8a-9c5b-7a6542d929c5" />

Durante el proceso de instalación se seleccionaron las siguientes opciones:

- Starter kit: No.
- Frontend stack: Blade.
- Configuración adicional: se continuó con las opciones del instalador hasta completar la creación del proyecto.
<img width="600" height="233" alt="Captura de pantalla 2026-10-22 172829" src="https://github.com/user-attachments/assets/d751f09f-951f-424e-8b26-0ee840ea8c63" />
<img width="1042" height="398" alt="Captura de pantalla 2026-10-22 173236" src="https://github.com/user-attachments/assets/6a373ea1-6625-45bd-8624-595540c6e774" />

Después se ingresó a la carpeta del proyecto:

```powershell
cd C:\wamp64\www\LaravelLab
```

Se verificó la instalación con:

```powershell
php artisan --version
```

El resultado confirmó que el proyecto utilizaba Laravel Framework 13.37.0.
<img width="1037" height="318" alt="Captura de pantalla 2026-10-22 173651" src="https://github.com/user-attachments/assets/e0cabefc-09dc-4295-a930-2cd826a723eb" />


### 4.3. Primera ejecución de la aplicación

Para comprobar que Laravel funcionaba correctamente, se inició el servidor local:

```powershell
php artisan serve
```
<img width="1028" height="122" alt="Captura de pantalla 2026-10-22 173754" src="https://github.com/user-attachments/assets/07d8c405-bc21-4cff-8c9f-329323aa3535" />

Posteriormente, se abrió la dirección local en el navegador:

`http://localhost:8000`

Se verificó que apareciera la página inicial de Laravel.

En las siguientes etapas también se utilizó el comando de desarrollo:

```powershell
composer run dev
```
<img width="1082" height="692" alt="Captura de pantalla 2026-10-22 182929" src="https://github.com/user-attachments/assets/8cf96d99-5b3c-4430-b936-e437ecca527a" />

Este comando inicia los servicios de desarrollo definidos en el proyecto.

<img width="1905" height="955" alt="Captura de pantalla 2026-10-22 182938" src="https://github.com/user-attachments/assets/0ed27a01-71b5-441e-a283-fbbd358d9b0e" />


## 5. Arquitectura Modelo-Vista-Controlador (MVC)

Laravel organiza los componentes de la aplicación mediante una estructura que facilita la separación de responsabilidades.

### 5.1. Modelo

Los modelos representan los datos y permiten interactuar con la base de datos mediante Eloquent ORM.

En este proyecto destaca:

- `app/Models/User.php`: representa a los usuarios de la aplicación y permite trabajar con sus datos.

### 5.2. Vista

Las vistas contienen la interfaz que se presenta al usuario. Laravel utiliza el motor de plantillas Blade para generar páginas HTML.

Entre las ubicaciones relevantes se encuentran:

- `resources/views/`: contiene las plantillas de la aplicación.
- `resources/views/auth/`: contiene las vistas de autenticación generadas por Laravel UI.
- `resources/views/home.blade.php`: corresponde a la vista de inicio generada por el scaffolding, si se encuentra presente en el proyecto.

Las vistas de autenticación permiten mostrar formularios de registro, inicio de sesión y recuperación de contraseña.

### 5.3. Controlador

Los controladores reciben las solicitudes y coordinan las acciones que debe realizar la aplicación.

En el laboratorio se trabajó con los siguientes archivos:

- `app/Http/Controllers/Auth/LoginController.php`: gestiona las acciones de inicio y cierre de sesión.
- `app/Http/Controllers/Auth/RegisterController.php`: gestiona el registro de usuarios.
- `app/Http/Controllers/HomeController.php`: controla el acceso a la página de inicio autenticada.

### 5.4. Rutas

El archivo `routes/web.php` contiene las rutas que permiten acceder a las diferentes páginas de la aplicación.

Entre las rutas generadas para el laboratorio se encuentran:

| Ruta | Método | Función |
|---|---|---|
| `/` | GET | Página principal |
| `/login` | GET | Mostrar el formulario de inicio de sesión |
| `/login` | POST | Procesar el inicio de sesión |
| `/register` | GET | Mostrar el formulario de registro |
| `/register` | POST | Procesar el registro |
| `/logout` | POST | Cerrar la sesión |
| `/home` | GET | Página de inicio para usuarios autenticados |

Las rutas de autenticación permiten controlar el acceso a las funcionalidades y relacionan las solicitudes con sus respectivos controladores.

<img width="386" height="97" alt="Captura de pantalla 2026-10-22 180036" src="https://github.com/user-attachments/assets/87cefd2e-e372-4cb1-b69e-7f379024e7b4" />


## 6. Configuración de la base de datos MySQL

### 6.1. Creación de la base de datos

Se utilizó WAMP para ejecutar el servidor de base de datos y phpMyAdmin para administrar las bases de datos desde el navegador.

En phpMyAdmin se creó la base de datos con el siguiente nombre:

`laravellab`

Se utilizó una configuración de cotejamiento compatible con UTF-8, como `utf8mb4_unicode_ci`.

<img width="575" height="665" alt="Captura de pantalla 2026-10-22 175546" src="https://github.com/user-attachments/assets/bf0ed275-7d14-4201-9f50-ac05968c074c" />
<img width="617" height="292" alt="Captura de pantalla 2026-10-22 175740" src="https://github.com/user-attachments/assets/eb1fdd12-5fb9-4852-aee3-b7fea2184adb" />


### 6.2. Configuración del archivo `.env`

El archivo `.env` contiene las variables de entorno utilizadas por Laravel para configurar la conexión con la base de datos y otros servicios.

Se modificó la configuración de SQLite a MySQL. Los valores utilizados fueron:

```dotenv
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravellab
DB_USERNAME=root
DB_PASSWORD=
```
<img width="455" height="300" alt="Captura de pantalla 2026-10-22 175916" src="https://github.com/user-attachments/assets/72f94827-9933-4e50-b7b1-7cc3adf84320" />

La contraseña se dejó vacía porque el usuario `root` del entorno local no tenía contraseña configurada. Estos valores dependen de la configuración específica de WAMP.

Después de modificar el archivo, se limpió la configuración almacenada en caché:

```powershell
php artisan config:clear
```

Este paso permite que Laravel vuelva a leer las variables actualizadas del archivo `.env`.
<img width="386" height="97" alt="Captura de pantalla 2026-10-22 180036" src="https://github.com/user-attachments/assets/4d5e2fea-ebed-4d09-8156-7ed0cbf6e56a" />


### 6.3. Ejecución de las migraciones

Las migraciones permiten definir y crear la estructura de las tablas de la base de datos mediante archivos PHP.

Para ejecutar las migraciones se utilizó:

```powershell
php artisan migrate
```

Durante la práctica se crearon las tablas iniciales del proyecto:

- `users`: almacena la información de los usuarios.
- `cache`: permite gestionar los datos almacenados en caché.
- `jobs`: contiene información relacionada con los trabajos en cola.
- `failed_jobs`: registra trabajos en cola que no se completaron correctamente.
- `migrations`: registra las migraciones ejecutadas.

Para verificar su estado se utilizó:

```powershell
php artisan migrate:status
```

Las migraciones completadas aparecieron con el estado `Ran`.

<img width="1015" height="385" alt="Captura de pantalla 2026-10-22 182022" src="https://github.com/user-attachments/assets/e6b05993-5af5-4fc4-8804-709da5fe4b0d" />


<img width="782" height="405" alt="image" src="https://github.com/user-attachments/assets/4c91fc9b-2a0f-4620-9a5c-0fc0f1748cdb" />


### 6.4. Respaldo de la base de datos

Como parte de la documentación del laboratorio, se debe generar un respaldo de la base de datos.

El respaldo puede obtenerse desde phpMyAdmin siguiendo estos pasos:

1. Seleccionar la base de datos `laravellab`.
2. Abrir la opción **Exportar**.
3. Seleccionar el formato SQL.
4. Descargar el archivo generado.
5. Guardar una copia en el repositorio, por ejemplo, en `database/backup/laravellab.sql`.

<img width="1597" height="488" alt="image" src="https://github.com/user-attachments/assets/75c1c183-c681-4e8c-90c5-48a48e02df7a" />


**Nota:** se debe agregar al repositorio el archivo SQL realmente exportado. El respaldo no se considera realizado hasta que el archivo haya sido generado y guardado.

## 7. Implementación del sistema de autenticación

### 7.1. Instalación de Laravel UI

Para generar las vistas y los controladores de autenticación se utilizó el paquete Laravel UI, que proporciona scaffolding basado en Bootstrap.

Se instaló mediante Composer:

```powershell
composer require laravel/ui
```

La versión instalada fue `v4.6.3`.

Posteriormente, se generó la estructura de Bootstrap y autenticación:

```powershell
php artisan ui bootstrap --auth
```

Este comando generó la estructura básica para el registro, el inicio de sesión, el cierre de sesión y la recuperación de contraseñas.

<img width="606" height="252" alt="Captura de pantalla 2026-10-22 183804" src="https://github.com/user-attachments/assets/2a0f1045-c8f6-4aa3-aa2e-062ea944ad6c" />


<img width="811" height="267" alt="Captura de pantalla 2026-10-22 185300" src="https://github.com/user-attachments/assets/9b4d2f87-86f2-4610-a233-1a9086ba1184" />


### 7.2. Instalación de dependencias del frontend

Para instalar las dependencias de JavaScript y CSS se utilizó npm:

```powershell
npm.cmd install
```
<img width="1252" height="493" alt="image" src="https://github.com/user-attachments/assets/c5844533-63ee-4735-b5d2-874db27cd131" />

Luego se compilaron los recursos del frontend:

```powershell
npm.cmd run dev
```
<img width="956" height="457" alt="image" src="https://github.com/user-attachments/assets/a20f8180-6762-4d4e-a254-cde19864e5f9" />

En este entorno, PowerShell bloqueaba la ejecución del archivo `npm.ps1` debido a la política de ejecución de scripts. Se utilizó `npm.cmd` como alternativa para ejecutar npm sin modificar dicha política.

### 7.3. Verificación de las rutas de autenticación

Se comprobó que Laravel registrara las rutas generadas mediante:

```powershell
php artisan route:list
```

El resultado mostró las rutas de inicio de sesión, registro, cierre de sesión, recuperación de contraseña y acceso a la página de inicio.

<img width="1240" height="423" alt="Captura de pantalla 2026-10-22 190602" src="https://github.com/user-attachments/assets/18f18dee-f559-48e0-8e25-b97b603ed4a7" />

### 7.4. Adaptación de los controladores a Laravel 13

Durante las pruebas se identificó que los controladores generados utilizaban la llamada tradicional `$this->middleware()`, que producía el error `Call to undefined method ...::middleware()` en este entorno.

Para resolverlo, se adaptaron los controladores de autenticación y de inicio a la interfaz `HasMiddleware` y al método estático `middleware()`, utilizando la clase `Illuminate\Routing\Controllers\Middleware`.

Los archivos modificados fueron:

- `app/Http/Controllers/Auth/LoginController.php`
- `app/Http/Controllers/Auth/RegisterController.php`
- `app/Http/Controllers/HomeController.php`

En cada controlador se conservaron las acciones correspondientes y se ajustó la declaración del middleware para permitir el acceso según el estado de autenticación del usuario.

Este cambio permitió que las rutas de inicio de sesión, registro y página de inicio funcionaran con la estructura de Laravel 13 utilizada en el laboratorio.

<img width="793" height="70" alt="image" src="https://github.com/user-attachments/assets/94067c4d-9e17-489f-b2f9-05b76d223997" />


## 8. Pruebas y resultados obtenidos

### 8.1. Página principal

Se comprobó el acceso a la aplicación mediante:

`http://localhost:8000/`

La página inicial permitió verificar que el servidor de Laravel se encontraba funcionando.

<img width="1093" height="715" alt="image" src="https://github.com/user-attachments/assets/e58068a4-5c79-4f50-a00e-4239a5eaca32" />


### 8.2. Registro de usuarios

Se accedió al formulario de registro mediante:

`http://localhost:8000/register`

Se completaron los campos solicitados y se registró un usuario de prueba. El proceso permitió comprobar que el sistema podía recibir los datos y almacenar la información del usuario en la base de datos.

<img width="1807" height="672" alt="Captura de pantalla 2026-10-22 193325" src="https://github.com/user-attachments/assets/7a3dd82d-2023-45c5-97c9-352f4256ec33" />


<img width="1110" height="432" alt="Captura de pantalla 2026-10-22 193740" src="https://github.com/user-attachments/assets/dbe6545d-f88c-4e2d-a58b-33bd91097eb1" />
<img width="1092" height="195" alt="image" src="https://github.com/user-attachments/assets/6191f530-a1a3-45ae-9099-7ce39ccd0410" />



### 8.3. Inicio de sesión

Se accedió al formulario mediante:

`http://localhost:8000/login`

Se utilizaron las credenciales del usuario registrado durante la prueba. El funcionamiento correcto permitió comprobar que Laravel podía validar las credenciales y gestionar la sesión del usuario.

<img width="1871" height="588" alt="Captura de pantalla 2026-10-22 192002" src="https://github.com/user-attachments/assets/a7345864-7455-4c55-a7cb-368fd2076f1c" />


### 8.4. Página de inicio autenticada

Finalmente, se verificó la ruta:

`http://localhost:8000/home`

Esta página permitió comprobar el acceso a la sección protegida para usuarios autenticados.

<img width="1916" height="352" alt="Captura de pantalla 2026-10-22 194231" src="https://github.com/user-attachments/assets/203f45ea-c86a-40ce-bea4-23a143e9d14c" />


## 9. Dificultades encontradas y soluciones aplicadas

### 9.1. Configuración incorrecta de la base de datos

**Dificultad:** Laravel intentaba conectarse a una base de datos llamada `laravel`, aunque la base de datos creada en phpMyAdmin tenía el nombre `laravellab`.

**Solución:** se revisó el archivo `.env`, se habilitaron las variables de conexión que estaban comentadas y se configuró el nombre correcto de la base de datos. Después se ejecutó `php artisan config:clear`.
<img width="247" height="151" alt="image" src="https://github.com/user-attachments/assets/bffc3956-4053-4ff4-a01a-db714a6a763a" />


### 9.2. Longitud máxima de los índices en MySQL

**Dificultad:** durante las migraciones aparecía el error `1071`, relacionado con la longitud máxima permitida para los índices.

**Solución:** se configuró una longitud predeterminada de 191 caracteres para las cadenas mediante `Schema::defaultStringLength(191)` en `AppServiceProvider.php`. También se redujo la longitud de las columnas `connection` y `queue` a 100 caracteres en la migración de `jobs` para resolver el problema del índice compuesto de `failed_jobs`.

### 9.3. Tabla existente durante las migraciones

**Dificultad:** después de una migración fallida, Laravel intentaba crear nuevamente la tabla `users`, que ya existía.

**Solución:** como la base de datos de práctica no contenía información que se necesitara conservar, se eliminaron las tablas de `laravellab` desde phpMyAdmin y se ejecutaron las migraciones nuevamente desde cero.

### 9.4. Bloqueo de npm en PowerShell

**Dificultad:** al ejecutar `npm install`, PowerShell mostraba un error de seguridad porque la ejecución de scripts estaba deshabilitada.

**Solución:** se utilizó `npm.cmd install` y posteriormente `npm.cmd run dev`, evitando tener que cambiar la política de ejecución de PowerShell.

### 9.5. Error de middleware en los controladores

**Dificultad:** al acceder a `/login`, `/register` y `/home` aparecía un error relacionado con la llamada al método `middleware()`.

**Solución:** se adaptaron los controladores generados por Laravel UI a la interfaz `HasMiddleware` y al método estático `middleware()` disponible en Laravel 13. Después de realizar los ajustes, se verificó nuevamente el acceso a las páginas.
<img width="886" height="546" alt="image" src="https://github.com/user-attachments/assets/3c59077c-4eb5-4ae0-9d8a-3e3b55800a33" />


### 9.6. Estilos y recursos del frontend

**Dificultad:** la apariencia inicial de algunas páginas no se mostraba correctamente durante las primeras pruebas.

**Solución:** se instalaron las dependencias del frontend con npm y se ejecutó el proceso de desarrollo para compilar los recursos de Bootstrap y Vite.

## 10. Conclusiones

El laboratorio permitió comprender la estructura básica de una aplicación desarrollada con Laravel y la importancia de organizar el código mediante el patrón Modelo-Vista-Controlador. Se comprobó la función de las rutas, los controladores, las vistas y los modelos durante la implementación de un sistema de autenticación.

Además, se practicó la configuración de una base de datos MySQL mediante el archivo `.env`, la creación de tablas con migraciones y el uso de comandos de Artisan para comprobar el estado de la aplicación. La instalación de Laravel UI permitió generar la estructura inicial de registro e inicio de sesión, mientras que los ajustes realizados en los controladores facilitaron su funcionamiento con Laravel 13.

Finalmente, la resolución de los errores de base de datos, la ejecución de npm y la compatibilidad de los controladores reforzó la importancia de revisar los mensajes de error y adaptar las configuraciones al entorno de desarrollo utilizado.

## 11. Referencias

1. Laravel. (s. f.). *Documentación oficial de Laravel 13: Instalación y configuración*.  
   https://laravel.com/docs/13.x/installation

2. Laravel. (s. f.). *Documentación oficial de Laravel 13: Bases de datos y migraciones*.  
   https://laravel.com/docs/13.x/migrations

3. Laravel. (s. f.). *Documentación oficial de Laravel 13: Enrutamiento*.  
   https://laravel.com/docs/13.x/routing

4. Laravel UI. (s. f.). *Repositorio y documentación oficial de Laravel UI*.  
   https://github.com/laravel/ui

5. Node.js. (s. f.). *Documentación oficial de npm*.  
   https://docs.npmjs.com/

## 12. Fecha de ejecución del laboratorio

**Fecha de ejecución:** 22 de Octubre de 2026

## 13. Datos del estudiante

Este laboratorio ha sido desarrollado por el estudiante de la Universidad Tecnológica de Panamá.

- **Nombre:** Samuel Orocú
- **Correo:** samuel.orocu@utp.ac.pa
- **Curso:** Desarrollo Web
- **Facultad:** Facultad de Ingeniería de Sistemas Computacionales
- **Campus:** Víctor Levi Sasso
- **Instructor del laboratorio:** Ing. Irina Fong
- **Laboratorio:** Laboratorio #2 – Implementación del Login en Laravel

---

<p align="center">
  Universidad Tecnológica de Panamá  
  Facultad de Ingeniería de Sistemas Computacionales  
  Desarrollo Web — II Semestre 2026
</p>


