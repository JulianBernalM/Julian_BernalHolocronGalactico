# Holocrón Galáctico

Aplicación Android desarrollada en Kotlin y Jetpack Compose que permite explorar información del universo de Star Wars utilizando la API pública SWAPI (Star Wars API).

## Descripción del proyecto

Holocrón Galáctico es una aplicación móvil que permite consultar personajes y películas del universo Star Wars, mostrando información obtenida desde una API REST.

El proyecto se desarrolla utilizando Kotlin, Jetpack Compose y una arquitectura organizada por responsabilidades, siguiendo los lineamientos del taller final.

## Tecnologías utilizadas

- Kotlin
- Jetpack Compose
- Android Studio
- Retrofit
- API REST
- SWAPI
- MVVM
- Arquitectura en capas

## API utilizada

**SWAPI — Star Wars API**

URL base:

https://swapi.dev/api/

### Endpoints principales

| Recurso | Endpoint |
|---|---|
| Listado de personajes | `people/` |
| Búsqueda de personajes | `people/?search={texto}` |
| Paginación de personajes | `people/?page={n}` |
| Detalle de personaje | `people/{id}/` |
| Planeta de origen | `planets/{id}/` |
| Listado de películas | `films/` |

---

# Contrato de la API

## 1. Campos de personajes (`people`)

Los datos de personajes son recibidos desde SWAPI en formato JSON.

| Campo | Tipo JSON | Descripción |
|---|---|---|
| `name` | String | Nombre del personaje |
| `height` | String | Estatura |
| `mass` | String | Masa |
| `hair_color` | String | Color del cabello |
| `skin_color` | String | Color de piel |
| `eye_color` | String | Color de ojos |
| `birth_year` | String | Año de nacimiento |
| `gender` | String | Género |
| `homeworld` | String | URL del planeta de origen |
| `films` | Array de String | URLs de las películas en las que aparece |

Los valores numéricos, como la estatura y la masa, son recibidos como cadenas de texto. Además, algunos atributos pueden contener valores como `unknown` o `n/a`, por lo que deben validarse antes de realizar conversiones numéricas.

## 2. Paginación

La API utiliza paginación para entregar los personajes en diferentes páginas.

Al consultar `people/?page=9`, se observó que la respuesta contiene:

- `count`: 82 personajes.
- `next`: null.
- `previous`: URL de la página anterior.

El campo `next` permite identificar si existe una página siguiente. Cuando su valor es `null`, significa que no hay más resultados disponibles para avanzar.

La aplicación utilizará este campo para controlar la paginación y evitar solicitar páginas inexistentes.


## 3. Identificadores de personajes

Se realizó una consulta al endpoint `people/17/`, obteniendo la siguiente respuesta:

```json
{
  "detail": "Not found."
}

- El resultado indica que el recurso solicitado no está disponible en la API.

- Por lo tanto, no se debe asumir que todos los identificadores numéricos de personajes son válidos. La aplicación deberá manejar correctamente las respuestas de recursos inexistentes y evitar depender de IDs consecutivos.


## 4. Orden de las películas
El endpoint films/ devuelve seis películas. En la consulta realizada se observó que el listado comienza con el Episodio IV (A New Hope), por lo que los resultados no llegan ordenados cronológicamente por número de episodio.

El orden recibido por la API es:

IV, V, VI, I, II, III.

Para Holocrón Galáctico, las películas se mostrarán ordenadas de forma ascendente según el campo episode_id, presentando los episodios del I al VI.

Este ordenamiento se realizará en la capa de datos correspondiente y no dentro de los Composables de la interfaz.


- **3. Identificadores de personajes** → título independiente.
- El JSON → dentro de su bloque correctamente delimitado.
- **4. Orden de las películas** → nuevo título independiente, con separación visual.
- Sin la sección adicional `Lo importante`.

No necesitas modificar ninguna configuración de Android Studio ni del proyecto. Es únicamente una limpieza del contenido de `README.md`.