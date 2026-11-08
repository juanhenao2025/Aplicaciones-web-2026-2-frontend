# Aplicaciones Web 2026-2 — Frontend

Aplicación frontend individual del Examen 4 para administrar productos y otras entidades mediante una API REST desarrollada con FastAPI.

## Objetivo

Ofrecer una interfaz web para listar, buscar, crear, actualizar y eliminar productos mediante la API. El módulo Productos está integrado al menú lateral y se muestra en la ruta `/Productos`.

## Tecnologías

Dependencias declaradas en `package.json`:

- **Angular 21**: `@angular/core`, `@angular/common`, `@angular/compiler`, `@angular/forms`, `@angular/platform-browser` y `@angular/router`.
- **TypeScript**: lenguaje de la aplicación.
- **RxJS** y **tslib**: dependencias de Angular y manejo de operaciones asíncronas.
- **Angular CLI** y **@angular/build**: desarrollo y compilación.
- **Vitest** y **jsdom**: pruebas unitarias.
- **Prettier**: formato de código.

## Requisitos previos

- Node.js compatible con Angular 21.
- npm (el proyecto declara `npm@10.9.2` como gestor de paquetes).
- La API FastAPI disponible para usar las operaciones que requieren conexión al backend.

## Instalación

Desde la carpeta raíz del proyecto:

```bash
npm install
```

## Ejecución

Inicia el servidor de desarrollo con el script definido en `package.json`:

```bash
npm start
```

Abre [http://localhost:4200](http://localhost:4200/).

## Conexión con el backend

El frontend se conecta con una API REST desarrollada con FastAPI. La URL base se configura en `src/environments/environment.ts`:

```typescript
export const environment = {
  apiUrl: 'http://127.0.0.1:8000',
};
```

El servicio de Productos concatena `/products` a esa URL base. Para cambiar el host o puerto de la API, actualiza `apiUrl` en ese archivo.

## Módulo Productos

La página de Productos permite:

| Funcionalidad | Método HTTP | Endpoint |
| --- | --- | --- |
| Listar productos | GET | `/products` |
| Consultar un producto por ID | GET | `/products/{id}` |
| Crear un producto | POST | `/products` |
| Actualizar un producto | PUT | `/products/{id}` |
| Eliminar un producto | DELETE | `/products/{id}` |

El formulario permite crear productos y reutilizarse para editar un producto seleccionado. La búsqueda por ID filtra la tabla; la opción para ver todos vuelve a cargar el listado. La eliminación solicita confirmación antes de enviar la petición.

Los datos se definen en `src/app/models/product.model.ts`. Incluyen `id`, `name`, `description`, `category`, `sku`, `cost`, `stock`, `available`, `image_url` y `brand`; las solicitudes de creación y actualización envían los campos editables, sin el identificador.

## Manejo de errores

La interfaz presenta un aviso cuando una operación falla. Si la API devuelve un detalle de error, se muestra ese detalle; si no, se usa un mensaje genérico. En la búsqueda por ID se muestran mensajes específicos para un producto no encontrado, un ID inválido o falta de conexión. Para que las operaciones funcionen, el backend FastAPI debe estar iniciado y accesible en la URL configurada.

## Estructura principal

```text
src/
├── app/
│   ├── layout/
│   │   └── shell/            # Menú lateral y área de rutas
│   ├── models/               # Modelos TypeScript, incluido Product
│   ├── pages/
│   │   ├── animal/           # Página CRUD de Animales
│   │   ├── empleado/         # Página CRUD de Empleados
│   │   ├── product/          # Página de Productos
│   │   └── proveedor/        # Página CRUD de Proveedores
│   ├── services/             # Servicios HTTP por entidad
│   ├── app.config.ts         # Proveedores de router y HttpClient
│   ├── app.routes.ts         # Rutas de la aplicación
│   ├── app.ts                # Componente raíz
│   └── app.html              # Plantilla del componente raíz
├── environments/
│   └── environment.ts        # URL base de la API
├── index.html
├── main.ts
└── styles.css
```
