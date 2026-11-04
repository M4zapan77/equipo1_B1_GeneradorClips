# ClipQuest

ClipQuest es un proyecto que busca ayudar a **creadores aficionados de contenido de Fortnite que editan sus propias grabaciones** a localizar escenas mediante una descripción breve. La primera versión recibirá un video de hasta cinco minutos y una consulta en inglés, y propondrá marcas de tiempo con vistas previas para que el creador seleccione los momentos que desea convertir en clips. Las pruebas iniciales se realizarán con grabaciones de Fortnite.

## Equipo

Herramientas de Procesamiento para IA · Grupo B · Equipo 1 · Ibero León · Otoño 2026

| Integrante | Papel en el proyecto |
| --- | --- |
| Diego Isaac Rico Hernández | Responsable del README y apoyo en la investigación de la problemática |
| César Iván Macías Anguiano | Investigación de la problemática |
| Ernesto Tehuintle Ramírez | Investigación de la problemática |
| Sebastián Guerrero Ambriz | Investigación de la problemática |

## Problemática

Para preparar clips de Fortnite, un creador debe localizar escenas dentro de sus grabaciones y revisar si corresponden a lo que quiere mostrar. Cuando recuerda una característica visual de la escena, pero no el momento en que ocurrió, necesita recorrer el video hasta encontrarla. ClipQuest propone una búsqueda por descripción que devuelva momentos candidatos y facilite esa revisión. El posible ahorro de tiempo y la relevancia de los resultados deberán comprobarse con grabaciones y consultas de prueba.

[Investigación de la problemática](docs/investigacion.md)

## Caso de uso

**Usuario:** creador aficionado que graba sus partidas de Fortnite y edita su propio contenido.

1. El usuario proporciona una grabación propia o autorizada de hasta cinco minutos.
2. Escribe una descripción breve en inglés de un elemento o una situación visible que quiere encontrar.
3. El sistema extrae fotogramas con sus marcas de tiempo y los compara con la descripción.
4. El usuario recibe momentos ordenados por similitud, acompañados de una vista previa y su tiempo dentro del video.
5. Revisa los resultados y decide qué fragmentos utilizar en su edición.

La primera versión se evaluará con un conjunto acotado de búsquedas visuales en Fortnite. El criterio de utilidad será encontrar escenas relacionadas con la consulta y facilitar su localización; la selección final del clip corresponde al creador.
