<template>
    <li class="list-group-item">
        DNI:
        {{empleado.leg_numdoc}}

        {{mayusculas(empleado.leg_apellido)}} {{mayusculas(empleado.leg_nombre)}}

        <!-- <button class="btn btn-primary" @click="manejar_mostrar()" >Ver más</button> -->
        <button class="btn btn-primary" @click="mostrar=!mostrar" >Ver más</button>

        


        <!-- <p>
            <button class="btn btn-primary" type="button" data-bs-toggle="collapse" :data-bs-target="'#collapse_'+empleado.leg_numdoc" aria-expanded="false" :aria-controls="'collapse_'+empleado.leg_numdoc">
                Button with data-bs-target
            </button>
            </p>
            <div class="collapse" :id="'collapse_'+empleado.leg_numdoc">
            <div class="card card-body">
                Some placeholder content for the collapse component. This panel is hidden by default but revealed when the user activates the relevant trigger.
            </div>
        </div> -->

        <div v-show="mostrar">
            <a :href="'tel:+549'+empleado.leg_celular">{{empleado.leg_celular}}</a>
            <a :href="'mailto:'+empleado.leg_mail">{{empleado.leg_mail}}</a>
        </div>
    </li>
</template>

<script>
export default {
    data(){
        return {
            mostrar:false
        }
    },


    props:{
        empleado:Object
    },

    methods:{
        // manejar_mostrar(){
        //     if(this.mostrar){
        //         this.mostrar=false
        //     } else {
        //         this.mostrar = true
        //     }
        // },

        mayusculas(cadena) {
            var palabras = cadena.toLowerCase().split(' ');
            for (var i = 0; i < palabras.length; i++) {
                palabras[i] = palabras[i].charAt(0).toUpperCase() + palabras[i].slice(1);
            }
            return palabras.join(' ');
        }
    }

}
</script>

<style>

</style>