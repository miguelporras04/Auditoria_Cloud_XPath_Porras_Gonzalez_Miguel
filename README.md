Miguel Porras González 24/03/2026
Misión 1 (La Mochila de Atributos)
He extraído los atributos id, rack y estado del elemento <servidor> para centralizarlos en un <xs:attributeGroup> llamado "Atributos Servidor" en la raíz del esquema. Esto permite que la definición del servidor sea mucho más limpia, ya que ahora solo necesita una referencia (ref) a este grupo en lugar de declarar cada atributo individualmente.

Misión 2 (El Paquete de Hardware)
Se ha creado un bloque reutilizable mediante <xs:group> llamado "Componentes Hardware", el cual encapsula los elementos cpu, ram, gpu y discos. Gracias al uso de <xs:sequence>, el esquema ahora garantiza estrictamente que estos componentes aparezcan siempre en ese orden específico dentro de cualquier servidor que invoque al grupo.

Misión 3 (Control de Cantidades) 
Para reflejar la realidad de la infraestructura donde no todos los equipos son iguales, se configuró el elemento <gpu> con minOccurs="0", convirtiéndolo en un componente opcional para servidores de respaldo o bases de datos. Asimismo, se aplicó una restricción de seguridad en el almacenamiento limitando el número de elementos <disco> a un máximo de 8 mediante el atributo maxOccurs="8".

Misión 4 (Redes Excluyentes)
Se introdujo una mejora lógica en la conectividad añadiendo el elemento <red> justo después de la sección de software. Utilizando el indicador <xs:choice>, el validador ahora impide que un servidor tenga configurada una <ip_fija> y use <dhcp> simultáneamente, forzando al usuario a elegir solo una de las dos opciones de red.

Misión 5 (Auditoría Flexible)
Al final de la estructura del servidor se ha incorporado la etiqueta <auditoria>, que contiene la fecha, el técnico y una nota de revisión. Para facilitar el trabajo administrativo y permitir que los datos se rellenen sin un orden estricto, se implementó el indicador <xs:all>, lo que permite que estas tres sub-etiquetas aparezcan en cualquier posición dentro de su contenedor.

Misión 6 (El Guardián de la Integridad)
Finalmente, para evitar errores de duplicidad humana al copiar y pegar datos, se añadió la restricción <xs:unique> al elemento raíz <catalogo_cloud>. Esta regla actúa como un cerrojo de integridad que rastrea todos los atributos @id de los servidores en el documento y dispara un error si detecta que un identificador se repite.

¿Cuántas líneas de código habéis ahorrado al usar grupos?
Ahorras en 15-20 lineas de codigo
¿Qué error os da VS Code si intentáis poner dos servidores con el mismo ID?
Que se incumpliria un restriccion que puse en el xsd