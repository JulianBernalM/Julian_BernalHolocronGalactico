# INVESTIGACION.md
# Holocrón Galáctico — Investigación de arquitectura

## 4.1 Conceptos de arquitectura

### 1. Arquitectura de software

La arquitectura de software define cómo se organizan los componentes de una aplicación, sus responsabilidades y las reglas de comunicación entre ellos. Su objetivo es facilitar la comprensión, el mantenimiento, las pruebas y la evolución del software.

En Holocrón Galáctico, la aplicación se organizará mediante componentes como la interfaz de usuario, los ViewModels, el Repository y los servicios encargados de comunicarse con la API SWAPI, permitiendo que cada elemento cumpla una función específica.

**Fuente:** Android Developers — Guide to app architecture  
https://developer.android.com/topic/architecture

---

### 2. Separación de responsabilidades

La separación de responsabilidades es un principio de diseño que busca que cada componente de una aplicación tenga una función específica y claramente definida. Esto evita que diferentes tareas se mezclen dentro de una misma clase y facilita su mantenimiento y modificación.

En Holocrón Galáctico, la interfaz se encargará de mostrar la información, el ViewModel administrará el estado de las pantallas y el Repository será responsable de obtener y organizar los datos provenientes de SWAPI. De esta manera, un cambio en la comunicación con la API no debería requerir modificaciones directas en los componentes visuales.

**Fuente:** Android Developers — Recommendations for Android architecture  
https://developer.android.com/topic/architecture/recommendations

---

### 3. Arquitectura en capas

La arquitectura en capas organiza una aplicación en niveles con responsabilidades específicas y relaciones de dependencia definidas. Esta estructura permite separar la presentación de los datos y facilita la evolución de cada componente de manera independiente.

Android recomienda, como estructura mínima, una capa de UI y una capa de datos, mientras que la capa de dominio es opcional y puede incorporarse cuando la complejidad o reutilización de la lógica lo requiera.

En Holocrón Galáctico utilizaremos una capa de UI para las pantallas y ViewModels, y una capa de datos para los componentes encargados de comunicarse con SWAPI, transformar la información y proporcionarla a la aplicación.

**Fuente:** Android Developers — Guide to app architecture  
https://developer.android.com/topic/architecture

---

### 4. MVVM (Model–View–ViewModel)

MVVM es un patrón de arquitectura que separa los datos y su lógica relacionada (Model), la interfaz visual (View) y la gestión del estado y las acciones de la pantalla (ViewModel). Permite que la interfaz se concentre en representar la información, mientras que el ViewModel coordina las operaciones y actualiza el estado que la UI observa.

En Holocrón Galáctico, los Composables representarán la View, los ViewModels administrarán el estado y las acciones de cada pantalla, y los componentes de datos, como el Repository y los modelos, proporcionarán la información necesaria para mostrar personajes y películas.

**Fuente:** Android Developers — UI layer  
https://developer.android.com/topic/architecture/ui-layer

---

### 5. Flujo de datos unidireccional (UDF)

El flujo de datos unidireccional es un patrón de comunicación en el que el estado fluye desde el ViewModel hacia la interfaz, mientras que las acciones o eventos del usuario viajan desde la interfaz hacia el ViewModel. Esto permite centralizar las modificaciones del estado y mantener un flujo de información organizado, predecible y fácil de mantener.

En Holocrón Galáctico, cuando el usuario realiza una búsqueda de personajes, la interfaz enviará la acción al ViewModel. Este realizará la operación correspondiente, actualizará el estado y Compose observará el resultado para representar la información o el mensaje correspondiente.

**Fuente:** Android Developers — UI layer  
https://developer.android.com/topic/architecture/ui-layer

---

### 6. Fuente única de verdad (SSOT)

La fuente única de verdad es un principio según el cual cada dato tiene un único responsable de administrarlo y modificarlo. Esto permite mantener la consistencia de la información y evita que diferentes componentes generen estados contradictorios.

En Holocrón Galáctico, el ViewModel será el responsable de administrar el estado de cada pantalla, exponiendo la información de manera que la interfaz pueda observarla sin modificarla directamente. De esta forma, los datos, los estados de carga y los errores se controlarán de forma centralizada.

**Fuente:** Android Developers — UI layer  
https://developer.android.com/topic/architecture/ui-layer

---

### 7. Inyección de dependencias (manual)

La inyección de dependencias es una técnica mediante la cual una clase recibe los componentes que necesita para funcionar, generalmente a través de su constructor, en lugar de crearlos internamente. La inyección manual consiste en que el desarrollador se encarga de crear y conectar las dependencias sin utilizar frameworks especializados.

En Holocrón Galáctico, utilizaremos un contenedor de dependencias manual para crear y conectar componentes como Retrofit, ApiService y Repository. Posteriormente, los ViewModels recibirán el Repository que necesitan, facilitando la organización, reutilización, mantenimiento y pruebas de la aplicación.

**Fuente:** Android Developers — Manual dependency injection  
https://developer.android.com/training/dependency-injection/manual

---

## Referencias bibliográficas

- Android Developers. *Guide to app architecture*. https://developer.android.com/topic/architecture
- Android Developers. *Recommendations for Android architecture*. https://developer.android.com/topic/architecture/recommendations
- Android Developers. *UI layer*. https://developer.android.com/topic/architecture/ui-layer
- Android Developers. *Manual dependency injection*. https://developer.android.com/training/dependency-injection/manual


# Parte 1 — Investigación dirigida

### Tema 1 — Arquitectura recomendada por Google

- Google recomienda organizar una aplicación Android en una capa de UI y una capa de datos. La capa de UI se encarga de mostrar la información, recibir las interacciones del usuario y actualizar la pantalla mediante componentes como Composables y ViewModels. La capa de datos administra la información, contiene los repositorios y permite acceder a fuentes como servicios web. En aplicaciones más complejas puede añadirse una capa de dominio para reutilizar lógica de negocio.

- La fuente única de verdad significa que cada dato tiene un único responsable de controlar sus modificaciones, evitando inconsistencias entre componentes.

- En Holocrón Galáctico utilizaremos una capa de UI con pantallas y ViewModels, y una capa de datos con Repository, DTO, Mapper y Retrofit para comunicarnos con SWAPI. Así, la interfaz no dependerá directamente de la API y cada componente tendrá una responsabilidad definida.

**Fuentes:**
- https://developer.android.com/topic/architecture
- https://developer.android.com/topic/architecture/recommendations

### Tema 2 — MVVM y flujo de datos unidireccional (UDF)

- MVVM (Model-View-ViewModel) es un patrón de arquitectura que separa la interfaz de usuario, los datos y la lógica de presentación. El Model representa los datos, la View muestra la información y recibe las interacciones del usuario, mientras que el ViewModel administra el estado de la pantalla y procesa las acciones.

- El flujo de datos unidireccional (UDF) establece que los eventos de usuario viajan desde la interfaz hacia el ViewModel, mientras que el estado actualizado fluye desde el ViewModel hacia la interfaz. Esto permite que la UI observe los cambios y se actualice sin gestionar directamente la lógica de los datos.

- En Holocrón Galáctico, cuando el usuario busca un personaje, la interfaz enviará la acción al ViewModel, este solicitará los datos al Repository y posteriormente actualizará el estado que Compose observará para mostrar los resultados.

**Fuentes:**
- https://developer.android.com/topic/architecture/ui-layer
- https://developer.android.com/topic/architecture

### Tema 3 — Repository, DTO y Mapper

- El patrón Repository actúa como intermediario entre el ViewModel y las fuentes de datos, centralizando la obtención y organización de la información. Permite que el ViewModel no dependa directamente de la API y facilita el mantenimiento y las pruebas.

- Un DTO (Data Transfer Object) es un objeto utilizado para representar los datos recibidos o enviados a través de una fuente externa, como una API. Su estructura puede corresponder al formato JSON de la respuesta.

- Un Mapper es un componente encargado de transformar los DTO en modelos que la aplicación utiliza internamente, permitiendo separar el formato de los datos externos de la estructura propia del proyecto.

- En Holocrón Galáctico, el Repository obtendrá los personajes de SWAPI, los DTO representarán las respuestas JSON y los Mapper transformarán los datos para utilizarlos en la aplicación.

Fuentes:

https://developer.android.com/topic/architecture/data-layer

https://developer.android.com/topic/architecture


## Tema 4 — Modelado de estados de UI

- El modelado de estados de UI consiste en representar de manera clara las diferentes situaciones en las que puede encontrarse una pantalla durante su funcionamiento. Esto permite que la interfaz responda correctamente mientras obtiene información, muestra resultados o presenta errores.

- Los estados más comunes en una aplicación que consume una API son Loading, Success y Error. Loading indica que se están cargando los datos, Success representa una operación exitosa y Error indica que ocurrió un problema durante el proceso.

- En Holocrón Galáctico, las pantallas de personajes y películas utilizarán estos estados para mostrar un indicador de carga, la información obtenida de SWAPI o un mensaje de error con la posibilidad de volver a intentar la operación.

Fuentes:

https://developer.android.com/topic/architecture/ui-layer

https://developer.android.com/develop/ui/compose/state

## Tema 5 — Coroutines: concurrencia estructurada y peticiones en paralelo

- Las Coroutines de Kotlin permiten ejecutar operaciones de larga duración sin bloquear el hilo principal de la aplicación, facilitando tareas como las solicitudes a servicios web.

- La concurrencia estructurada permite organizar las tareas dentro de un ámbito definido, controlar su ciclo de vida y gestionar su cancelación cuando ya no son necesarias. Esto ayuda a evitar tareas descontroladas y facilita el manejo de errores.

- Las peticiones en paralelo permiten ejecutar varias operaciones independientes al mismo tiempo, reduciendo el tiempo total de espera cuando los resultados no dependen unos de otros.

- En Holocrón Galáctico, las Coroutines permitirán consultar SWAPI sin bloquear la interfaz y podrán utilizarse para obtener simultáneamente información independiente, cuando el funcionamiento del taller lo requiera.

Fuentes:

https://developer.android.com/kotlin/coroutines

https://kotlinlang.org/docs/coroutines-basics.html


### Tema 6 — Manejo de errores en red

Los errores de red (`IOException`) ocurren cuando una solicitud no puede completarse debido a problemas de conectividad, como falta de internet, tiempos de espera o fallos en la conexión con el servidor. Los errores HTTP (`HttpException`) se presentan cuando el servidor recibe la solicitud, pero responde con un código que indica un problema, como un 404 (recurso no encontrado) o un 5xx (error del servidor).

En Holocrón Galáctico, solicitar `people/17/` puede producir un error 404 si el recurso no existe, mientras que una falta de conexión puede generar una excepción de red. El Repository debe gestionar estos errores y devolver un resultado controlado, por ejemplo, mediante `Result<T>`, para que el ViewModel pueda actualizar el estado de la UI sin propagar excepciones directamente.

De esta manera, la aplicación podrá diferenciar los problemas de conectividad de los errores del servidor y ofrecer mensajes adecuados al usuario.

- Sin internet ->	IOException
- Solicitar people/17/ ->	HttpException — 404

- Error del servidor -> HttpException — 5xx

¿Qué ventaja tiene Result<T>?

Permite devolver el resultado de una operación de forma controlada, representando tanto el éxito como el error. Así, el ViewModel puede gestionar el resultado sin tener que recibir excepciones inesperadas directamente.

Mensajes para el usuario:
- Sin internet: No hay conexión a internet. Verifica tu conexión e inténtalo nuevamente.
- Recurso no encontrado: No encontramos la información solicitada.
- Error del servidor: El servidor presenta problemas. Inténtalo nuevamente más tarde.


**Fuentes:**
- https://developer.android.com/topic/architecture
- https://kotlinlang.org/docs/exceptions.html