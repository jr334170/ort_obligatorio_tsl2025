¿Qué es Ansible? Mencione dos actividades que se puedan hacer con Ansible
Ansible es una herramienta de automatización de código abierto que reduce la complejidad de la administración y puede ejecutarse en cualquier entorno, permitiendo automatizar prácticamente cualquier tarea.
Algunas de las actividades que se pueden realizar con Ansible son:
-	Eliminar la repetición y simplificar los flujos de trabajo
-	Administrar y mantener la configuración del sistema
-	Implementar continuamente software complejo


¿Qué es un playbook de Ansible?
Un playbook de Ansible es un plano técnico en YAML que define tareas de automatización para ejecutarse con mínima intervención manual sobre inventarios o dispositivos específicos de TI.
Contiene uno o más plays (conjuntos de tareas) que se ejecutan mediante módulos, permitiendo automatizar acciones en servidores, redes, sistemas de seguridad, plataformas como Kubernetes o repositorios de código.
Se pueden guardar, compartir y reutilizar, garantizando que los procesos se realicen siempre de forma uniforme.
3.	¿Qué información contiene un inventario de Ansible?
Un inventario de Ansible contiene la lista de nodos administrados o hosts sobre los que se ejecutará la automatización, junto con las variables asociadas a cada uno. También puede incluir grupos de hosts para organizarlos, definir variables en bloque y facilitar su selección mediante patrones.
El inventario puede ser estático (por ejemplo, un archivo en /etc/ansible/hosts) o dinámico, generado desde fuentes como proveedores de nube, y puede combinar múltiples archivos o fuentes para mayor flexibilidad.





Explique que es un módulo de Ansible y dé un ejemplo.
Un módulo de Ansible es una unidad de código que ejecuta tareas específicas de TI, cómo gestionar conexiones de red, configurar sistemas, administrar seguridad,usuarios, nubes o servicios. Los módulos se utilizan dentro de tareas, que forman parte de plays y playbooks, para automatizar diferentes casos prácticos.
Ejemplos:
●	ansible.builtin.dnf: instala, actualiza o elimina paquetes y grupos utilizando el
gestor de paquetes “dnf” en sistemas basados en Fedora.
●	ansible.builtin.service: gestiona servicios en hosts remotos, permitiendo iniciarlos, detenerlos o reiniciarlos, entre otras acciones.


¿Qué ventajas tiene Ansible sobre otros métodos de automatización?
Su principal ventaja frente a otros sistemas de automatización radica en su diseño sin agentes, que elimina la necesidad de instalar software adicional en los nodos administrados y reduce la complejidad de la infraestructura. Además, su lenguaje simple basado en YAML y su facilidad de despliegue lo hacen accesible incluso para equipos con poca experiencia en programación. Estas características, junto con su capacidad para describir cómo los sistemas se interrelacionan y su amplia compatibilidad, convierten a Ansible en una solución más ligera, flexible y eficiente que muchas alternativas propietarias o basadas en agentes.
