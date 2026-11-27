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

La respuesta incluye el campo `next`, que permite identificar la URL de la siguiente página de resultados. Cuando no existen más resultados, este campo puede ser `null`.

La aplicación utilizará este campo para determinar si es posible continuar cargando más personajes.


## 3. Identificadores de personajes

Los personajes cuentan con identificadores que permiten consultar sus detalles individuales.

La API permite acceder a un personaje mediante una URL específica, por ejemplo:

`https://swapi.dev/api/people/17/`

La respuesta de este endpoint será utilizada para analizar el comportamiento de los identificadores y la disponibilidad de los recursos.


## 4. Orden de las películas

El endpoint `films/` proporciona información sobre las películas de Star Wars.

Los datos recibidos serán organizados para presentar las películas en orden ascendente según el número de episodio, independientemente del orden en el que sean entregadas por la API.

---



