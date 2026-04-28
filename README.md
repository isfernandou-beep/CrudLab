# CrudLab — CRUD de Productos en Laravel

Laboratorio académico que implementa un CRUD completo (Create, Read, Update, Delete) de productos utilizando Laravel 13, migraciones y el generador automático de CRUD `ibex/crud-generator`.

---

## Tecnologías utilizadas

| Tecnología | Versión |
|---|---|
| PHP | ^8.3 |
| Laravel Framework | ^13.0 |
| ibex/crud-generator | ^2.1 |
| laravel/ui | ^4.6 |
| Bootstrap | 5.x (CDN) |
| MySQL | WAMP |

---

## Requisitos previos

- WAMP instalado y corriendo (ícono verde en la barra de tareas)
- PHP 8.3 o superior
- Composer
- Laravel CLI

---

## Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/isfernandou-beep/CrudLab.git
cd CrudLab
```

### 2. Instalar dependencias

```bash
composer install
```

### 3. Crear el archivo de entorno

```bash
cp .env.example .env
php artisan key:generate
```

### 4. Crear la base de datos

Abrir phpMyAdmin desde el menú de WAMP y crear una base de datos llamada `crud_db`.

### 5. Configurar el archivo `.env`

```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=crud_db
DB_USERNAME=root
DB_PASSWORD=
```

### 6. Solución al error de longitud de clave (MySQL antiguo)

En `app/Providers/AppServiceProvider.php`, dentro del método `boot()`:

```php
use Illuminate\Support\Facades\Schema;

public function boot(): void
{
    Schema::defaultStringLength(191);
}
```

### 7. Ejecutar las migraciones

```bash
php artisan migrate
```

---

## Estructura del modelo Product

La tabla `products` contiene los siguientes campos:

| Campo | Tipo |
|---|---|
| id | bigint (auto) |
| description | string |
| price | double(8,2) |
| stock | integer |
| created_at | timestamp |
| updated_at | timestamp |

Asignación masiva en `app/Models/Product.php`:

```php
protected $fillable = ['description', 'price', 'stock'];
```

---

## Rutas disponibles

En `routes/web.php`:

```php
use App\Http\Controllers\ProductController;

Route::resource('products', ProductController::class);
```

| Método | Ruta | Acción |
|---|---|---|
| GET | /products | Listar productos |
| GET | /products/create | Formulario de creación |
| POST | /products | Guardar producto |
| GET | /products/{id}/edit | Formulario de edición |
| PUT/PATCH | /products/{id} | Actualizar producto |
| DELETE | /products/{id} | Eliminar producto |

---

## Ejecución del proyecto

```bash
php artisan serve
```

Abrir en el navegador: [http://127.0.0.1:8000/products](http://127.0.0.1:8000/products)

---

## Generación del CRUD (referencia)

El CRUD fue generado automáticamente con:

```bash
composer require ibex/crud-generator --dev
php artisan vendor:publish --tag=crud
php artisan make:crud products
```

Stack seleccionado: **Bootstrap**

---

## Solución de errores comunes

| Error | Solución |
|---|---|
| Error de longitud de clave | Agregar `Schema::defaultStringLength(191)` en `AppServiceProvider` |
| Tablas ya existen | Ejecutar `php artisan migrate:fresh` |
| Error de sesiones | Agregar `SESSION_DRIVER=file` en `.env` |
| Error de configuración | Ejecutar `php artisan config:clear` |
| Error de clases | Ejecutar `composer dump-autoload` |
| Error de Vite/assets | Reemplazar `@vite` en `layouts/app.blade.php` por CDN de Bootstrap 5 |

---

## Autor

**Fernando**  
Repositorio: [github.com/isfernandou-beep/CrudLab](https://github.com/isfernandou-beep/CrudLab)  
Curso: Desarrollo de Aplicaciones Web
