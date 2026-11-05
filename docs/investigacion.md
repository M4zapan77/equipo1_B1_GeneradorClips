# Investigación de la problemática de ClipQuest

ClipQuest propone facilitar la búsqueda de escenas en grabaciones de Fortnite para creadores aficionados que editan sus propios videos. El avance de la Fase 2 documenta el problema, las alternativas disponibles y el diseño de un prototipo académico. Sus beneficios y metas se comprobarán durante el desarrollo del Parcial III; todavía no se presentan resultados de funcionamiento.

## El problema

Un creador que conserva grabaciones de sus partidas necesita seleccionar fragmentos para preparar contenido. Puede recordar un objeto, una situación o un elemento del escenario sin recordar su ubicación en el video. Encontrarlo exige revisar la grabación, desplazarse por la línea de tiempo y comprobar que la escena corresponde a lo que busca. El problema que aborda ClipQuest es esa localización previa a la edición.

La necesidad puede aparecer en sesiones extensas que contienen varias partidas. Sin embargo, no se supone una duración mínima universal de una partida ni se afirma que un video corto consiga más visitas por su duración. La propuesta se concentra en ayudar al creador a recuperar momentos que él considera útiles, conservando su criterio editorial.

Como contexto, el informe de YouTube Gaming de Stream Hatchet registra 8.8 mil millones de horas vistas durante 2025 y alrededor de seis millones de publicaciones de Shorts relacionadas con videojuegos en agosto de ese año [1]. Son indicadores de consumo de transmisiones y producción de contenido breve; no miden el tiempo de edición de un creador de Fortnite.

| Indicador | Cifra y periodo | Ámbito | Relación con el proyecto | Fuente |
| --- | --- | --- | --- | --- |
| Horas vistas en YouTube Gaming | 8.8 mil millones, durante 2025 | Transmisiones de videojuegos en YouTube Gaming | Describe el contexto de consumo de grabaciones y transmisiones; no demuestra por sí solo una necesidad de edición | [Stream Hatchet, informe 2025](https://hatchet.gg/resources/guides/2025-youtube-gaming-live-streaming-trends/) |
| Publicaciones de gaming en YouTube Shorts | Aproximadamente seis millones, en agosto de 2025 | Publicaciones cortas relacionadas con videojuegos | Contextualiza la producción de contenido breve al que puede destinarse una selección de escenas | [Stream Hatchet, informe 2025](https://hatchet.gg/resources/guides/2025-youtube-gaming-live-streaming-trends/) |

Para estudiar la necesidad concreta, el equipo comparará la búsqueda manual y la asistida sobre los mismos fragmentos. Se registrará si aparece el momento buscado y cuánto tarda la persona en localizarlo. Esto permitirá evaluar una hipótesis de utilidad sin atribuir al prototipo un ahorro todavía no medido.

Las siguientes capturas del canal TheGrefg, seleccionadas en la documentación del equipo, ilustran publicaciones de distinta duración. No constituyen una muestra representativa ni permiten atribuir diferencias de visitas a la duración.

![Ejemplo ilustrativo de una publicación de Fortnite con duración visible de 21 minutos y 46 segundos](img/ejemplo-video-corto.png)

Figura 1. Publicación con duración visible de 21:46. [Captura aportada por el equipo](https://github.com/user-attachments/assets/74116d36-d0b9-4039-a8ca-f21e0ee31691).

![Ejemplo ilustrativo de una transmisión de Fortnite con duración visible de una hora, 46 minutos y 59 segundos](img/ejemplo-video-largo.png)

Figura 2. Publicación con duración visible de 1:46:59. [Captura aportada por el equipo](https://github.com/user-attachments/assets/a0e63c70-4f89-495d-adee-eaf3f377e920).

Aunque el problema incluye grabaciones largas, la primera versión procesará **fragmentos de hasta cinco minutos**. El creador proporcionará previamente un fragmento de su grabación. La evaluación medirá la búsqueda dentro de ese fragmento e informará por separado cualquier tiempo de preparación. Este alcance permite probar la idea antes de plantear sesiones completas.

## Cómo se resuelve hoy

## Por qué con IA y por qué este modelo

Una búsqueda basada únicamente en palabras del audio no recupera necesariamente lo que aparece en pantalla. La propuesta utiliza un modelo que relaciona imágenes y texto para comparar descripciones con fotogramas. El trabajo original de CLIP estudia esa asociación y su transferencia a distintas tareas visuales [2]. Esto justifica explorar su uso, pero no garantiza precisión en Fortnite.

Se conserva `openai/clip-vit-base-patch32`, elegido en la Fase 1. La Model Card describe sus codificadores de imagen y texto y advierte dificultades con categorías muy específicas y conteo de objetos [3]. Por ello, las primeras consultas se formularán en inglés y describirán elementos visibles; las búsquedas ambiguas y las acciones que requieren contexto temporal se tratarán como posibles limitaciones.

| Modelo | Parámetros aproximados | Licencia | Ventajas para el prototipo | Desventajas o aspectos por comprobar |
| --- | --- | --- | --- | --- |
| [CLIP ViT-B/32](https://huggingface.co/openai/clip-vit-base-patch32) | 151.28 millones | [MIT](https://github.com/openai/CLIP/blob/main/LICENSE) [4] | Continúa el trabajo de la Fase 1 y permite comparar imagen y texto; su cantidad de parámetros es menor que la de la alternativa indicada | Su desempeño con escenas y objetos de Fortnite no se ha medido; puede confundir detalles visuales o consultas poco precisas |
| [SigLIP base-patch16-224](https://huggingface.co/google/siglip-base-patch16-224) | La ficha indica 0.2B, aproximadamente 200 millones para el modelo completo | Apache 2.0, indicada en su ficha [5] | También permite recuperación imagen-texto; ofrece una alternativa para comparar los mismos casos | Tiene más parámetros que el CLIP elegido y aún no se dispone de mediciones locales de precisión, memoria o tiempo |

SigLIP introduce una función de pérdida sigmoide para el entrenamiento de pares imagen-texto [6]. Esa diferencia no demuestra por sí misma que sea más rápido o más preciso en este proyecto. La elección inicial de CLIP se justifica por continuidad, documentación disponible y una estimación menor de memoria de pesos; no supone una superioridad ya comprobada frente a SigLIP.

El modelo calculará la afinidad entre cada fotograma y la consulta. La aplicación se encargará de validar el video, extraer fotogramas, conservar sus tiempos, ordenar los resultados y mostrar vistas previas. Una puntuación alta servirá para ordenar candidatos; no se presentará como una probabilidad calibrada de que la escena sea correcta.

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
