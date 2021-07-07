<template>
    <div>
        <Header/>
        <div class="container izquierda">
            <button class="btn btn-primary" v-on:click="nuevo()" >Nuevo organigrama</button>
                <br><br>
            <table class="table table-hover">
                <thead>
                    <tr>
                        <th scope="col">ID</th>
                        <th scope="col">AREA</th>
                        <th scope="col">DESCRIPCION</th>
                        <th scope="col">AREA_DEPENDE</th>
                        <th scope="col">NIVEL</th>
                        <th scope="col">TIPO_AREA</th>
                        <th scope="col">TITULAR</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="organigrama in Listaorganigramas" :key="organigrama.ID_ORGANIGRAMA" v-on:click="editar(organigrama.ID_ORGANIGRAMA)">
                        <th scope="row">{{ organigrama.ID_ORGANIGRAMA}}</th>
                        <td>{{ organigrama.AREA }}</td>
                        <td>{{ organigrama.DESCRIPCION }}</td>
                        <td>{{ organigrama.AREA_DEPENDE }}</td>
                        <td>{{ organigrama.NIVEL }}</td>
                        <td>{{ organigrama.TIPO_AREA }}</td>
                        <td>{{ organigrama.TITULAR }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
        <Footer/>
    </div>
</template>
<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default{
    name: "Dashboard",
    data(){
        return{
            Listaorganigramas:null,
            pagina:1
        }
    },
    components:{
        Header,
        Footer
    },
    methods:{
            editar(id){
                this.$router.push('/editar/' + id);
            },
            nuevo(){
                this.$router.push('/nuevo');
            }
    },
    mounted:function(){
        let direccion = "http://85.187.158.121/~victormanuelca/organigrama/?page=" + this.pagina;
        axios.get(direccion).then(data=> {
            this.Listaorganigramas = data.data;
        })
    }
}
</script>
<style scoped>
.izquierda{
        text-align: left;
    }
</style>