# Investigación de la problemática de ClipQuest

> **Base de trabajo en elaboración.** César, Ernesto y Sebastián desarrollarán principalmente este documento, con apoyo de Diego. Antes de entregar, sustituyan las indicaciones de esta base por su investigación y completen las tablas. La extensión sugerida es de 1,500 a 2,500 palabras.

**Alcance acordado:** creadores aficionados que editan sus propias grabaciones de Fortnite. La primera versión buscará escenas a partir de una descripción breve en inglés, dentro de videos de hasta cinco minutos, y devolverá marcas de tiempo y vistas previas para revisión del creador.

## El problema

Desarrollar un análisis que explique:

- Qué dificultad tiene el creador al localizar escenas dentro de sus grabaciones de Fortnite.
- A quién afecta y en qué momento de su proceso de edición aparece.
- Qué consecuencias tiene para su trabajo y qué evidencia permite sostenerlo.
- Qué tan extendida es la necesidad. Distinguir las cifras generales sobre videojuegos o creación de contenido de los datos que realmente describan el problema de buscar escenas.

Incluir **al menos dos datos verificables**, con su fecha, ámbito y enlace a la fuente. Integrarlos también en el texto y explicar qué aportan al análisis.

| Dato o indicador | Cifra y periodo | Población o ámbito | Relación con el problema | Fuente con enlace |
| --- | --- | --- | --- | --- |
| | | | | |
| | | | | |

## Cómo se resuelve hoy

Investigar **al menos tres soluciones o alternativas existentes**. Pueden considerar la revisión manual y herramientas de búsqueda, selección o edición de clips. Comparar las funciones verificadas de cada alternativa y explicar sus límites para el caso de uso de ClipQuest.

| Solución o alternativa | Qué ofrece | Limitaciones para este caso de uso | Fuente con enlace |
| --- | --- | --- | --- |
| | | | |
| | | | |
| | | | |

Después de la tabla, explicar qué necesidad sigue sin cubrirse y qué aportación concreta se propone evaluar con ClipQuest. Evitar atribuir funciones o carencias a una herramienta sin comprobarlas en una fuente.

## Por qué con IA y por qué este modelo

Explicar cómo la comparación de texto e imagen podría ayudar a localizar escenas y qué ventajas se esperan frente a recorrer manualmente el video. Presentar esas ventajas como hipótesis mientras no existan pruebas del prototipo.

El modelo elegido es [`openai/clip-vit-base-patch32`](https://huggingface.co/openai/clip-vit-base-patch32). Compararlo con **al menos otro modelo de Hugging Face**. Completar y justificar la elección a partir de sus parámetros, licencia, ventajas y desventajas.

| Modelo y enlace | Parámetros | Licencia y fuente | Ventajas para ClipQuest | Desventajas o límites |
| --- | --- | --- | --- | --- |
| [CLIP ViT-B/32](https://huggingface.co/openai/clip-vit-base-patch32) | Aproximadamente 151.28 millones | [MIT](https://github.com/openai/CLIP/blob/main/LICENSE) | Permite relacionar imágenes y descripciones de texto | Su rendimiento en Fortnite debe probarse; la Model Card describe dificultades con categorías muy específicas y conteo de objetos |
| | | | | |

Precisar qué parte hará el modelo y qué parte hará la aplicación: extracción de fotogramas, conservación de tiempos, ordenamiento y presentación de resultados. Consultar la Model Card y la documentación del modelo alternativo; citar las fuentes de la comparación en el texto.

## Usuarios y requisitos

Describir al usuario principal a partir del alcance acordado: una persona que graba sus partidas de Fortnite, edita su contenido y necesita localizar escenas para preparar clips. Explicar qué sabe hacer, qué información recuerda de la escena y qué espera recibir del sistema.

Requisitos ya acordados que deben desarrollar y justificar:

- Recibir una grabación propia o autorizada de Fortnite de hasta cinco minutos.
- Aceptar una descripción breve en inglés sobre contenido visible en la escena.
- Comparar la consulta con fotogramas del video y conservar sus marcas de tiempo.
- Mostrar momentos ordenados por similitud, acompañados de una vista previa y su tiempo.
- Permitir que el creador revise los resultados y seleccione las escenas que le sirven.
- Proteger las grabaciones y evitar la publicación de datos personales.

Completar los criterios de aceptación. Las metas de precisión, tiempo y cantidad de resultados deberán acordarse con el equipo y comprobarse con pruebas.

| Requisito | Cómo se comprobará | Criterio de aceptación acordado |
| --- | --- | --- |
| Búsqueda de una escena relacionada con la consulta | | |
| Presentación de vistas previas y marcas de tiempo | | |
| Utilidad frente a una revisión manual | | |
| Manejo de grabaciones y archivos temporales | | |

## Impacto ético

Analizar los siguientes aspectos, aplicándolos al caso de ClipQuest y respaldando con fuentes las afirmaciones sobre el modelo o la infraestructura:

- **Privacidad y permisos:** consentimiento para utilizar las grabaciones, conversaciones, nombres de usuario y otros datos visibles; conservación y eliminación de archivos.
- **Sesgos y límites del modelo:** elementos visuales o situaciones que CLIP podría representar peor y cómo se evaluarán en Fortnite.
- **Personas afectadas y responsabilidad:** consecuencias de un resultado equivocado, quién revisará las sugerencias y quién responderá por la publicación de un clip.
- **Costo energético:** relación entre la ejecución en Colab con GPU, la duración del procesamiento, el número de fotogramas y los recursos utilizados. Separar las estimaciones de las mediciones que se obtengan durante las pruebas.

| Riesgo | A quién podría afectar | Mitigación propuesta | Responsable | Cómo verificar la medida |
| --- | --- | --- | --- | --- |
| | | | | |
| | | | | |
| | | | | |

## Referencias

Reunir **al menos cinco fuentes confiables**, con enlace, y citarlas en los apartados donde se utilicen. Agregar las fuentes de los datos del problema, las alternativas existentes y el modelo de comparación. Las siguientes fuentes técnicas ya corresponden al modelo elegido:

1. OpenAI. [Model Card de openai/clip-vit-base-patch32](https://huggingface.co/openai/clip-vit-base-patch32).
2. Radford, A. et al. (2021). [Learning Transferable Visual Models From Natural Language Supervision](https://arxiv.org/abs/2103.00020).
3. OpenAI. [Licencia MIT del repositorio oficial de CLIP](https://github.com/openai/CLIP/blob/main/LICENSE).

Antes de la entrega, comprobar que cada cifra y comparación tenga una fuente, que las citas del texto correspondan a esta lista y que todos los enlaces funcionen. Esta base todavía no constituye la investigación terminada.
