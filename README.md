# Servidor Web Multi-Hilos en Java

## Descripción

En este proyecto de realiza la implemetnación de un servidor web empleando el lenguaje de programación Java. Este servidor se encarga de manejar peticiones HTTP de manera concurrente haciendo uso del patrón **ThreadPool** para mejorar la eficiencia, manejo de hilos y respuesta a múltiples clientes.

El servidor escucha en el puerto **6879** y responde con una página estática HTML. Se pueden obtener dos respuestas HTML cuando se accede a `127.0.0.1:6789/<archivo-html>`, pudiendo ser reemplazado `<archivo-html>` por `miarchivo.html` o `index.html`

## Estructura del Proyecto

```
Servidor-Web/
|
|-- .metals/
|-- -vscode/
|-- README.md      # Documentación del proyecto
|-- .gitignore
|-- index.html     # Archivo html de respuesta
|-- miarchivo.html # Archivo html de respuesta
|-- ServidorWeb.java    # Servidor Web simple sin concurrencia
|-- ServidorWeb1.java   # Servidor Web con concurrencia e implementación del patrón ThreadPool
```

## Compilación y Ejecución

A continuación, se especifican los pasos a seguir para compilar y ejecutar correctamente el proyecto:

1. Abre una terminal (cmd, powershell, en vscode, etc.) en la carpeta principal del proyecto.

2. Compila el servidor web concurrente `javac ServidorWeb1.java`

3. Ejecuta el servidor web concurrente para que se encuentre en un estado de escucha `java ServidorWeb1`

4. Accede al navegador web de su preferencia (Firefox, Chrome, Edge, etc.) e ingrese una de las siguientes direcciones: `127.0.0.1:6879/miarchivo.html`, `127.0.0.1:6879/index.html`.

## Autor

Daniel Jose Plazas Cortes