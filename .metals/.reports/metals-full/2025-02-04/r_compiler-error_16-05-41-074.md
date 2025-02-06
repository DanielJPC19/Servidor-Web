file:///C:/Users/danie/Documents/Semestre%206/Compunet/Servidor%20web%20multihilos/ServidorWeb1.java
### java.util.NoSuchElementException: next on empty iterator

occurred in the presentation compiler.

presentation compiler configuration:


action parameters:
offset: 3118
uri: file:///C:/Users/danie/Documents/Semestre%206/Compunet/Servidor%20web%20multihilos/ServidorWeb1.java
text:
```scala
import java.io.*; 
import java.net.*;
import java.util.*;

public final class ServidorWeb1{
    public static void main(String argv[]) throws Exception{
        int puerto = 6789;

        // Estableciendo el socket de escucha
        ServerSocket socketDeEscucha = new ServerSocket(puerto);

        // Procesando las solicitudes HTTP en un ciclo infinito.
        while(true){
            // Escuchando por una conexión
            Socket socketDeConexion = socketDeEscucha.accept();

            // Construye un objeto para procesar el mensaje de solicitud HTTP.
            SolicitudHttp solicitud = new SolicitudHttp(socketDeConexion);

            // Creando un nuevo hilo para procesar la solicitud.
            Thread hilo = new Thread(solicitud);

            // Iniciando el hilo.
            hilo.start();
        }

    }
}

final class SolicitudHttp implements Runnable{
    final static String CRLF = "\r\n";
    Socket socket;

    // Constructor
    public SolicitudHttp(Socket socket) throws Exception 
    {
            this.socket = socket;
    }

    // Implementa el método run() de la interface Runnable.
    public void run(){
        try {
                proceseSolicitud();
        } catch (Exception e) {
                System.out.println(e);
        }
    }

    private void proceseSolicitud() throws Exception{

        // Referencia al stream de salida del socket.
        DataOutputStream os = new DataOutputStream(socket.getOutputStream());;

        // Referencia y filtros (InputStreamReader y BufferedReader)para el stream de entrada.
        BufferedReader br = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        
        // Recoge la línea de solicitud HTTP del mensaje.
        String lineaDeSolicitud = br.readLine();

        // Muestra la línea de solicitud en la pantalla.
        System.out.println();
        System.out.println(lineaDeSolicitud);


        // recoge y muestra las líneas de header.
        String lineaDelHeader = null;
        while ((lineaDelHeader = br.readLine()).length() != 0) {
                System.out.println(lineaDelHeader);
        }

        // Extrae el nombre del archivo de la línea de solicitud.
        StringTokenizer partesLinea = new StringTokenizer(lineaDeSolicitud);
        partesLinea.nextToken();  // "salta" sobre el método, se supone que debe ser "GET"
        String nombreArchivo = partesLinea.nextToken();

        // Anexa un ".", de tal forma que el archivo solicitado debe estar en el directorio actual.
        nombreArchivo = "." + nombreArchivo;

        // Abre el archivo seleccionado.
        FileInputStream fis = null;
        boolean existeArchivo = true;
        try {
                fis = new FileInputStream(nombreArchivo);
        } catch (FileNotFoundException e) {
                existeArchivo = false;
        }

        // Construye el mensaje de respuesta.
        String lineaDeEstado = null;
        String lineaDeTipoContenido = null;
        String cuerpoMensaje = null;
        i@@
```



#### Error stacktrace:

```
scala.collection.Iterator$$anon$19.next(Iterator.scala:973)
	scala.collection.Iterator$$anon$19.next(Iterator.scala:971)
	scala.collection.mutable.MutationTracker$CheckedIterator.next(MutationTracker.scala:76)
	scala.collection.IterableOps.head(Iterable.scala:222)
	scala.collection.IterableOps.head$(Iterable.scala:222)
	scala.collection.AbstractIterable.head(Iterable.scala:935)
	dotty.tools.dotc.interactive.InteractiveDriver.run(InteractiveDriver.scala:164)
	dotty.tools.pc.MetalsDriver.run(MetalsDriver.scala:45)
	dotty.tools.pc.completions.CompletionProvider.completions(CompletionProvider.scala:50)
	dotty.tools.pc.ScalaPresentationCompiler.complete$$anonfun$1(ScalaPresentationCompiler.scala:146)
```
#### Short summary: 

java.util.NoSuchElementException: next on empty iterator