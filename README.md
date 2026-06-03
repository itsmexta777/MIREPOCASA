# PROYECTO DISQUERA

Implementa Base de Datos Relacionales

## Integrantes

- Martinez Jimenez Kevin Andres
- Gonzalez Hernandez Luis Antonio
- Barajas Bañuelos Jesus Axel
- Mexta Torres Genesis
- Gutierrez Ruiz Jesus Javier
- Garcia Hernandez Joshua Alexander

**Profesor:** Jose Christian Romero Hernandez

**Grupo:** 4AVPG

**Fecha de entrega:** 28 de mayo del 2026

---

# Introducción

## Descripción General del Proyecto

“Disquera” es una aplicación web desarrollada con Django utilizando Python y el patrón de arquitectura MVT (Modelo-Vista-Template). El objetivo principal del proyecto es simular el funcionamiento de una tienda discográfica digital, donde los usuarios pueden explorar álbumes musicales, filtrarlos por categorías y realizar compras desde una plataforma web moderna e interactiva.

La aplicación fue diseñada para ofrecer una experiencia sencilla y cómoda para el usuario, permitiendo navegar entre diferentes géneros musicales, consultar información detallada de los álbumes y administrar compras mediante un sistema de carrito y pedidos. Además, el proyecto integra funciones de autenticación para el registro e inicio de sesión de usuarios.

En la parte visual se utilizó Bootstrap 5 para construir una interfaz responsiva y adaptable a distintos dispositivos, logrando una apariencia más moderna y organizada. Mientras tanto, Django se encargó de toda la lógica del sistema, la conexión con la base de datos y el manejo dinámico de la información.

---

# Arquitectura de Datos y Evolución del Backend (Modelos)

El funcionamiento interno de la aplicación se basa en una base de datos relacional administrada mediante el sistema de migraciones de Django, lo cual permite agregar nuevas funcionalidades y mantener organizada la estructura del proyecto.

Los modelos principales del sistema son los siguientes:

## Gestión de Catálogo (Category y Post)

El modelo Category se utiliza para clasificar los diferentes géneros musicales, como Rock, Reggaetón o Phonk. Cada categoría cuenta con un slug, el cual ayuda a generar URLs más limpias y fáciles de identificar.

Por otro lado, el modelo Post representa los álbumes musicales disponibles dentro de la plataforma. Este almacena información importante como:

- título
- descripción
- portada
- precio
- stock
- fecha de creación

Gracias a esta estructura es posible mostrar los álbumes dinámicamente dentro de la aplicación.

---

## Sistema Comercial e Inventario

Conforme avanzó el desarrollo del proyecto, se agregaron funciones relacionadas con ventas e inventario.

Para los precios se utilizó `DecimalField`, ya que permite manejar cantidades monetarias con mayor precisión. También se implementó `PositiveIntegerField` para el control del stock, evitando cantidades negativas y ayudando a mantener un mejor control de los productos disponibles.

El archivo `admin.py` de la aplicación disquera dentro de Django sirve para registrar los modelos en el panel de administración de Django, permitiendo que el administrador pueda agregar, visualizar, modificar y eliminar información desde la interfaz de admin.

### Importación del módulo de administración

```python
from django.contrib import admin
```

### Importación de modelos

```python
from .models import (
    Category,
    Artist,
    Post,
    Specification,
    Comment,
    CartItem
)
```

Estos modelos representan las tablas principales de la base de datos del proyecto, por ejemplo:

- Category almacena las categorías musicales.
- Artist almacena los artistas.
- Post representa los álbumes.
- Comment guarda comentarios.
- CartItem controla el carrito de compras.

### Registro de modelos

```python
admin.site.register(Category)
```

El método `admin.site.register()` le indica a Django que ese modelo debe aparecer dentro del panel de administración.

Gracias a esto el administrador puede realizar operaciones CRUD directamente desde `/admin`, es decir:

- Crear registros.
- Visualizar información.
- Modificar datos.
- Eliminar registros.

Por ejemplo, al registrar el modelo Post, el administrador puede subir nuevos álbumes musicales, cambiar precios o eliminar publicaciones directamente desde el panel de Django sin necesidad de modificar el código manualmente.

Este archivo es muy importante porque conecta los modelos de la base de datos con la interfaz administrativa del sistema.

---

## Gestión de Usuarios y Artistas

La aplicación también cuenta con un sistema de autenticación basado en el modelo de usuarios de Django.

Además, mediante relaciones `OneToOneField`, es posible crear perfiles personalizados asociados a cada usuario. Esto permite almacenar información adicional y mantener separada la lógica de autenticación de otros datos del sistema.

---

## Sistema de Compras (CartItem y Order)

El proyecto incluye un sistema completo de carrito de compras y pedidos.

El modelo CartItem almacena temporalmente los productos que el usuario desea comprar, junto con la cantidad seleccionada.

Después, durante el proceso de checkout, se genera una orden mediante el modelo Order, donde se guarda:

- información del cliente
- dirección de envío
- total de compra
- estado del pedido

De esta manera la aplicación puede llevar un historial de compras realizadas por cada usuario.

---

# Diseño de la Interfaz y Experiencia de Usuario (Frontend)

La interfaz de la aplicación fue desarrollada utilizando Bootstrap 5 y el sistema de templates de Django.

Uno de los conceptos más importantes utilizados fue la herencia de plantillas, la cual permite reutilizar código y mantener un diseño uniforme en todas las páginas.

## Plantilla Base (base.html)

El archivo `base.html` funciona como la estructura principal del proyecto. Aquí se encuentran elementos globales como:

- la navbar
- Bootstrap
- estructura HTML general
- estilos compartidos

Los demás templates heredan esta estructura usando:

```django
{% extends 'disquera/base.html' %}
```

Esto facilita mucho el mantenimiento del proyecto y evita repetir código innecesariamente.

## Página Principal (home.html)

Aquí se muestran:

- los álbumes disponibles
- categorías musicales
- botones de navegación
- acceso rápido al carrito

Los productos se presentan mediante cards de Bootstrap para lograr una interfaz más limpia y visualmente agradable.
