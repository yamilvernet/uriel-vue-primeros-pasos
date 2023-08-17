<!--<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>-->

<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <h1 class="">Visor de empleades</h1>
        <div>
          Cantidad de empleados activos: 
          <div class="badge bg-secondary" v-if="empleados_activos!=null">{{empleados_activos.length}}</div>
          <div class="badge bg-secondary" v-else>
            <div class="spinner-grow spinner-grow-sm text-light" role="status">
            </div>
          </div>
        </div>

        <small class="w-100" v-if="empleados_inactivos!=null">
          Existen {{empleados_inactivos.length}} empleados inactivos <a href="">Ver</a>
        </small>

        <ul class="list-group">
            <LiEmpleado :empleado="empleado" v-for="(empleado,dni) in empleados_activos" :key="dni"/>
        </ul>

      </div>

      
    </div>
  </div>


  <header>

    <!-- <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" /> -->

    
      

      <!-- <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav> -->
  </header>

  <!-- <RouterView /> -->
</template>

<script>
import LiEmpleado from "@/components/LiEmpleado.vue";
export default {
  components:{LiEmpleado},
  data(){
    return {
      // empleados:null,
      empleados_activos: null,
      empleados_inactivos: null
    }
  },

  mounted(){
    fetch('https://apprrhh-707b9.firebaseio.com/personal_cat.json').then((r)=>r.json()).then((data)=>{
      // this.empleados = data

      // empleados = temp0

      Object.keys(data).forEach((dni)=>{
        let empleado = data[dni]
        // Comprobamos si el empleado sigue trabajando
        if(empleado.leg_fecegr == undefined){
          if(this.empleados_activos==null) this.empleados_activos = []

          this.empleados_activos.push(empleado)
        } else {
          // El empleado tiene fecha de egresdo, fue dado de baja
          if(this.empleados_inactivos==null) this.empleados_inactivos = []
          
          this.empleados_inactivos.push(empleado)
        }
      })


    }).catch((e)=>console.error('Hubo un error',e))
  }

}

</script>

<style scoped>
</style>