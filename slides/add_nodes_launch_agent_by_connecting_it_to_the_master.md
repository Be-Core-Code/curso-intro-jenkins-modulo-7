#### _Launch agent by connecting it to the master_

A veces, podemos encontrarnos con configuraciones de red que no permiten
que el maestro llegue al resto de nodos por SSH.

Jenkins dispone de otra forma de levantar un agente para solventar este tipo de situaciones.

^^^^^^

#### Añadir nodos: JNLP - Agente

⚠️ **¡Atención!** El soporte para Java Web Start se ha retirado a 
[partir de la versión 11 de Java](https://en.wikipedia.org/wiki/Java_Web_Start#Deprecation) ⚠️

No usaremos Java Web Start en el curso. 

^^^^^^

#### _Launch agent by connecting it to the master_

En este modo de ejecución, es el agente el que se conecta al maestro a través de un puerto TCP.

notes:

Eliminaremos el agente `agente1` que creamos en la sección anterior y lo volveremos a crear.

^^^^^^
#### _Launch agent by connecting it to the master_ - Maestro

Para poder trabajar en este nodo, es necesario activar una configuración nueva.

^^^^^^
#### _Launch agent by connecting it to the master_ - Maestro

Ir a "Jenkins" -> "Administrar Jenkins" -> "Configuración global de seguridad"

![add_nodes_jnlp_master_configuration](/slides/images/add_nodes_jnlp_master_configuration.png)

^^^^^^
#### _Launch agent by connecting it to the master_ - Maestro

Creamos un nuevo nodo: ir a "Jenkins" -> "Administrar Jenkins" -> "Admnistrar nodos"

![add_nodes_jnlp_create_node_step_1](/slides/images/add_nodes_jnlp_create_node_step_1.png)<!-- .element: style="height: 50vh" -->

^^^^^^
#### _Launch agent by connecting it to the master_ - Maestro

![add_nodes_jnlp_create_node_step_2](/slides/images/add_nodes_jnlp_create_node_step_2.png)

^^^^^^
#### _Launch agent by connecting it to the master_ - Maestro
 
Configuramos un nuevo nodo con la opción _Launch agent by connecting it to the master_

![add_nodes_jnlp_create_node_step_3](/slides/images/add_nodes_jnlp_create_node_step_3.png)<!-- .element: style="height: 50vh" -->


^^^^^^
#### _Launch agent by connecting it to the master_ - Maestro
 

![add_nodes_jnlp_create_node_step_4](/slides/images/add_nodes_jnlp_create_node_step_4.png)

notes:

Una vez configurado el agente, este queda en modo fuera de línea hasta que el agente se conecte
al maestro.

^^^^^^
#### _Launch agent by connecting it to the master_ - Maestro

Si haces click sobre status, veremos las instrucciones para conectar el agente al maestro.

![add_nodes_jnlp_create_node_step_5](/slides/images/add_nodes_jnlp_create_node_step_5.png)

^^^^^^
#### _Launch agent by connecting it to the master_ - Agente

Una vez configurado el maestro, configuramos el agente (esclavo).

Abrimos una terminal en el agente.

^^^^^^
#### _Launch agent by connecting it to the master_ - Agente

Lo primero que haremos será descargarnos el fichero agent.jar de la URL 
`http://IP_O_URL_DEL_MAESTRO:8080/jnlpJars/agent.jar`

notes:

Esta URL podemos obtenerla desde la página del agente en el maestro:

![Connect from agent](/slides/images/add_nodes_jnlp_connect_from_agent_step_1.png)

^^^^^^
#### _Launch agent by connecting it to the master_ - Agente

```bash 
agente_jnlp $ java -jar agent.jar \ 
-jnlpUrl http://192.168.157.131:8080/computer/agente_jlnp/slave-agent.jnlp \ 
-secret f53842ae85371a429a32af9913b085ba4068fcecb25d8b3f55fc0b345313a8cb \ 
-workDir "/home/jks/jenkins" \
-failIfWorkDirIsMissing  
```

notes:

Ejecutamos este comando desde el agente teniendo en cuenta que:

* La IP o el nombre del agente serán diferentes
* El `secret` será el que nos facilite nuestro servidor
* La URL contendrá el nombre de vuestro agente

^^^^^^
#### _Launch agent by connecting it to the master_ - Agente

```bash
Feb 14, 2020 3:17:31 PM org.jenkinsci.remoting.engine.WorkDirManager initializeWorkDir
INFO: Using /home/jks/jenkins/remoting as a remoting work directory
Feb 14, 2020 3:17:31 PM org.jenkinsci.remoting.engine.WorkDirManager setupLogging
INFO: Both error and output logs will be printed to /home/jks/jenkins/remoting
Feb 14, 2020 3:17:31 PM hudson.remoting.jnlp.Main createEngine
INFO: Setting up agent: agente_jnlp
Feb 14, 2020 3:17:31 PM hudson.remoting.jnlp.Main$CuiListener <init>
INFO: Jenkins agent is running in headless mode.
Feb 14, 2020 3:17:31 PM hudson.remoting.Engine startEngine
INFO: Using Remoting version: 4.0
Feb 14, 2020 3:17:31 PM org.jenkinsci.remoting.engine.WorkDirManager initializeWorkDir
INFO: Using /home/jks/jenkins/remoting as a remoting work directory
Feb 14, 2020 3:17:31 PM hudson.remoting.jnlp.Main$CuiListener status
INFO: Locating server among [http://localhost:8080/, http://192.168.157.131:8080/]
Feb 14, 2020 3:17:31 PM org.jenkinsci.remoting.engine.JnlpAgentEndpointResolver resolve
INFO: Remoting server accepts the following protocols: [JNLP4-connect, Ping]
Feb 14, 2020 3:17:31 PM hudson.remoting.jnlp.Main$CuiListener status
INFO: Agent discovery successful
  Agent address: 192.168.157.131
  Agent port:    8081
  Identity:      61:21:56:78:6a:e1:ff:96:d5:c5:f8:fa:c2:89:a2:e5
Feb 14, 2020 3:17:31 PM hudson.remoting.jnlp.Main$CuiListener status
INFO: Handshaking
Feb 14, 2020 3:17:31 PM hudson.remoting.jnlp.Main$CuiListener status
INFO: Connecting to 192.168.157.131:8081
Feb 14, 2020 3:17:31 PM hudson.remoting.jnlp.Main$CuiListener status
INFO: Trying protocol: JNLP4-connect
Feb 14, 2020 3:17:31 PM hudson.remoting.jnlp.Main$CuiListener status
INFO: Remote identity confirmed: 61:21:56:78:6a:e1:ff:96:d5:c5:f8:fa:c2:89:a2:e5
Feb 14, 2020 3:17:31 PM hudson.remoting.jnlp.Main$CuiListener status
INFO: Connected

```

^^^^^^
#### _Launch agent by connecting it to the master_ - Agente

![Connect from agent](/slides/images/add_nodes_jnlp_connect_from_agent_step_3.png)

