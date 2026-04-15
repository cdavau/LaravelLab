# LaravelLab
Prerequisitos para este laboratorio:
PHP Versión 8.3.28, Composer última versión estable, Laravel Installer, WAMP Server, MySQL running, Visual Studio Code, SO: Windows.
Se requerió instalar Node.js para ejecutar comandos npm. Se configuró el archivo .env con las siguientes líneas: use Illuminate\Support\Facades\Schema; y Schema::defaultStringLength(191) en la función "boot".
Flujo de comandos utilizados:
Creación de la aplicación: laravel new pruebaLab.
Migraciones: php artisan migrate, php artisan migrate:status, php artisan migrate:fresh.
Caché de configuración: php config:clear, php config:cache, php artisan migrate (para ver el estado).
Composer run dev: composer run dev.
Laravel/UI: composer require laravel/ui, php artisan bootstrap, php artisan bootstrap --auth, npm install, npm run dev.





Este laboratorio ha sido desarrollado por el estudiante de la Universidad
Tecnológica de Panamá: 
Nombre: Carlos Abadia
Correo: carlos.abadia1@utp.ac.pa
Curso: Desarrollo de Software VII
Instructor del Laboratorio: Irina Fong.
