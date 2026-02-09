# 📚 Web Scraping de Libros - Books.toscrape.com

Un proyecto completo de web scraping que extrae información de libros desde **books.toscrape.com**, enriquece los datos con información de autores desde la API de Google Books, y organiza todo en una base de datos SQLite relacional.

## 📋 Descripción del Proyecto

Este proyecto realiza las siguientes tareas:

1. **Web Scraping**: Extrae datos de 50 páginas de books.toscrape.com
2. **Enriquecimiento de Datos**: Busca autores en la API de Google Books
3. **Almacenamiento**: Guarda datos en JSON y SQLite
4. **Análisis**: Realiza consultas complejas sobre la base de datos

## 📁 Estructura del Proyecto

```
Scraping_chall4/
├── prueba.ipynb                 # Notebook principal con todo el código
├── autores.json                 # JSON con títulos y autores
├── libros_scrapeados.json       # JSON con datos completos de libros
├── biblioteca.db                # Base de datos SQLite (se genera)
└── README.md                    # Este archivo
```

## 📊 Datos Extraídos

### Información de cada libro:
- **Título**: Nombre del libro
- **Precio**: En libras esterlinas (£)
- **Género**: Categoría del libro
- **Rating**: Puntuación de 1 a 5 estrellas
- **UPC**: Código único del producto
- **Disponibilidad**: Unidades en stock
- **Link**: URL del producto
- **Autor**: Obtenido desde Google Books API

## 🗄️ Estructura de la Base de Datos

### Tablas:

#### Autor
```sql
id_autor (INTEGER, PRIMARY KEY)
nombre (TEXT, UNIQUE)
```

#### Genero
```sql
id_genero (INTEGER, PRIMARY KEY)
nombre_genero (TEXT, UNIQUE)
```

#### Libro
```sql
id_libro (INTEGER, PRIMARY KEY)
titulo (TEXT, NOT NULL)
precio (REAL)
id_genero (INTEGER, FOREIGN KEY)
id_autor (INTEGER, FOREIGN KEY)
upc (TEXT)
disponibles (INTEGER)
rating (INTEGER)
link (TEXT)
```

## 🚀 Cómo Usar

### Requisitos
```bash
pip install beautifulsoup4 requests
```

### Ejecución

Abre la notebook `prueba.ipynb` y ejecuta las celdas en orden:

1. **Celdas 1**: Importar librerías
2. **Celda 2**: Crear base de datos SQLite
3. **Celda 3**: Scrapear libros (⚠️ puede tardar ~10 minutos)
4. **Celda 4**: Guardar libros en `libros_scrapeados.json`
5. **Celdas 5-6**: Obtener autores y guardar en `autores.json`
6. **Celdas 7-10**: Insertar datos en SQLite
7. **Celdas 11+**: Ejecutar consultas de análisis

## 📈 Consultas de Análisis

El proyecto incluye varias consultas SQL útiles:

### 📊 Libros por Rating
Muestra cuántos libros hay en cada clasificación de estrellas (1-5).

### 📌 Libros con Bajo Stock
Lista libros con menos de 5 unidades disponibles.

### 👤 Autores Prolíficos
Identifica autores con más de 3 libros en la base de datos.

### ❓ Autores Desconocidos
Muestra libros cuyo autor no se pudo identificar mediante la API.

### 💰 Ofertas Económicas
Lista libros disponibles por menos de 11 euros.

## 💡 Características Técnicas

- ✅ **Web Scraping**: BeautifulSoup + requests
- ✅ **Manejo de URLs**: `urllib.parse.urljoin` para URLs relativas
- ✅ **API Integration**: Google Books API
- ✅ **Base de Datos Relacional**: SQLite3 con claves foráneas
- ✅ **Gestión de Errores**: Try-catch para robustez
- ✅ **Throttling**: Delays para no sobrecargar servidores
- ✅ **Expresiones Regulares**: Para extracción de datos

## ⚠️ Notas Importantes

- El web scraping puede tomar ~10 minutos debido a las solicitudes y delays
- Algunos autores pueden aparecer como "Desconocido" si no constan en Google Books
- La base de datos SQLite se genera automáticamente
- Se respetan los tiempos de espera para no sobrecargar los servidores

Este es un proyecto educativo de web scraping. Siéntete libre de modificar y mejorar el código.
Proyecto educativo - Uso libre con responsabilidad.
