# tasks

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).

div
  h1 Manipulacion del DOM con Vue.js
  p Este ejercicio consiste en aprender a usar la funcionalidad de renderizado declaritivo que provee Vue.js
  p Para eso vamos a crear una pequeña aplicacion web que nos permita hacer seguimiento de tareas utilizando el local storage del Browser.
  p De esta manera vamos a reforzar los concepto mas basicos que nos ofrece Vue.js para manipular e interactuar con el DOM.

  h2 Ejercicios
  ol 
    li Crear dentro de data una propiedad "name" de tipo String y una propiedad tasks de tipo de Array.
    li Agregar una expresion para mostrar el valor de name y utilizar la directiva apropieda para para mostrar en una lista cada uno de los elementos dentro de task. Cada "task" es un objeto con una propiedad "title" y otra "time". Agregemos las expresiones necesarias para que en cada tarea podamos visualizar ambas propiedades.
    li Agregar funcionalidad para crear una nueva tarea:
      ol
        li Vamos a necesitar una nueva propiedad llamada "newTask" que sea un Object. Dentro de este objeto tambien agregamos una propiedad "tilte" de tipo String y una propiedad "time" de tipo Number. Recorda inicializar las propiedades con valores default.
        li Vamos a crear un metodo llamado "addTask" que agregue una nueva tarea al array "tasks". Una vez agregada tambien va a reiniciar los valores dentro de "newTaks". Ten en cuenta que antes de agregar la propiedad debemos chequear con los valores de "newTask.title" y "newTask.time" existan (sean distintos de "falsy"). Por otro lado es importante que cada elemento nuevo que agregemos al array de "tasks" sea un objeto nuevo y no la instancia de "newTask".
        li Vamos a agregar el HTML necesario, necesitamos dos "inputs" y un "button". Tambien debemos agregar las diretivas correspondientes para enlazar el codigo con la vista.
    li Creamos tambien una funcionalidad para cancelar, para eso debemos crear un metodo llamado "cancel" que simplemente reinicie los valores de las propiedades de newTask. Recordemos agregarun button de HTML donde enlazar este nuevo metodo
    li Es momento de saber cuantas horas llevamos trabajadas, para eso vamos a crear una computed property llamada "totalTime" donde se recorran todas las tareas y se calculo el total del tiempo trabajado. Tambien vamos agregar un elemento HTML con la expresion necesaria para visualizar la proopiedad.
    li Vamos a integrar la app con el local storage del browser. Dentro del metodo "addTask", vamos a guardar toda la lista de tareas en dicho storage usando este metodo: "localStorage.setItem('tasks', JSON.stringify(this.tasks))".
    li Guardando las tareas en el browser vamos a poder persistir la informacion aunque estemos cerrando o refrezcando la pagina. Debemos tambien al momento de crearse el componente, leer esta informacion para poder cargar la lista de tareas. Para eso dentro del hook "created", escribimos el siguiente codigo: "this.tasks = JSON.parse(localStorage.getItem('tasks')) || []"
    li Lo ultimo que nos queda es poder eliminar las tareas que ya no queremos. Para eso vamos a crear un metodo que se llame "removeTask". Este metodo debe recibir por parametro el indice de la tarea y podemos utilizar ese indice (en conjunto con el metodo "splice" de Array) para eliminar el elemento. Recordemos tambien que vamos a tener que agregar un boton por cada tarea y cada boton se encarga de llamar al metodo "removeTask" enviando por parametro el indice correspondiente. Recordemos invocar la funcionalidad que ya pusimos en "addTask", para actualizar el local storage del Browser.
    li Por ultimo vamos a mejorar la UI, cuando no haya tareas podemos mostrar un mensaje que indica que no hay ninguna tarea cargada y por otro lado ocultar el lista vacia
  
  hr
  #app
    h2 Administrador de Tareas
    h3 {{ name }}
    fieldset
      legend Nueva Tarea
      p
        input(type="text", placeholder="Titulo", v-model="newTask.title")
      p
        input(type="number", placeholder="Horas Trabajadas", v-model="newTask.time")
      p
        button(@click="addTask") Guardar
        button(@click="cancel") Cancelar
    div
      h3 Lista Tareas
      p(style="color: tomato", v-show="!tasks.length") Aun no hay tareas cargadas
      div(v-show="tasks.length")
        ol
          li(v-for="(t, i) in tasks") 
           span {{ t.title }} - {{ t.time }}
           span(@click="removeTask(i)") ❌
        hr
        p Tiempo Trabajado: 
          strong {{ totalTime }}
      
  