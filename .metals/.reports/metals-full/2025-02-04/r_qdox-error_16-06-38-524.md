error id: file:///C:/Users/danie/Documents/Semestre%206/Compunet/Servidor%20web%20multihilos/ServidorWeb1.java
file:///C:/Users/danie/Documents/Semestre%206/Compunet/Servidor%20web%20multihilos/ServidorWeb1.java
### com.thoughtworks.qdox.parser.ParseException: syntax error @[49,13]

error in qdox parser
file content:
```java
offset: 1349
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

    private v@@oid proceseSolicitud() throws Exception{

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
        if()
```

```



#### Error stacktrace:

```
com.thoughtworks.qdox.parser.impl.Parser.yyerror(Parser.java:2025)
	com.thoughtworks.qdox.parser.impl.Parser.yyparse(Parser.java:2147)
	com.thoughtworks.qdox.parser.impl.Parser.parse(Parser.java:2006)
	com.thoughtworks.qdox.library.SourceLibrary.parse(SourceLibrary.java:232)
	com.thoughtworks.qdox.library.SourceLibrary.parse(SourceLibrary.java:190)
	com.thoughtworks.qdox.library.SourceLibrary.addSource(SourceLibrary.java:94)
	com.thoughtworks.qdox.library.SourceLibrary.addSource(SourceLibrary.java:89)
	com.thoughtworks.qdox.library.SortedClassLibraryBuilder.addSource(SortedClassLibraryBuilder.java:162)
	com.thoughtworks.qdox.JavaProjectBuilder.addSource(JavaProjectBuilder.java:174)
	scala.meta.internal.mtags.JavaMtags.indexRoot(JavaMtags.scala:48)
	scala.meta.internal.metals.SemanticdbDefinition$.foreachWithReturnMtags(SemanticdbDefinition.scala:97)
	scala.meta.internal.metals.Indexer.indexSourceFile(Indexer.scala:485)
	scala.meta.internal.metals.Indexer.$anonfun$reindexWorkspaceSources$3(Indexer.scala:583)
	scala.meta.internal.metals.Indexer.$anonfun$reindexWorkspaceSources$3$adapted(Indexer.scala:580)
	scala.collection.IterableOnceOps.foreach(IterableOnce.scala:619)
	scala.collection.IterableOnceOps.foreach$(IterableOnce.scala:617)
	scala.collection.AbstractIterator.foreach(Iterator.scala:1306)
	scala.meta.internal.metals.Indexer.reindexWorkspaceSources(Indexer.scala:580)
	scala.meta.internal.metals.MetalsLspService.$anonfun$onChange$2(MetalsLspService.scala:927)
	scala.runtime.java8.JFunction0$mcV$sp.apply(JFunction0$mcV$sp.scala:18)
	scala.concurrent.Future$.$anonfun$apply$1(Future.scala:687)
	scala.concurrent.impl.Promise$Transformation.run(Promise.scala:467)
	java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1144)
	java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:642)
	java.base/java.lang.Thread.run(Thread.java:1575)
```
#### Short summary: 

QDox parse error in file:///C:/Users/danie/Documents/Semestre%206/Compunet/Servidor%20web%20multihilos/ServidorWeb1.java