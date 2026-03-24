# Tutorial 04 - Django REST API (To-Do App)

Tutorial de construcción de una API REST completa con Django REST Framework, incluyendo autenticación por tokens, operaciones CRUD y endpoints de signup/login.

## Tecnologías

- Python 3.13
- Django 6.0
- Django REST Framework 3.17
- SQLite

## Instalación

```bash
# Clonar el repositorio
git clone https://github.com/Pacha-e/Tutorial-Django-todo-API.git
cd Tutorial-Django-todo-API

# Crear entorno virtual
python -m venv venv
venv\Scripts\activate  # Windows
# source venv/bin/activate  # Mac/Linux

# Instalar dependencias
pip install django djangorestframework

# Aplicar migraciones
python manage.py migrate

# Crear superusuario
python manage.py createsuperuser

# Correr el servidor
python manage.py runserver
```

## Endpoints de la API

| Método | URL | Descripción | Auth requerida |
|--------|-----|-------------|----------------|
| POST | `/api/signup/` | Registrar nuevo usuario | No |
| POST | `/api/login/` | Iniciar sesión y obtener token | No |
| GET | `/api/todos/` | Listar todos los To-Dos del usuario | Sí |
| POST | `/api/todos/` | Crear un nuevo To-Do | Sí |
| GET | `/api/todos/<id>` | Ver un To-Do específico | Sí |
| PUT | `/api/todos/<id>` | Editar un To-Do | Sí |
| DELETE | `/api/todos/<id>` | Eliminar un To-Do | Sí |
| PUT | `/api/todos/<id>/complete` | Marcar/desmarcar como completado | Sí |

## Autenticación

La API usa autenticación por **Token**. Para obtener un token:

```bash
# Signup
POST /api/signup/
{
    "username": "tuusuario",
    "password": "tucontraseña"
}

# Respuesta
{
    "token": "9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
}
```

Para usar el token en las peticiones autenticadas, agrégalo en el header:

```
Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b
```

## Ejemplos de uso con curl

```bash
# Listar To-Dos
curl http://127.0.0.1:8000/api/todos/ -H "Authorization: Token <TU_TOKEN>"

# Crear un To-Do
curl -X POST http://127.0.0.1:8000/api/todos/ \
  -H "Authorization: Token <TU_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{"title": "Mi tarea", "memo": "Descripción"}'

# Marcar como completado
curl -X PUT http://127.0.0.1:8000/api/todos/1/complete \
  -H "Authorization: Token <TU_TOKEN>"
```

## Estructura del proyecto

```
todoapp/
├── backend/            # Configuración del proyecto
│   ├── settings.py
│   └── urls.py
├── todo/               # App del modelo ToDo
│   ├── models.py
│   └── admin.py
├── api/                # App de la API REST
│   ├── views.py
│   ├── serializers.py
│   └── urls.py
└── manage.py
```

## Panel de administración

Disponible en `http://127.0.0.1:8000/admin/` para gestionar usuarios y To-Dos directamente desde el navegador.
