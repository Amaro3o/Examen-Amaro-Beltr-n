# Examen-Amaro-Beltran  
## Estereotipos de género  
**Amaro Beltrán**  

## Descripción  
Este proyecto busca exponer la problemática de género sobre los estereotipos de género y la expresión mediante una animación o sketch de p5.js.  
 
En la pantalla inicial se puede apreciar un fondo negro con un texto que introduce el tema a hablar, al dar click pasa a una segunda pantalla la cual muestra un fondo que va cambiando de color en escala de grises con un texto que lo acompaña hablando sobre el molde definido por los estereotipos de genero y dos imagenes que representan el molde de hombre y mujer en el que se debe encajar, finalmente en la ultima pantalla el fondo cambia en colores más vividos y empiezan a aparecer iconos de personas diveras las cuales muestran distintas formas de expresión de genero  

## Descripción conceptual  
El proyecto busca exponer conceptualmente los estereotipos de género desde una mirada emocional, sobre el cómo se siente estar bajo esa situación, mediante el uso de diversos elementos que relatan esa transición hasta finalmente ser capaz de darse cuenta y romper con esa estructura planteada por la sociedad.  
Cada elemento tiene su significado, partiendo por el color del background el cual es en tonos grises, dando una sensación de rigidez, frialdad y falta de emocionalidad y personalidad al no poder demostrarse como es realmente al igual que los elementos como el molde con figuras estereotipicas, los fondos de colores y iconos de personas con distintas formas, representan la diversidad y la libertad del entendimiento de que nadie encaja 100% dentro de esta estructura y hay diversas formas de expresar el genero y verse dependiendo de cada persona.  

La regla principal es la condicional if mouseIsPressed, ya que esta es la que cambia por completo el carácter del sketch cambiando de escenas y dando paso a este ambiente más diverso que se plantea en cuanto a romper con el molde o los estereotipos de género, tambien esta condicional representa la oposición a estos estereotipos.

## Input/Output  
Los datos que entran al sistema son las imagenes y variables declaradas para poder ejecutar las distintas etapas del sketch.  

Estos datos se procesan mediante el uso de distintas funciones como mousePressed, keyPressed, utilización de if-else if- else.  

Los datos que salen son los distintos estados del sketch los cuales muestran la pantalla de inicio, pantalla del molde (fondo gris) y pantalla final de colores de diversidad.  

## Referentes  
<img width="735" height="490" alt="What Is a Stereotype_" src="https://github.com/user-attachments/assets/4023986d-f64b-4a2d-93ab-cb1d79cc88a4" />  
ThoughtCo.  

<img width="735" height="730" alt="descarga" src="https://github.com/user-attachments/assets/7c054358-34af-4aca-bb19-bd61552b6b25" />  
Chloe Chapman Art en Pinterest  

**Diagrama de flujo**  
<img width="4086" height="5196" alt="Diagrama en blanco" src="https://github.com/user-attachments/assets/46cdde48-4ae5-4011-b5be-19ff3d97d914" />  


**Link**
[P5.js](https://editor.p5js.org/Amaro3o/sketches/tz0J1kmCr)  

**Código**  
```// Variables creadas
let estado = 0; //controla las fases del lienzo
let particulas = []; // crea array para las particulas
let imgHombre, imgMujer; //variable para guardar imagen moldes
let colorFondoGris = 120; // Almacena el valor numérico actual del color de fondo para la Fase 2

let imagenesParticulas = []; //array para almacenar imagenes de particulas

// Variables de apoyo para el diseño responsivo dinámico
let factorX, factorY; // Guardan la proporción de escala actual respecto al lienzo ideal de 1920x1080

function preload() {
  //funcion que carga las imagenes
  imgHombre = loadImage("/assets/moldehombre.png");
  imgMujer = loadImage("/assets/moldemujer.png");

  //Carga las 6 nuevas imágenes de personitas diversas en el array
  imagenesParticulas.push(loadImage("/assets/personitanaranja.png"));
  imagenesParticulas.push(loadImage("/assets/personitaverde.png"));
  imagenesParticulas.push(loadImage("/assets/personitamorada.png"));
  imagenesParticulas.push(loadImage("/assets/personitaazul.png"));
  imagenesParticulas.push(loadImage("/assets/personitaroja.png"));
  imagenesParticulas.push(loadImage("/assets/personitaamarilla.png"));
}
// Función de configuración inicial que se ejecuta una sola vez al arrancar el programa
function setup() {
  //Inicializa en 1920x1080 pero ajusta inmediatamente al formato real
  createCanvas(windowWidth, windowHeight); //// Crea el lienzo interactivo adaptándolo al tamaño completo de la ventana del navegador del usuario
  actualizarFactores(); // Llama a la función personalizada para establecer las relaciones de escala responsivas iniciales
}

function draw() {
  // Sentencias condicionales
  //// Estructura de control condicional que decide qué pantalla dibujar basándose en el valor de la variable 'estado'
  if (estado === 0) {
    // Si el estado es 0, renderiza la primera interfaz
    pantallaInicio();
  } else if (estado === 1) {
    // Si el estado es 1, salta a la segunda fase
    pantallaGris();
  } else {
    // Para cualquier otro valor (estado 2), activa la fase final de la lluvia
    pantallaLluviaRGB();
  }
  frameRate(60);
}

//Funciones propias definidas fuera de draw()

function pantallaInicio() {
  // Renderiza la pantalla inicial con fondo negro y textos de introducción
  background(0);
  fill(255); //color de texto blanco
  textAlign(CENTER, CENTER); //alinea textos en el centro

  // Texto (Multiplicado por factores responsivos para que no se corten)
  textSize(width * 0.03 > 45 ? 45 : width * 0.04); // Tamaño de fuente fluido, si el 3% del ancho de pantalla supera los 45px, congela el tamaño en 45; si no, lo encoge de forma fluida
  text("Estereotipos de Género: Rompiendo el Molde", width / 2, height * 0.4); // Dibuja el título en el centro horizontal y 40% de altura

  textSize(width * 0.015 > 24 ? 24 : width * 0.025); //si el 1.5% del ancho de pantalla supera los 24px, congela el tamaño en 24; si no, lo encoge de forma fluida
  text(
    "Tradicionalmente nos dividen en moldes... Haz CLICK para entrar al análisis.",
    width / 2,
    height * 0.52
  ); // Dibuja el título en el centro horizontal y 52% de altura
}
//segunda fase representa los estereotipos rigidos y sin libertad de expresion
function pantallaGris() {
  //renderiza la segunda pantalla
  // Función map() automática
  let oscilacion = sin(frameCount * 0.02); //genera un valor matemático oscilatorio continuo entre -1 y 1 basado en el tiempo del programa
  colorFondoGris = map(oscilacion, -1, 1, 30, 220); // Mapea matemáticamente el rango de la oscilación (-1 a 1) a un rango visible de escala de grises oscuros y claros (30 a 220)
  background(colorFondoGris); // Actualiza el color del fondo con el valor de grises calculado automáticamente

  fill(255); //rellena texto de color blanco
  textAlign(CENTER, CENTER); //alinea texto en el centro

  textSize(width * 0.025 > 40 ? 40 : width * 0.04); //si el 2.5% del ancho de pantalla supera los 40px, congela el tamaño en 40; si no, lo encoge de forma fluida
  text("Fase 2: La rigidez del molde", width / 2, height * 0.25); // Dibuja el título en el centro horizontal y 25% de altura

  textSize(width * 0.015 > 22 ? 22 : width * 0.025); //si el 1.5% del ancho de pantalla supera los 22px, congela el tamaño en 22; si no, lo encoge de forma fluida
  text("Haz CLICK de nuevo para oponerte al molde", width / 2, height * 0.3); // Dibuja el título en el centro horizontal y 30% de altura

  // Las imágenes se posicionan de manera fluida usando el ancho real (width)
  let tamImg = width * 0.4 > 300 ? 300 : width * 0.4; //Calcula el tamaño adaptativo de las imágenes para que ocupen el 40% del ancho, topado a un máximo de 300 píxeles
  image(imgHombre, width * 0.25 - tamImg / 2, height * 0.45, tamImg, tamImg); // Dibuja la primera imagen en el cuadrante izquierdo restando la mitad de su tamaño para centrarla perfectamente
  image(imgMujer, width * 0.75 - tamImg / 2, height * 0.45, tamImg, tamImg); // Dibuja la segunda imagen en el cuadrante derecho usando el mismo principio de centrado
}
// Controla la última fase que ejecuta la lluvia de imágenes simultáneas o particulas, expresa la diversidad de formas de expresion d egenero
function pantallaLluviaRGB() {
  //random() para fondo
  if (frameCount % 1 === 0) {
    // Modifica el fondo únicamente cada 1 fotograma
    background(random(80, 255), random(80, 255), random(80, 255)); // Sobrescribe el lienzo usando tres canales aleatorios (R, G, B) limitados a tonos entre (80 a 255)
  }

  fill(255); //rellena el texto de color blanco
  textAlign(CENTER, CENTER); //alinea texto al centro
  textSize(width * 0.03 > 45 ? 45 : width * 0.04); //si el 3% del ancho de pantalla supera los 45px, congela el tamaño en 45; si no, lo encoge de forma fluida
  text("Fase 3: Fluidez, Diversidad y Libertad", width / 2, height * 0.15); // Dibuja el título en el centro horizontal y 15% de altura
  textSize(18); //tamaño de letra 18
  text(
    "Presiona la barra espaciadora [SPACE] para hacer un RESET.",
    width / 2,
    height * 0.23
  ); // Dibuja el título en el centro horizontal y 23% de altura

  // Añadir partículas
  if (particulas.length < 60) {
    // Lógica de control de densidad: Mientras la lista tenga menos de 60 elementos activos
    particulas.push(new Particula()); // Instancia e introduce un nuevo objeto de la clase 'Particula' al array
  }

  // Bucle for
  for (let i = 0; i < particulas.length; i++) {
    // se repite el ciclo cuando i sea menor que la cantidad de particulas

    particulas[i].caer(); //hace que las particulas caigan

    particulas[i].mostrar(); //muestra las imagenes de las particulas de lluvia
  }
}

// Cambia dinámicamente el canvas al tamaño exacto de la ventana del navegador
function windowResized() {
  resizeCanvas(windowWidth, windowHeight); // Ajusta instantáneamente las dimensiones del lienzo a los nuevos límites
  actualizarFactores(); // Recalcula los factores de escala responsivos de apoyo
}

// Calcula la proporción actual contra la base de desarrollo (1920x1080)
function actualizarFactores() {
  factorX = width / 1920; // Proporción de escala en el eje horizontal
  factorY = height / 1080; // Proporción de escala en el eje vertical
}

function mousePressed() {
  //funcion que se activa al presionar el mouse
  if (estado === 0) {
    // Si está en inicio (0), avanza a la fase gris (1)
    estado = 1;
  } else if (estado === 1) {
    // Si está en la fase gris (1), avanza a la lluvia de colores (2)
    estado = 2;
  }
}

function keyPressed() {
  //funcion que se activa al presionar la tecla enter

  if (keyCode === ENTER) {
    // Comprueba si el código de la tecla presionada equivale a la tecla enter
    estado = 0; // Devuelve los estados a la pantalla de inicio (Fase 1)
    particulas = []; // Vacía por completo el array para eliminar de memoria los objetos clonados y reiniciar limpio
  }
}
// Definición de la plantilla (Clase) para controlar de forma individual cada elemento de la lluvia
class Particula {
  constructor() {
    //da las propiedades iniciales de cada particula

    this.x = random(width); //la partícula aparece en una posición aleatoria horizontal dentro de el ancho del canvas

    this.y = random(-600, 0); //la particula nace desde arriba, fuera de la pantalla y van entrando al lienzo

    this.velocidad = random(5, 6); //la partícula recibe una velocidad aleatoria entre 2 y 6

    this.tamaño = random(20, 80); //la partícula recibe un tamaño aleatorio entre los valores 20 y 80

    this.imagen = random(imagenesParticulas); //la partícula elige una imagen aleatoriamente
  }
  caer() {
    //hace que las particulas vayan hacia abajo

    this.y = this.y + this.velocidad; // hace que las imagenes avancen hacía abajo

    if (this.y > height + 60) {
      // si las imagenes llegan al final del lienzo caen nuevamente con valores diferentes

      this.y = random(-60, -20); // La imagen aparece nuevamente por encima del canvas

      this.x = random(width); // pone la imagen en una posición  aleatoria del ancho

      this.velocidad = random(5, 6); // Se asigna una velocidad aleatoria entre 2 y 6

      this.imagen = random(imagenesParticulas); // se genera una imagen al azar cada vez que la particula nace
    }
  }

  mostrar() {
    // dibuja las figuras

    image(this.imagen, this.x, this.y, this.tamaño, this.tamaño); //se le asignan los valores anteriores para la caida de las imagenes
  }
}```




