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
