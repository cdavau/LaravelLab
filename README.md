# LaravelLab
# Laboratorio - Instalación de Laravel

**Universidad Tecnológica de Panamá**  
**Facultad de Ingeniería de Sistemas Computacionales**  
**Departamento de Programación de Computadoras**

| | |
|---|---|
| **Asignatura** | Desarrollo de Software VII |
| **Tema** | Instalación de Laravel |
| **Semestre** | I Semestre |
| **Grupo** | 1GS132 |
| **Estudiante** | Carlos Abadía - 4-823-2233 |
| **Correo** | carlos.abadia1@utp.ac.pa |
| **Facilitador** | Irina Fong |
| **Fecha** | 14/04/2026 |

---

## Introducción

El MVC o Modelo-Vista-Controlador es un patrón de arquitectura de software que,
utilizando 3 componentes, separa la lógica de la aplicación de la lógica de la vista.
En Laravel, esto se traduce en carpetas muy concretas dentro de los proyectos que se crean.

### El Modelo — `app/Models`
Hace referencia a la estructura de datos de la aplicación. Los datos pueden ser
transferidos desde la base de datos directamente a la vista o ser transformados en
el controlador para ser actualizados nuevamente al origen. En este laboratorio,
el modelo `User.php` fue el encargado de representar la tabla `users` en MySQL.

### El Controlador — `app/Http/Controllers`
Los controladores son el punto intermedio entre las rutas que lanza el usuario y
las vistas, donde además se aplica toda la lógica de programación. Cuando se hace
el registro en `/register`, fue un controlador el que procesó el formulario y le
indicó al modelo que guardara el usuario en la base de datos.

### La Vista — `resources/views`
La Vista es la representación de la información en una interfaz de usuario. En
Laravel estas vistas se escriben con archivos `.blade.php`, que es el motor de
plantillas del framework.

### Las Rutas — `routes/web.php`
Es posible definir las rutas en `routes/web.php` si son para la web y en
`routes/api.php` cuando son para el backend. Las rutas son la puerta de entrada:
definen qué URL responde a qué controlador. Sin ellas, Laravel no sabría a dónde
dirigir cada petición del usuario.

---
<img width="921" height="215" alt="image" src="https://github.com/user-attachments/assets/5d57630a-ff0e-4c5c-8def-c69a98812f6f" />

Dashboard de laravel luego de registrar un usuario.

<img width="921" height="287" alt="image" src="https://github.com/user-attachments/assets/bb42eb16-980b-4734-8370-ccd3a4802a97" />

En phpMyAdmin, el usuario creado en Laravel aparece en la tabla users.

## Entorno de Desarrollo del Laboratorio

Para el desarrollo de este laboratorio se utilizó **WAMP64** como entorno de
desarrollo local, el cual integra tres componentes esenciales: Windows como sistema
operativo, Apache como servidor web y MySQL como gestor de base de datos. Este
ecosistema permite simular un servidor web en la máquina local sin necesidad de un
hosting externo.

La base de datos utilizada se denominó **`pruebalab`**, creada previamente en
**phpMyAdmin**, que es la interfaz gráfica que provee WAMP para administrar MySQL.
Una vez creada la base de datos, Laravel se encargó de generar automáticamente las
tablas necesarias a través de su sistema de migraciones.

---

## Archivo `.env`

El archivo `.env` es el archivo de configuración de variables de entorno de Laravel.
Se encuentra en la raíz del proyecto y contiene información sensible y específica
del entorno donde corre la aplicación, como las credenciales de la base de datos,
el nombre de la aplicación y el modo de depuración.

Para este laboratorio, las variables más relevantes fueron las siguientes:

```env
APP_NAME=Laravel
APP_ENV=local
APP_DEBUG=true

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=pruebalab
DB_USERNAME=root
DB_PASSWORD=
```

---

## Migraciones

Las migraciones son archivos PHP ubicados en la carpeta `database/migrations/` que
describen la estructura de las tablas de la base de datos de forma controlada y
versionada. En lugar de crear tablas manualmente en phpMyAdmin, Laravel permite
definirlas mediante código, lo que facilita el trabajo en equipo y el control de cambios.

Cada archivo de migración contiene dos métodos principales:

- **`up()`** → Se ejecuta al correr la migración. Crea o modifica la tabla.
- **`down()`** → Se ejecuta al revertir la migración. Elimina o deshace los cambios.

Para el laboratorio, Laravel generó automáticamente las siguientes migraciones:

| Archivo de Migración | Tabla que crea |
|---|---|
| `0001_01_01_000000_create_users_table` | `users` |
| `0001_01_01_000001_create_cache_table` | `cache` |
| `0001_01_01_000002_create_jobs_table` | `jobs` |

---

## Comandos Utilizados

```bash
# Instalar Laravel y crear el proyecto
composer global require laravel/installer
laravel new pruebaLab

# Ejecutar migraciones
php artisan migrate

# Resetear y volver a migrar desde cero
php artisan migrate:fresh

# Limpiar y cachear configuración (después de editar .env)
php artisan config:clear
php artisan config:cache

# Instalar paquete de autenticación con Bootstrap
composer require laravel/ui
php artisan ui bootstrap --auth

# Instalar dependencias front-end y compilar
npm install
npm run dev

# Levantar el servidor de desarrollo
composer run dev
```

---

## Dificultades y Soluciones

### Error 1 — Longitud de cadena en MySQL

**Error:**
SQLSTATE[42000]: Syntax error or access violation: 1071
Specified key was too long; max key length is 1000 bytes

**Causa:** La versión de MySQL en WAMP tiene un límite de longitud para índices
incompatible con la longitud predeterminada de Laravel.

**Solución:** Modificar `app/Providers/AppServiceProvider.php`:

```php
use Illuminate\Support\Facades\Schema;

public function boot(): void
{
    Schema::defaultStringLength(191);
}
```

---

### Error 2 — npm no reconocido en PowerShell

**Error:**
npm : No se puede cargar el archivo C:\Program Files\nodejs\npm.ps1 porque
la ejecución de scripts está deshabilitada en este sistema.

**Causa:** Node.js no estaba instalado en el sistema.

**Solución:** Instalar Node.js desde https://nodejs.org y ejecutar los comandos
`npm install` y `npm run dev` desde el **cmd** en lugar de PowerShell.

---

## Resultado Final

Dashboard de Laravel luego de registrar un usuario exitosamente en
`http://127.0.0.1:8000/home`, confirmando que el flujo completo
Ruta → Controlador → Modelo → Vista funcionó correctamente.

El usuario registrado también es visible en phpMyAdmin dentro de la tabla
`users` de la base de datos `pruebalab`.

---

## Puntos de Referencia

- Material dado por la profesora — Guía del Laboratorio Login de Laravel
- https://codigofacilito.com/articulos/mvc-model-view-controller-explicado
- https://claude.ai/

---

Este laboratorio ha sido desarrollado por el estudiante de la Universidad Tecnológica de Panamá:

Nombre: Carlos Abadia

Correo: carlos.abadia1@utp.ac.pa

Curso: Desarrollo de Software VII

Instructor del Laboratorio: Irina Fong.
