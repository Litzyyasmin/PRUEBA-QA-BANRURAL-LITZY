<!-- LITZY YASMIN MEJIA AGUILAR, EVALUACION TESTER I  -->
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">

    <title>Juego de adivina tu número</title>

    <style>
      html {
        font-family: sans-serif;
      }
      body {
        width: 50%;
        max-width: 800px;
        min-width: 480px;
        margin: 0 auto;
      }
      <!-- AGREGUE ESTA FUNCION .form input[type="number"] {
        width: 200px;
        } -->

      .lastResult {
        color: white;
        padding: 3px;
      }
    </style>
  </head>

  <body>
      <h1>Juego Adivina tu número</h1>

      <p>Hemos seleccionado un número aleatorío entre 1 a 100. Trata de adivinar el número, en un total de 10 turnos o menos. No te preocupes, te diremos sí el número es más alto o más bajo </p>

<div class="form">
  <label for="guessField">Ingresa el número a adivinar: </label>
  <!-- AGREGAR: Se agrego a la funcion el tipo numero en vez del tipo texto y se declaro que el numero minimo es 1 y maximo 100, Para que se de la opcion de ingresar numeros enteros y no caracteres, esto nos ahorra lineas de codigo, y tiempo ya que el juego solo nos pide numeros enteros nos ahorra la programacion para el numero de intento asi mismo para la alerta en mensaje <input type="number" min ="1" max="100" required id="guessField" class="guessField"> -->
  <input type="text" id="guessField" class="guessField">

  <!--  /*ERROR: Cambie el mensaje de "ingresar el numero aleatorio" a enviar respuesta, <input type="submit" value="Ingresar el numero aleatorio" class="guessSubmit"> porque entre los requisitos del programa y las instrucciones dadas no mencionaba agregar numeros aleatoriamente/*-->
  <input type="submit" value="Enviar respuesta" class="guessSubmit"> 

</div>

<div class="resultParas">
  <p class="guesses"></p>
  <p class="lastResult"></p>
  <p class="lowOrHi"></p>
</div>

<!-- ERROR: SE ELIMINO ESTE BODY Y SE COLOCO AL FINAL DEL PROGRAMA -->
</body>

<script>

  /*ERROR: SE AGREGO LA FUNCION let randomNumber = Math.floor(Math.random() * 100) +1; para que el Math.floor me devuelva el maximo entero menor o igual al numero y lo agregue *100 ya que entre los requisitos indica un numero del 1 al 100 y en el codigo brindado decía 10 y agregue el +1 luego del parentesis para que me cuente hasta el numero 100*/
  let randomNumber = Math.random() * 10;

  // ERROR: SE ELIMINO ESTA CONSTANTE QUE NO IBA A SER FUNCIONAL PARA EL PROYECTO//
  const ATTEMPS = 5;

  const guesses = document.querySelector('.guesses');
  const lastResult = document.querySelector('.lastResult');
  const lowOrHi = document.querySelector('lowOrHi');

  const guessSubmit = document.querySelector('.guessSubmit');
  const guessField = document.querySelector('.guessField');

  let guessCount = 1;
  let resetButton;

  //Agregue esta funcion para que el cursos se posicione en la casilla cuando el juego inicie//
  guessField.focus();

  function checkGuess() {

    // ERROR: Agregue el const userGuess = Number(guessField.value); adicione el number afuera de la funcion a evaluar//
    let userGuess = guessField.value;

    if(guessCount === 1) {
      
      // ERROR: Agregue el siguiente texto guesses.textContent = 'Numeros de Intentos anteriores: //
      guesses.textContent = 'Número aleatorio anterior: ';
    }
    guesses.textContent += userGuess + ' ';

    if(userGuess === randomNumber) {

      // ERROR: Se hizo la modificacion de la linea, para que cuando adivine el usuario el numero antes de los 10 intentos me muestre el mensaje de felicitaciones lastResult.textContent = 'Felicitaciones! adivinaste el número!'; //
      lastResult.textContent = '!!!Pérdistes!!!';

      // ERROR: Se hizo la modificacion del color negro a color verde a la hora de ganar  lastResult.style.backgroundColor = 'green';//
      lastResult.style.backgroundColor = 'black';

      lowOrHi.textContent = '';
      setGameOver();

      //ERROR: se modifico esta funcion, porque arriba elimine la constante ya que no me serviria, y le coloque el numero de intentos que tiene si se pasa de esos 10 intentos sin adivinar esta funcion me servira para leerlo en este caso una igualdad estricta "else if(guessCount === 10) {"//
    } else if(guessCount === ATTEMPS) {

      // ERROR: Se mofidico el texto para que me muestre en pantalla el mensaje de perdistes por si no adivina el numero en los 10 intentos que tiene lastResult.textContent = '!!!Pérdistes!!!';//
      lastResult.textContent = 'Felicitaciones! adivinaste el número!';

      lastResult.style.backgroundColor = 'red';
      //ERROR: Se agrego esta linea con la funcion lowOrHi.textContent = '';
      setGameOver();
    } else {
      lastResult.textContent = 'Incorrecto! ';

      // ERROR: Se cambio el color a negro como se solicita cuando el numero es incorrecto lastResult.style.backgroundColor = 'black';//
      lastResult.style.backgroundColor = 'green';


      if(userGuess < randomNumber) {
        lowOrHi.textContent = 'El número es mayor!';
      } else if(userGuess > randomNumber) {
        lowOrHi.textContent = 'El número es menor!';
      }
    }

    guessCount++;
    guessField.value = '';
    guessField.focus();
  }
  guessSubmit.addEventListener('click', checkGuess);

  function setGameOver() {
	  guessField.disabled = true;
	  guessSubmit.disabled = true;
	  resetButton = document.createElement('button');
	  resetButton.textContent = 'Comienza un nuevo juego';
	  document.body.appendChild(resetButton);
	  resetButton.addeventListener('click', resetGame);
  }

  function resetGame() {
	  guessCount = 1;

	  const resetParas = document.querySelectorAll('.resultParas p');
    //MODIFICACIÓN: Modifique la funcion for  for (const resetPara of resetParas) { por una constante
	  for(let i = 0; i < resetParas.length; i++) {
		  resetParas[i].textContent = '';
	  }

	  resetButton.parentNode.removeChild(resetButton);
	  guessField.disabled = false;
	  guessSubmit.disabled = false;
	  guessField.value = '';
	  guessField.focus();
	  lastResult.style.backgroundColor = 'white';
    
    //ERROR: Se modifico el numero *100 +1 como se especifico en  la funcion de arriba para que pueda leerme los numeros enteros y se coloca el +1 para que tome en cuenta el numero 100 ya que sino lo hacemos solo cuenta hasta el 99 randomNumber = Math.floor(Math.random() * 100) + 1;
	  randomNumber = Math.floor(Math.random()) + 1;
    }
</script>
</body>
</html>
