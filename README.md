# Hola Mundo 2 - Django

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Django](https://img.shields.io/badge/Django-6.1.3-092E20?logo=django&logoColor=white)](https://www.djangoproject.com/)
[![SQLite](https://img.shields.io/badge/SQLite-Base%20de%20datos-003B57?logo=sqlite&logoColor=white)](https://www.sqlite.org/)
[![License](https://img.shields.io/badge/license-No%20specified-lightgrey)](#licencia)

Aplicacion web construida con Django que muestra una pagina de inicio con el mensaje **"Hola mundo en Django"**.

Este proyecto sirve como base educativa para aprender la estructura de un proyecto Django, el sistema de rutas, las vistas basadas en clases y el uso de plantillas HTML.

---

## Tabla de contenidos

- [Caracteristicas](#caracteristicas)
- [Tecnologias](#tecnologias)
- [Requisitos](#requisitos)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Instalacion en Windows](#instalacion-en-windows)
- [Ejecucion](#ejecucion)
- [Rutas disponibles](#rutas-disponibles)
- [Comandos utiles](#comandos-utiles)
- [Arquitectura](#arquitectura)
- [Solucion de problemas](#solucion-de-problemas)
- [Configuracion para desarrollo](#configuracion-para-desarrollo)
- [Contribuciones](#contribuciones)
- [Licencia](#licencia)

---

## Caracteristicas

- Configuracion creada con Django.
- Aplicacion `pages` separada de la configuracion principal.
- Pagina de inicio renderizada desde una plantilla HTML.
- Administracion disponible mediante `/admin/`.
- Base de datos SQLite incluida para desarrollo.
- Entorno virtual recomendado para aislar las dependencias.
- Compatible con entornos locales de Windows.

---

## Tecnologias

| Tecnologia | Version | Uso |
|---|---:|---|
| Python | 3.12 | Lenguaje principal |
| Django | 6.1.3 | Framework web |
| SQLite | Incluida con Python | Base de datos local |
| HTML5 | - | Plantilla de interfaz |
| asgiref | 3.13.0 | Soporte ASGI |
| sqlparse | 0.6.1 | Procesamiento SQL |
| tzdata | 2026.6 | Datos de zonas horarias |

---

## Requisitos

- Windows 10 u 11.
- Python 3.12 o una version compatible con Django 6.1.
- `pip`, incluido normalmente con Python.
- Git, opcional, para clonar el repositorio.
- Un navegador web moderno.

Comprueba la instalacion de Python:

```powershell
python --version
python -m pip --version
```

---

## Estructura del proyecto

```text
hola_mundo2/
├── django_base/                 # Configuracion principal del proyecto
│   ├── settings.py              # Ajustes, aplicaciones y base de datos
│   ├── urls.py                  # Rutas principales
│   ├── asgi.py                  # Punto de entrada ASGI
│   └── wsgi.py                  # Punto de entrada WSGI
├── pages/                       # Aplicacion principal
│   ├── migrations/              # Migraciones de Django
│   ├── admin.py                 # Configuracion del panel administrativo
│   ├── apps.py                  # Configuracion de la aplicacion
│   ├── models.py                # Modelos de datos
│   ├── tests.py                 # Pruebas automatizadas
│   ├── urls.py                  # Rutas de la aplicacion
│   └── views.py                 # Vista de la pagina de inicio
├── templates/
│   └── home.html                # Plantilla principal
├── .venv/                       # Entorno virtual local, no versionado
├── db.sqlite3                   # Base SQLite de desarrollo
├── manage.py                    # CLI de administracion de Django
├── requirements.txt             # Dependencias del proyecto
└── .gitignore                   # Archivos excluidos de Git
```

---

## Instalacion en Windows

### 1. Clonar el repositorio

```powershell
git clone https://github.com/Pansitaxe/hola-mundo-2-nov-26.git
cd hola-mundo-2-nov-26
```

Si ya tienes el proyecto descargado, abre una terminal y entra en la carpeta:

```powershell
cd C:\Users\Pc\Desktop\hola_mundo2
```

### 2. Crear el entorno virtual

```powershell
python -m venv .venv
```

### 3. Activar el entorno virtual

PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Si PowerShell bloquea la ejecucion del script, habilita temporalmente scripts locales:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

Command Prompt:

```bat
.venv\Scripts\activate.bat
```

Al activar correctamente el entorno, apareceran `(.venv)` al inicio de la terminal.

### 4. Instalar las dependencias

Con el entorno virtual activo:

```powershell
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### 5. Preparar la base de datos

El proyecto incluye SQLite y no requiere instalar un servidor de base de datos.

```powershell
python manage.py migrate
```

---

## Ejecucion

Inicia el servidor de desarrollo:

```powershell
python manage.py runserver
```

Abre tu navegador en:

- Sitio principal: http://127.0.0.1:8000/
- Panel administrativo: http://127.0.0.1:8000/admin/

Para detener el servidor, presiona `Ctrl+C` en la terminal.

Para aceptar conexiones desde una red local:

```powershell
python manage.py runserver 0.0.0.0:8000
```

---

## Rutas disponibles

| Metodo | Ruta | Nombre Django | Descripcion |
|---|---|---|---|
| `GET` | `/` | `home` | Renderiza `templates/home.html` |
| `GET` | `/admin/` | Django Admin | Panel administrativo integrado |

---

## Comandos utiles

### Desarrollo

```powershell
# Iniciar el servidor
python manage.py runserver

# Ejecutar pruebas
python manage.py test

# Comprobar errores y configuracion
python manage.py check

# Crear archivos de migracion
python manage.py makemigrations

# Aplicar migraciones
python manage.py migrate

# Abrir consola interactiva de Django
python manage.py shell
```

### Administracion

```powershell
# Crear un superusuario para entrar al panel
python manage.py createsuperuser

# Reunir archivos estaticos para despliegue
python manage.py collectstatic
```

---

## Arquitectura

El flujo de una peticion a la pagina principal es:

```text
Navegador
   |
   v
django_base/urls.py
   |
   v
pages/urls.py
   |
   v
HomePageView (TemplateView)
   |
   v
templates/home.html
```

La configuracion principal se encuentra en `django_base`. La funcionalidad especifica se organiza en la aplicacion `pages`, mientras que las plantillas compartidas se encuentran en `templates`.

### Componente principal

`pages/views.py` define una vista basada en clases:

```python
from django.views.generic import TemplateView


class HomePageView(TemplateView):
    template_name = 'home.html'
```

Esta vista utiliza `TemplateView` para cargar directamente la plantilla `home.html` sin consultar datos ni ejecutar logica adicional.

---

## Configuracion para desarrollo

La configuracion actual esta pensada exclusivamente para desarrollo local:

- `DEBUG = True`
- `ALLOWED_HOSTS = []`
- Base de datos SQLite.
- Zona horaria UTC.
- Idioma configurado como `en-us`.
- El correo usa el backend de consola.

Antes de desplegar en produccion, la clave secreta debe moverse a una variable de entorno y deben revisarse como minimo `DEBUG`, `ALLOWED_HOSTS`, seguridad HTTPS, archivos estaticos y el motor de base de datos.

---

## Solucion de problemas

### `python` no se reconoce

Instala Python desde https://www.python.org/downloads/ y activa **Add Python to PATH** durante la instalacion.

### Django no esta instalado

Activa el entorno virtual y ejecuta:

```powershell
python -m pip install -r requirements.txt
```

### La activacion de PowerShell esta bloqueada

Usa Command Prompt:

```bat
.venv\Scripts\activate.bat
```

### El puerto 8000 esta ocupado

Puedes iniciar el servidor en otro puerto:

```powershell
python manage.py runserver 8001
```

### Los cambios no aparecen

- Guarda los archivos modificados.
- Reinicia el servidor si cambiaste ajustes globales.
- Recarga la pagina con `Ctrl+F5`.

---

## Contribuciones

Las contribuciones son bienvenidas.

1. Crea una rama nueva:

```powershell
git checkout -b feature/nueva-funcionalidad
```

2. Realiza tus cambios.
3. Ejecuta las pruebas:

```powershell
python manage.py test
python manage.py check
```

4. Confirma y envia la rama:

```powershell
git add .
git commit -m "Agrega nueva funcionalidad"
git push origin feature/nueva-funcionalidad
```

5. Abre un Pull Request en GitHub.

---

## Licencia

Este proyecto no declara una licencia todavia. Antes de redistribuirlo o reutilizarlo fuera de fines educativos, se recomienda agregar un archivo de licencia apropiado.

---

<div align="center">

Hecho con Django y Python

</div>
