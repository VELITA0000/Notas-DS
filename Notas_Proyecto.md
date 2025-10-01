# ############################################################################################################################## #
# ------------------- INTRODUCCION SKILL -------------------
Diseñar para la voz es un “Proceso Cíclico” siguiendo ciertos pasos definidos para ir mejorando en base a la experiencia 
(investigar - diseñar - evaluar). Es parecido a la metodología ágil, donde se trabaja con dos fases (inspeccionar y adaptar). 
Para validar lo mejor es probarla con el usuario, no caer en el bucle de mejoras sino establecer un punto en el que es 
adecuado sacar el producto.
Alexa se debe adaptar al usuario, a su forma de hablar y las palabras que usa. Esa experiencia no lo tienen otras aplicaciones

# Principios:
    Disponible: estar disponible cuando el usuario lo necesite y que sea utiles
    Personal: que sea unica para el usuario, con mejoras continuas, memoria, recordar, aumentar el dialogo
    Relaciones: no llenar de palabras al usuario mantener una conversacion mas que instrucciones y tareas. respuestas cortas y concisas
    Adaptable: mejorar el dialogo natural, sin monotonia, ser accesible al usuario no seguir un guion sino adaptarse a la situacion

# Valor personal
En cada interaccion debe ser distinta la respuesta, para no crear un ambiente repetitivo,
pero sobre todo agregarle valor a cada respuesta de nuestra skill, tener variantes, hacer sentir especial al usuario. 
Agregar gamification (aire divertido y de juego) o Call to action (incentivar a mas preguntas)
Se deben evitar ordenes imperativas
Deben ser respuestas rapidas y cortas, debe haber un dialogo dinamico sin lanzar tantos datos al usuario
Usar la funcionalidad en el contexto y situacion adecuada, no esconder ciertas funciones que le dan valor a la skill
Podemos habilitar ciertas cosas personalizables y beneficios al usar la skill (escoger entre ciertos metodos de compra, de coach)
Hay tipos de skills, unos donde se maneja el dialogo, otros donde el usuario toma la iniciativa, alexa simplemente hace tareas
Hay otras skills donde alexa lidera la experiencia con el usuario, lo guia le da instrucciones, trivias, maraton, ejercicios
Hay otras que tienen intermedio, pero es importante entender la necesidad del usuario y el problema a resolver

# Working backwards
Construimos una mezcla entre ambos tipos de skills, donde en el proceso alexa obtiene mas datos para personalizar al usuario

# Scripts
Se recomienda crear un script o guion para evaluar las interacciones con alexa

# ASR (Automatic Speech Recognition)
Is a technology that uses Machine Learning to understand words and transform them
Desarrollo Basado en Eventos
Utiliza las funciones Lambda para desarrollar tus Skills y desplegarlos en la nube


# ------------------- COMPONENTES -------------------
Alexa empieza con los comandos de voz.
Para crear tus propios comandos necesitas una skill (app de voz)
Una vez creada necesitas definir los siguientes componentes para que tus usuarios puedan usar la skill
El invocation name es clave para que el usuario pueda llamar a tu skill

wake word - launch - invocation name - utterance
ALEXA - pide a - nutricionn inteligente - un consejo
         lanza

# Componentes skill:
El usuario manda un audio con un dispositivo, con el speech recognition a amazon alexa
hay un intent al servicio o la skill y este devuelve una response

Skill
- Modelo de interacción: define lo que el usuario dice (intents, utterances, slots).
- Backend/endpoint: lógica de negocio (en AWS Lambda o un servidor propio)

Intents
- Intenciones del usuario, ver que esta buscando el usuario. 
Tenemos que guiar al usuario a dar datos que nos sean utiles para un intent valido
Alexa, dame un dato curioso

Utterances
- Son las frases que disparan un intent, saber la intencion del usuario
Se mapean contra un intent
Dame un dato curioso
Dime una curiosidad

Slots
- Son variables dentro de un intent, los parametros que son utiles del intent
“curioso”, “curiosidad”. Son los componentes que se mandan a la skill
Estos pueden tener muchas variantes y se debe tener previsto eso

Handlers
- En el backend cada intent tiene un handler, la funcion que responde al intent

# Slot elicitation & bigNoMatch
Cuando un usuario lanza un intent con slots, con sinonimos que tenemos dados de alta. La
peticion tiene metadatos que marcan si el modelo de lenguaje tuvo exito o no viendo el valor
que decia el usuario. Para eso creamos una bitacora de aprendizaje y adaptable en base a
los bigNoMatch o valores que no se identifican.

# Build in intents:
intents basicos y de ayuda, acciones bases que se deben poner sobre las demas acciones para verificar la skill


# ------------------- DIAGRAMAS DE DISENO SITUACIONAL -------------------
Utterance: lo que el usuario dice
Situation: detalles de la situacion, el contexto
Changes: describe los cambios en el contexto, conductas que se sobrescriben o agregan por la situacion
Response: alexa responde en base a la situacion y el contexto
Prompt: alexa ingresa la pregunta a la respuesta para continuar la conversacion para complir el intent
    Si no hay prompt la sesion debe terminar, es decir cuando hay un error o simplemente termina la conversacion

- Ejemplo uso 1:
Utterance: alexa, abre coach universitario
Situation: primer lanzamiento
Changes: da la bienvenida y primer aviso
Response: Bienvenido a coach universitario, detalles...
Prompt: donde te gustaria ir a la escuela?

- Ejemplo uso 2:
Utterance: alexa, abre coach universitario
Situation: el usuario ha regresado por quinta vez
Changes: felicitar al usuario por constancia
Response: wow, quinto dia
Prompt: que calificacion le pondrias a tu universidad en cuanto a educacion

- Ejemplo uso 3:
Utterance: alexa, abre coach universitario
Situation: el usuario regreso una vez
Changes: en anterior busqueda pregunto esto, dar bienvenida
Response: bienvenido, en tu ultima busqueda preguntaste sobre la universidad de colorado
Prompt: que calificacion le pondrias a la universidad de colorado


# ------------------- CONCLUSION -------------------
Para resumir el proceso: el usuario dice una frase (utterance) con los componentes wake
word, launch, invocation name y la propia utterance.
Alexa NLU (Natural Language Understanding) analiza la frase, obtiene los parámetros
importantes (slots) e identifica la intención del usuario (intent).
La skill compara la utterance con los intents definidos en el modelo de interacción, y
finalmente el (handler) correspondiente recibe esos datos, ejecuta la lógica y devuelve la
respuesta que Alexa pronunciará.


# ############################################################################################################################## #
# ------------------- DESARROLLO SKILL -------------------
Para el desarrollo de la skill se trabaja desde consola, para establecer la interfaz basica.
Build: Aqui diseños el modelo de interaccion de la skill
Code: Aqui escribes o editas el codigo backend de la skill
Test: Aqui pruebas tu skill como si fueras un usuario
Distribution: Aqui preparas tu skill para compartirla
Certification: Aqui envias la skill para que amazon la revise
Analytics: Aqui ves estadisticas de uso de tu skill

# ------------------- ESTRUCTURA DE PROYECTO -------------------
Front-end (interaction-model): Lo que el usuario dice y cómo Alexa entiende esas frases.
Back-end (lambda_function): Lo que hace la skill y qué responde Alexa.

- Estructura basica:
alexa-skill/
│
├── interaction-model.json     # Modelo de interacción (intents, utterances, slots) BACKEND
├── lambda/                    # Carpeta del código backend
│   ├── lambda_function.py     # Código principal en Python
│   ├── requirements.txt       # Dependencias (si usas externas)
└── skill.json                 # Configuración de la skill

- Estructura completa:
alexa-skill-hello-world/
│
├── skill.json                  # Configuración de la skill (metadatos)
├── interaction-model.json       # Modelo de interacción (intents, utterances, slots) BACKEND
│
├── lambda/                      # Código backend (AWS Lambda)
│   ├── lambda_function.py       # Código principal en Python
│   ├── api_client.py            # implementacion de api externa, importandose en lambda
│   ├── requirements.txt         # Dependencias del proyecto
│   └── __init__.py              # (opcional, para marcar paquete)
│
└── README.md                    # Documentación básica del proyecto

# Creacion de skill
- configuracion frontend
Consola: https://developer.amazon.com/alexa
Crea una nueva skill.
Define idioma y modelo de interacción (puedes pegar tu interaction-model.json)
- configuracion backend
lambda: https://console.aws.amazon.com/lambda
Crea una función Lambda en AWS (runtime: Python 3.9+).
Sube tu código (lambda_function.py + requirements.txt).
Copia el ARN de la Lambda.
- coneccion alexa y lambda
En la consola de Alexa Developer → pestaña “Endpoint”.
Pega el ARN de tu Lambda.
- pruebas
Entra a “Test” en la consola de Alexa Developer.
Activa el “Test Simulator”.
Escribe o habla: abre hola mundo.
- recomendaciones
Siempre incluye intents default: HelpIntent, StopIntent, CancelIntent
Tener handler de errores, al no tener coincidencias con algun intent
Cumplir con politicas de privacidad de amazon

# Archivos de Ejemplo 
-  skill.json                 # Configuración de la skill 
{
  "manifest": {
    "publishingInformation": {
      "locales": {
        "es-MX": {
          "summary": "Skill para buscar información de películas usando Alexa",
          "examplePhrases": [
            "Alexa, abre buscador de películas",
            "Alexa, busca la película Titanic",
            "Alexa, dime información sobre Inception"
          ],
          "name": "Buscador de Películas",
          "description": "Con esta skill puedes consultar información básica sobre cualquier película."
        }
      },
      "isAvailableWorldwide": true,
      "testingInstructions": "Prueba diciendo: 'abre buscador de películas' y luego pide información de cualquier película.",
      "category": "EDUCATION_AND_REFERENCE"
    },
    "apis": {
      "custom": {
        "endpoint": {
          "uri": "arn:aws:lambda:REGION:ACCOUNT_ID:function:NOMBRE_DE_TU_LAMBDA"
        }
      }
    },
    "manifestVersion": "1.0"
  }
}

- interaction-model.json       # Modelo de interacción (intents, utterances, slots) BACKEND
{
  "interactionModel": {
    "languageModel": {
      "invocationName": "buscador de películas",
      "intents": [
        {
          "name": "MovieIntent",
          "slots": [
            {
              "name": "movie",
              "type": "AMAZON.Movie",
              "samples": [
                "busca la película {movie}",
                "dime información sobre {movie}",
                "quiero saber sobre {movie}"
              ]
            }
          ],
          "samples": [
            "busca una película",
            "dime una película"
          ]
        },
        {
          "name": "AMAZON.HelpIntent",
          "samples": []
        },
        {
          "name": "AMAZON.CancelIntent",
          "samples": []
        },
        {
          "name": "AMAZON.StopIntent",
          "samples": []
        }
      ]
    }
  }
}

- lambda_function.py       # Código principal en Python
import logging
import ask_sdk_core.utils as ask_utils
from ask_sdk_core.skill_builder import SkillBuilder
from ask_sdk_core.dispatch_components import AbstractRequestHandler
from ask_sdk_core.handler_input import HandlerInput
from ask_sdk_model import Response
from api_client import get_movie_info  # 👈 uso de la API

logger = logging.getLogger(__name__)
logger.setLevel(logging.INFO)

class LaunchRequestHandler(AbstractRequestHandler):
    def can_handle(self, handler_input):
        return ask_utils.is_request_type("LaunchRequest")(handler_input)
    def handle(self, handler_input):
        speak_output = "¡Bienvenido! Dime el nombre de una película para buscar."
        return handler_input.response_builder.speak(speak_output).ask(speak_output).response

class MovieIntentHandler(AbstractRequestHandler):
    def can_handle(self, handler_input):
        return ask_utils.is_intent_name("MovieIntent")(handler_input)
    def handle(self, handler_input):
        slots = handler_input.request_envelope.request.intent.slots
        movie_name = slots["movie"].value if "movie" in slots else None
        if not movie_name:
            speak_output = "No entendí el nombre de la película. ¿Cuál quieres buscar?"
        else:
            speak_output = get_movie_info(movie_name)
        return handler_input.response_builder.speak(speak_output).ask("¿Quieres buscar otra película?").response


sb = SkillBuilder()
sb.add_request_handler(LaunchRequestHandler())
sb.add_request_handler(MovieIntentHandler())
lambda_handler = sb.lambda_handler()

- api_client.py
import urllib.request
import json

API_URL = "http://www.omdbapi.com/"
API_KEY = "TU_API_KEY"

def get_movie_info(title: str):
    """Obtiene info de una película usando OMDB API con urllib"""
    url = f"{API_URL}?t={title}&apikey={API_KEY}"
    try:
        with urllib.request.urlopen(url) as response:
            data = json.load(response)
            if data.get("Response") == "True":
                return f"La película {data['Title']} fue lanzada en {data['Year']}."
            else:
                return f"No encontré información sobre {title}."
    except Exception:
        return "Error al conectar con la API de películas."


# ############################################################################################################################## #
# ------------------- DOCUMENTACION PROYECTO SKILL -------------------
# Proposito de la Skill
El propósito principal de esta skill de Alexa es crear una experiencia de entretenimiento interactivo y competitivo, utilizando un formato similar al del juego Akinator, pero aplicado al mundo del cine. La skill actuará como mediadora en un juego de adivinanza de películas entre dos jugadores, sin que ellos puedan darse pistas entre sí. 

Utilizando la API de The Movie Database (TMDb), Alexa guiará el juego, proporcionará pistas basadas en datos reales de las películas y evaluará las respuestas de los jugadores para determinar quién logra adivinar la película primero. La skill busca ofrecer una forma divertida y única de poner a prueba los conocimientos cinematográficos de los jugadores.

# Frases de invocacion
Alexa, adivina la película
Alexa, jugar Adivinanza de películas
Alexa, inicia Juego de adivinar películas
Alexa, abre Adivina la Película
Alexa, quiero jugar a Adivina la Película

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
Usuario: "Alexa, abre Adivina la Película."
Alexa: "¡Hola! Bienvenido a Adivina la Película. ¿Qué tipo de juego quieres? Puedes jugar contra mí, jugar con otro jugador, o en modo equipo."
Usuario (Jugador 1): "Quiero jugar con otro jugador."
Alexa: "Perfecto. Por favor, dime tu nombre."
Jugador 1: "Soy Juan."
Alexa: "¿Y quién es el segundo jugador?"
Jugador 2: "Soy María."
Alexa: "¡Excelente! Juan, dime en voz baja la película que quieres que María adivine."
Juan: (En voz baja) "La película es 'Interstellar'."
Alexa: "¡Entendido! María, es tu turno. Puedes empezar a hacer tus preguntas."

- GUión 2: Juego en Curso (Con estados)
María: "Alexa, ¿es una película de drama?"
Alexa: "No, no es de drama. Tienes 0 respuestas correctas. Estás frío."
(Turno de Juan)
Juan: "Alexa, ¿la película es de acción?"
Alexa: "No, no es de acción. Tienes 0 respuestas correctas. Estás frío."
(Turno de María, después de varios intentos)
María: "Alexa, ¿aparece Matthew McConaughey?"
Alexa: "¡Sí! Matthew McConaughey es uno de los actores principales. Tienes 1 respuesta correcta. Te estás poniendo tibio."
(Grabación de audio: Sonido de una bocina de cine antigua)
Alexa: "¡María, estás muy cerca! Te doy una pista extra: el director es Christopher Nolan."
(Turno de María, ya cerca de adivinar)
María: "Alexa, ¿la película es de ciencia ficción?"
Alexa: "¡Sí! Con esa y la pista anterior, estás caliente. ¡Ya casi lo tienes!"
(Turno de María, último intento)
María: "Alexa, ¿la película es 'Interstellar'?"
Alexa: "¡Correcto! ¡Felicidades, María! Has adivinado la película."
(Grabación de audio: Música de victoria o aplausos)

- Guión 3: Pistas automáticas (después de 5 intentos sin adivinar)
(Grabación de audio: Sonido de una bocina de cine antigua)
Alexa: "¡Atención! Parece que los intentos no han dado resultado. Es el turno de Juan. Te daré una pista extra: el director de la película que intentas adivinar es Bong Joon-ho."
(Se repite un proceso similar para María después de su turno)
Alexa: (Usando una grabación de audio personalizable) "María, el tiempo se agota. La película que intentas adivinar tiene más de dos horas de duración."

- Guión 4: Adivinanza de la película
María: "Alexa, ¿la película es 'Parásitos'?"
Alexa: (Usando la API de TMDb para verificar el título y compararlo con la película de Juan) "¡Correcto! ¡Felicidades, María! ¡Has adivinado la película de Juan!"
(Grabación de audio: Música de victoria o aplausos)
Alexa: "Ahora, Juan, es tu turno. ¿Quieres seguir intentándolo?"

# ############################################################################################################################## #
# ------------------- DOCUMENTACION PROYECTO SKILL -------------------
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

# Que quiere el cliente
