# p6-dsi

## Desarrollo pasos mínimos.

Para la práctica, se crearon 3 componentes: Win331Icon, Win311Window y Win311Error.

### Win331Icon

Win311Icon tiene un prop obligatorio que es type, dos methods y un computed.

La función switch focus modifica el state y este se activa cuando se activa el eventlistener añadido durante el montaje en el componente. Simplemente guarda en el estado el elemento activo.

La función getUrl simplemente obtiene la imagen correspondiente según el prop recibido.

La función computed isSelected simplemente comprueba el estado, a ver si es el propio elemento o no, que se llama desde el HTML utilizando v-bind:class.

### Win311Window

En esta se carga del fichero windows.json las ventanas definidas.

Solo recibe un prop y se da por válido siempre y cuando ese prop este dentro el fichero windows.json.

Tiene varias variables que se establecen con su valor en el momento en el que el componente está montado.

Por otra parte, a la hora de montar, se añade también un evento de dblclick que llama al metodo switchMsg.

Lo que hace este método simplemente es cambiar el valor de la variable footerMsg según el valor que se encuentre en el estado "focus".

Para cargar los iconos pertenecientes al componente, se utiliza la directa de vue de v-for.

### Deploy

Para hacer el deploy, solo tienes que añadir el fichero vue.config.js especificando que cuando vaya a hacer un build, añada el prefijo de la url que le pongas.

Una vez hecho esto, con gh-pages haces lo de siempre y se sube perfectamente (gh-pages -d dist).

## Retos

Los retos pedidos se resolvieron todos mediante gestión de estado, con Vuex.

Simplemente se define un objeto llamado store que va a actuar como una "variable global" que va a guardar los valores que tu quieras y va a tener una serie de funciones llamadas "mutations" que las puedes utilizar para definir la lógica que se va a seguir para modificar las variables que tengas.

Para nuestro caso, hay una mutation llamada switchFocus. Cada icono tiene un event listener de dbl click, por lo que cuando haces dblclick, llama a esta función y cambia el valor del focus y guarda el elemento que tiene el foco.

Así, como los iconos establecen el CSS con una función computed, cada vez que hay cambios en el estado comprueban si el elemento guardado es el mismo elemento que ellos. Si no es asi, no hacen nada y, si es asi, añaden el background azul.

Igual hace el objeto Window. Si la variable focus está vacía, muestra un mensaje predeterminado ("Selecciona una app para abrir") y si el focus tiene un elemento o cambia a un elemento, obtiene el prop name de ellos y añade el mensaje "X ha sido abierta". Esto es como reemplazo al console.log().

Finalmente, cuando haces 3 veces doble click, por alguna razón la práctica se corrompe. He buscado en stack overflow pero no sé que ocurre.
