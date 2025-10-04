
# ------------------- PROMPT -------------------
TENGO PENSADO HACER EL SIGUIENTE PROYECTO DESDE LA PAGINA DE AWS DEVELOPER

# Proposito de la Skill
El propósito principal de esta skill de Alexa es crear una experiencia de entretenimiento interactivo y competitivo, utilizando un formato similar al del juego Akinator, pero aplicado al mundo del cine. La skill actuará como mediadora en un juego de adivinanza de películas entre dos jugadores, sin que ellos puedan darse pistas entre sí. 

Utilizando la API de The Movie Database (TMDb), Alexa guiará el juego, proporcionará pistas basadas en datos reales de las películas y evaluará las respuestas de los jugadores para determinar quién logra adivinar la película primero. La skill busca ofrecer una forma divertida y única de poner a prueba los conocimientos cinematográficos de los jugadores.

# Estructura de Proyecto
alexa-skill-hello-world/
│
├── skill.json                  # Configuración de la skill (metadatos)
├── interaction-model.json       # Modelo de interacción (intents, utterances, slots) BACKEND
│
├── lambda/                      # Código backend (AWS Lambda)
│   ├── lambda_function.py       # Código principal en Python
│   ├── api_client.py            # implementacion de api externa, importandose en lambda
└── README.md                    # Documentación básica del proyecto

# Alcances de la skill
La skill permitirá a los usuarios realizar las siguientes acciones:

- Jugar en modo individual o multijugador: 
Alexa permitirá jugar de forma individual o con 2 equipos, para más personas
- Recibir pistas progresivas: 
La skill proporcionará pistas sobre la película, como el género, los actores, la época, el número de palabras en el título, etc.
- Evaluar respuestas de los jugadores: 
Alexa procesará las preguntas de los jugadores (ej. "¿Es una comedia?", "¿Actúa Tom Hanks?") y les responderá con un "Sí", "No" o "Tal vez", según la información de la película seleccionada.
- Acceder a información de películas: 
La skill se conectará a la API de TMDb para obtener datos precisos y actualizados de una vasta base de datos de películas.
- Ofrecer una experiencia dinámica: 
Utilizará grabaciones de audio personalizadas para reaccionar a la situación del juego (ej. cuando un jugador está cerca de adivinar o está muy lejos).

# Personalizacion
Para personalizar la experiencia, la skill necesita la siguiente información de los usuarios:

- Nombres de los jugadores: 
Esto permitirá a Alexa dirigirse a cada jugador por su nombre, haciendo la interacción más personal y fluida. Por ejemplo: "Ahora es tu turno, Juan".
- Introducción al uso de la skill: 
Al lanzar la skill de Alexa de adivina la película esta te menciona que es lo que puede hacer ya sea, jugar con otro, jugar en vivo o en línea o jugar tu contra Alexa.
- Información de la película secreta: 
Al comienzo del juego, la skill solicitará a cada jugador el título de la película que ha elegido para que el otro jugador la adivine. Esta es la información central que la skill necesita para funcionar.
- Estado en el que se encuentra: 
Se medirá en base a las preguntas que ha realizado el jugador el estado en el que está el jugador (FRÍO, TIBIO, CALIENTE), esto para disparar las frases personalizadas en base a cómo va el jugador
- Preguntas preprogramadas: 
Alexa tendrá, ciertas respuestas preestablecidas de forma parcial que se suelen hacer al adivinar peliculas, para obtener ciertos datos esenciales al tener el título de la película (número de palabras, género, actores, caracteristicas de personajes, etc)

# Diseño Situacional
- Guión 1 - Inicio del Juego y Selección de Modo
Datos iniciales de la partida y su configuracion

- GUión 2: Juego en Curso (Con estados)
Comparacion de datos (pregunta dato, responde si si es correcto o no)
Estados (frio, tibio, caliente)

- Guión 3: Pistas automáticas (después de 5 intentos sin adivinar)
En base a los estados, estadisticas y situacion del jugador, decidir que hacer, como dar pistas, lanzar mensajes de voz personalizados, etc

- Guión 4: Adivinanza de la película
Comparacion del nombre con la pelicula dada

Tengo pensado distribuir el trabajo de la siguiente forma:
# Estimación Modelos Predictivos
- SEMANA 1 - Fundamentos y Estructura Básica
Iteración 1: Proyecto inicial configurado
    Intent: Setup proyecto y intents básicos
    Complejidad: 8
    Valor: 3
    Test: Revisar creación proyecto, probar frases invocación básicas

Iteración 2: Función consulta TMDb API
    Intent: Integración básica con TMDb
    Complejidad: 10
    Valor: 5
    Test: Test conexión API, respuesta datos película

Iteración 3: Juego inicio y turnos básicos
    Intent: Flujo básico del juego
    Complejidad: 12
    Valor: 8
    Test: Juego inicia, turno simple, respuestas correctas/no

- SEMANA 2 - Lógica de Juego y Estados
Iteración 1: Estados del juego
    Intent: Estado del juego (Frío, Tibio, Caliente)
    Complejidad: 12
    Valor: 8
    Test: Cambios estado según preguntas, test puntuación

Iteración 2: Modos de juego
    Intent: Modos de juego (individual, multijugador, equipos)
    Complejidad: 14
    Valor: 13
    Test: Prueba interacción en distintos modos

Iteración 3: Sistema de pistas progresivas
    Intent: Flujo básico del juego
    Complejidad: 12
    Valor: 8    
    Test: Validar pistas automáticas y progresivas según intentos

- SEMANA 3 - Experiencia y Pulido
Iteración 1: Audio y respuestas pulidas
    Intent: Sistema audio y respuestas dinámicas
    Complejidad: 14
    Valor: 13
    Test: Prueba efectos sonido, grabaciones personalizadas

Iteración 2: Personalización y UX
    Intent: Personalización y UX
    Complejidad: 10
    Valor: 5
    Test: Validar uso nombres, estados guardados, preguntas preprogramadas

Iteración 3: Entregable: Pruebas y optimización
    Intent: Testing, optimización y pulido
    Complejidad: 12
    Valor: 8    
    Test: Tests flujos completos, optimización y refinamiento


EN BASE A ESTA INFORMACION, ME GUSTARIA COMENZAR A TRABAJAR EN MI SKILL, DESDE AWS DEVELOPER, SIN EMBARGO, NO TENGO NINGUN CONOCIMIENTO DE COMO USARLO, NI CREAR UNA SKILL. DIME POR DONDE EMPEZAR, LOS PASOS ESENCIALES, EN DONDE SE ENCUENTRA CADA COSA Y QUE LAS PRIMERAS COSAS QUE DEBERIA EMPEZAR A CODIFICAR. 
