<template>
  <div class="padre">
    <div class="caja">
      <h3 :style="alerta === 'tarea guardada' ? ['background:green', 'color:white', 'padding:8px'] : ''">{{ alerta }}</h3>
      <h1>Agendador</h1>
      <input class="input" v-model="tareas" type="text" placeholder="Agenda tu tarea" />
      <input class="input" v-model="fecha" type="date" />
      <button @click="enviar()"><img src="./mas.png" alt="" /></button>
    </div>

    <div class="opciones">
      <button @click="ordenar()" class="ordenar">ordenar</button>
      <label class="container">
        <label class="alto">nivel alto:</label>
        <input :checked="prioridad === 'alto'" @change="prioridad = $event.target.checked ? 'alto' : 'baja'"
          v-model="prioridad" type="checkbox" />
        <div class="checkmark"></div>
      </label>
    </div>

    <table>
      <colgroup>
        <col style="width: 250px" />
        <col style="width: 250px" />
        <col style="width: 250px" />
        <col style="width:200px" />
      </colgroup>
      <thead>
        <tr>
          <td>tarea</td>
          <td>prioridad</td>
          <td>fecha de inicio</td>
          <td>opciones</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in datos" :key="index"
          :style="item.prioridad > 'alto' ? '' : ['background:red', 'color:white']">
          <td>{{ item.tareas }}</td>
          <td>{{ item.prioridad }}</td>
          <td>{{ item.fecha }}</td>
          <td>
            <button @click="eliminar(index)">❌</button>
            <button @click="editar(item,index)">📝</button>
          </td>
        </tr>
      </tbody>

    </table>
  </div>
</template>

<script setup>
import { ref } from "vue";
let tareas = ref("");
let fecha = ref("");
let prioridad = ref("baja");

let datos = ref([]);
let alerta = ref("");


function enviar() {
  if (tareas.value === "") {
    alerta.value = "Ingresa tu tarea";
    ocultar();
  } else if (fecha.value === "") {
    alerta.value = " ingresa fecha";
    ocultar();
  } else {
    datos.value.push({
      tareas: tareas.value,
      fecha: fecha.value,
      prioridad: prioridad.value,
    });
    alerta.value = "tarea guardada";
    ocultar()
    console.log(datos);
  }
}
function ocultar() {
  setTimeout(() => {
    alerta.value = "";
  }, 1500);
}

const ordenar = () => {
  datos.value.sort((a, b) => {
    return a.prioridad === 'alto' ? -1 : 1;
  });
  
}

const eliminar=(index)=>{
 datos.value.splice(index,1)
}

  const editar=(item,index)=>{
    console.log(item);
    console.log(index);
    nombre.value = item.nombre
    apellidos.value = item.apellidos

  }

</script>
<style scoped>
.caja {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100vh;
  height: auto;
  background-color: #ffa02e;
  padding: 20px;
  border-radius: 10px;
}

.padre {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.input {
  width: 80%;
  padding: 10px;
  margin: 8px;
}

img {
  width: 30px;
  /* padding: 5px; */
}

button {
  width: 15%;
}

table {
  text-align: center;
  background-color: #f07818;
  padding: 10px;

  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
  margin: 50px;
}

tbody {
  background-color: white;
  border: 2px solid black;
}

tbody tr td {
  border-radius: 50px solid;
}

/* Hide the default checkbox */
.container input {
  display: none;
}

.container {
  display: flex;
  position: relative;
  cursor: pointer;
  font-size: 20px;
  user-select: none;
  -webkit-tap-highlight-color: transparent;
  margin: 2px;
}

.checkmark {
  position: relative;
  top: 0;
  left: 0;
  height: 1.3em;
  width: 1.3em;
  background-color: #2196f300;
  border-radius: 0.25em;
  transition: all 0.25s;
}

.container input:checked~.checkmark {
  background-color: #2196f3;
}

.checkmark:after {
  content: "";
  position: absolute;
  transform: rotate(0deg);
  border: 0.1em solid black;
  left: 0;
  top: 0;
  width: 1.05em;
  height: 1.05em;
  border-radius: 0.25em;
  transition: all 0.25s, border-width 0.1s;
}

.container input:checked~.checkmark:after {
  left: 0.45em;
  top: 0.25em;
  width: 0.25em;
  height: 0.5em;
  border-color: #fff0 white white #fff0;
  border-width: 0 0.15em 0.15em 0;
  border-radius: 0em;
  transform: rotate(45deg);
}

.opciones {
  display: flex;
  justify-content: space-around;

  width: 20%;
  padding: 10px;
  background-color: gray;
  border: 2px solid;
  margin: 30px;
  border-radius: 10px;
}

.alto {
  color: white;
}

.ordenar {
  background-color: white;
  border-radius: 10px;
  padding: 8px;
  width: 80px;
  text-align: center;
}

h3 {
  width: 400px;
  background: red;
  text-align: center;
  color: white;

}
</style> 

 












<!-- <template>
  <div id="padre">
    <h1>{{ parseInt(num) / parseInt(num2==0?1:num2) }}</h1>
    <input type="text" placeholder="Telefono..." v-model.trim="num">
    <input type="text" placeholder="Telefono..." v-model="num2"> 

      <h1>{{ contador }}</h1>
    <button @click="contar()">Cambiar</button>
    <h2 v-if="contador<21">Hola soy el msj q van a desaparecer</h2>
    <h2 v-else>hola yo voy aparecer</h2>
    <h2 > {{contador<21?"Hola soy el msj q van a desaparecer":"hola yo voy aparecer"}}</h2>

    <h3 :style="alerta === 'Formulario enviado correctamente' ? 'color:green' : ''">{{ alerta }}</h3>
    <h1>Formulario</h1>
    <form>
      <label for="nombre">Nombre:</label>
      <input type="text" id="nombre" name="nombre" v-model="nombre">
      <label for="apellidos">Apellidos:</label>
      <input type="text" id="apellidos" name="apellidos" v-model="apellidos">
      <label for="tipo_documento">Tipo documento:</label>
      <select id="tipo_documento" name="tipo_documento" v-model="tipo_documento">
        <option value="cedula">Cédula</option>
        <option value="tarjeta_identidad">Tarjeta de identidad</option>
        <option value="pasaporte">Pasaporte</option>
      </select>
      <label for="numero_documento">Número de documento:</label>
      <input type="text" id="numero_documento" name="numero_documento" v-model="numero_documento">
      <label for="genero">Genero:</label>
      <select id="genero" name="genero" v-model="genero">
        <option value="masculino">Masculino</option>
        <option value="femenino">Femenino</option>
        <option value="otro">Otro</option>
      </select>
      <label for="correo">Correo:</label>
      <input type="email" id="correo" name="correo" v-model="correo">
      <label for="telefono">Teléfono:</label>
      <input type="text" id="telefono" name="telefono" v-model="telefono">
      <label for="fecha_nacimiento">Fecha de nacimiento:</label>
      <input type="date" id="fecha_nacimiento" name="fecha_nacimiento" v-model="fecha_nacimiento">
      <label for="telefono">Edad:</label>
      <input type="number" id="telefono" name="telefono" v-model="edad1">
    </form>
    <button @click="validar()">enviar</button>

    <table>
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Apellido</th>
          <th>Tipo de documento</th>
          <th>Numero de documento</th>
          <th>Telefono</th>
          <th>Correo</th>
          <th>Genero</th>
          <th>Fecha de nacimiento</th>
          <th>edad</th>
          <th>Opciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, i) in registros" :key="i"
          :style="item.edad > 17 ? [' background:red', 'color:white'] : 'color:purple'">
          <td>{{ item.nombre }}</td>
          <td>{{ item.apellidos }}</td>
          <td>{{ item.tipo_documento }}</td>
          <td>{{ item.numero_documento }}</td>
          <td>{{ item.telefono }}</td>
          <td>{{ item.correo }}</td>
          <td>{{ item.genero }}</td>
          <td>{{ item.fecha_nacimiento }}</td>
          <td>{{ item.edad }}</td>
          <td>
            <button @click="eliminar(i)">❌</button>
            <button @click="editar(item, i)">📝</button>
          </td>
        </tr>

      </tbody>

    </table>

   <img :src="image" alt="" :style="{borderRadius:num}"> 
     <h1 :style="{borderRadius:12}">hola a todos</h1> 
   <h1 :style="num>18?'color:salmon':'color:green'">mi edad es {{ num }}</h1> 

  </div>
</template>

<script setup>
import { ref } from "vue"
let num = ref(19)
let color = ref("yellow")
let image = ref("https://adrianalonso.es/wp-content/uploads/2018/01/vue.jpg")

const registros = ref([{
  nombre: "jose",
  apellidos: "HOla",
  tipo_documento: "CC",
  numero_documento: "123123123",
  telefono: "123123213",
  correo: "asdas",
  genero: "m",
  fecha_nacimiento: "12312",
  edad: "12"
},
{
  nombre: "jmiguel",
  apellidos: "HOla",
  tipo_documento: "CC",
  numero_documento: "123123123",
  telefono: "123123213",
  correo: "asdas",
  genero: "m",
  fecha_nacimiento: "12312",
  edad: "12"
},
{
  nombre: "cvcijiase",
  apellidos: "HOla",
  tipo_documento: "CC",
  numero_documento: "123123123",
  telefono: "123123213",
  correo: "asdas",
  genero: "m",
  fecha_nacimiento: "12312",
  edad: "12"
},
{
  nombre: "jadasdnsae",
  apellidos: "HOla",
  tipo_documento: "CC",
  numero_documento: "123123123",
  telefono: "123123213",
  correo: "asdas",
  genero: "m",
  fecha_nacimiento: "12312",
  edad: "12"
}])
let bd = ref(true)
const nombre = ref("")
const apellidos = ref("")
const tipo_documento = ref("")
const numero_documento = ref("")
const genero = ref("")
const correo = ref("")
const telefono = ref("")
const fecha_nacimiento = ref("")
const edad1 = ref(0)
let alerta = ref("")
let index=null

function eliminar(i) {
  registros.value.splice(i, 1)
}

function editar(item, i) {
  bd.value=false
  index=i
  console.log(item);
  console.log(i);
  nombre.value = item.nombre
  apellidos.value = item.apellidos
  tipo_documento.value = item.tipo_documento
  numero_documento.value = item.numero_documento
  genero.value = item.genero
  correo.value = item.correo
  telefono.value = item.telefono
  fecha_nacimiento.value = item.fecha_nacimiento
  edad1.value = item.edad1

}

function ocultarAlerta() {
  setTimeout(() => {
    alerta.value = "";
  }, 3500)
}


const validar = () => {
  if (bd.value == true) {
    if (nombre.value === "") {
      alerta.value = "El campo nombre no puede estar vacio"
      ocultarAlerta()
    }
    else if (apellidos.value === "") {
      alerta.value = "El campo apellidos no puede estar vacio"
      ocultarAlerta()
    }
    else if (tipo_documento.value === "") {
      alerta.value = "El campo tipo de documento no puede estar vacio"
      ocultarAlerta()
    }
    else if (numero_documento.value === "") {
      alerta.value = "El campo número de documento no puede estar vacio"
      ocultarAlerta()
    }
    else if (isNaN(numero_documento.value)) {
      alerta.value = "El campo número de documento solo puede contener números"
      ocultarAlerta()
    }
    else if (genero.value === "") {
      alerta.value = "El campo genero no puede estar vacio"
      ocultarAlerta()
    }
    else if (correo.value === "") {
      alerta.value = "El campo correo no puede estar vacio"
      ocultarAlerta()
    }
    else if (!correo.value.includes("@")) {
      alerta.value = "El campo correo debe ser un correo valido"
      ocultarAlerta()
    }
    else if (telefono.value === "") {
      alerta.value = "El campo teléfono no puede estar vacio"
      ocultarAlerta()
    }
    else if (telefono.value.length < 10) {
      alerta.value = "El campo teléfono debe tener al menos 10 números"
      ocultarAlerta()
    }
    else if (fecha_nacimiento.value === "") {
      alerta.value = "El campo fecha de nacimiento no puede estar vacio"
      ocultarAlerta()
    }
    else {
      const fecha = new Date();
      const fechaActual = fecha.toISOString().split('T')[0];
      let edad = fechaActual.split("-")[0] - fecha_nacimiento.value.split("-")[0];
      if (fechaActual.split("-")[1] < fecha_nacimiento.value.split("-")[1]) {
        edad--;
      }
      if (edad < 18) {
        alerta.value = "Debe ser mayor de 18 años para registrarse";
        ocultarAlerta()
      } else {
        alerta.value = "Formulario enviado correctamente"
        ocultarAlerta()
        registros.value.push({
          nombre: nombre.value,
          apellidos: apellidos.value,
          tipo_documento: tipo_documento.value,
          numero_documento: numero_documento.value,
          genero: genero.value,
          correo: correo.value,
          telefono: telefono.value,
          fecha_nacimiento: fecha_nacimiento.value,
          edad: edad1.value
        })
        console.log(registros.value)
        nombre.value = ""
        apellidos.value = ""
        tipo_documento.value = ""
        numero_documento.value = ""
        genero.value = ""
        correo.value = ""
        telefono.value = ""
        fecha_nacimiento.value = ""
        edad1.value = 0
      }
    }
  }else{
      registros.value[index].nombre=nombre.value
      registros.value[index].apellidos=apellidos.value
      registros.value[index].tipo_documento=tipo_documento.value
      registros.value[index].numero_documento=numero_documento.value
      registros.value[index].genero=genero.value
      registros.value[index].correo=correo.value
      registros.value[index].telefono=telefono.value
      registros.value[index].fecha_nacimiento=fecha_nacimiento.value
      registros.value[index].edad=edad1.value
      bd.value=true

  }

}





 let contador=ref(0)
function contar(){
  contador.value+=1
} 


// let num =ref(0)
// let num2 =ref(0)
// let telefono = ref("312446579")
telefono.value="345"
// let nombre = ref("Contreras")
nombre.value = telefono.value 

</script>

<style scoped>
h3 {
  color: red;
}

#padre {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  padding: 10px;
}

th,
tr,
td {
  border: 2px solid blue;
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  width: 80%;
  margin-bottom: 20px;
  background-color: #5a007d;
  padding: 10px;
  color: white;
  padding: 30px;
}

input {
  width: 100%;
}

select {
  width: 100%;
  padding: 2px;
}</style>  -->