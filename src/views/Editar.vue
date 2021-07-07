<template>
        <div>
          <Header />
            <div class="container">
                <form action="" class="form-horizontal">
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">AREA</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="AREA" id="AREA" v-model="form.AREA">
                       </div>
                    </div>
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">DESCRIPCION</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="DESCRIPCION" id="DESCRIPCION" v-model="form.DESCRIPCION">
                       </div>
                    </div>
                    <div class="form-group left row">
                      <div class="col">
                            <label for="" class="control-label col-sm-3">AREA DEPENDE</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="AREA_DEPENDE" id="AREA_DEPENDE" v-model="form.AREA_DEPENDE">
                            </div>
                        </div>
                        <div class="col">
                          <label for="" class="control-label col-sm-5">NIVEL</label>
                          <div class="col-sm-7">
                              <input type="text" class="form-control" name="NIVEL" id="NIVEL" v-model="form.NIVEL">
                          </div>
                        </div> 
                    </div>
                    <div class="form-group left row">
                         <div class="col">
                            <label for="" class="control-label col-sm-2">TIPO AREA</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="TIPO_AREA" id="TIPO_AREA" v-model="form.TIPO_AREA">
                            </div>
                          </div>
                         <div class="col">
                              <label for="" class="control-label col-sm-2">TITULAR</label>
                              <div class="col-sm-7">
                                  <input type="text" class="form-control" name="TITULAR" id="TITULAR" v-model="form.TITULAR">
                              </div>
                        </div>
                    </div><br><br>
                    <div class="form-group">
                      <button type="button" class="btn btn-primary" v-on:click="editar()" >Editar</button>
                      <button type="button" class="btn btn-danger margen" v-on:click="eliminar()" >Eliminar</button>
                      <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                    </div> 
                </form>
            </div>
          <!-- <Footer />   -->
        </div>
</template>
<script>
import Header from '@/components/Header.vue';
//import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default {
    name:"Editar",
    components:{
        Header,
        //Footer
    },
    data:function(){
        return {
            form:{
            "ID_ORGANIGRAMA":"",
            "AREA" : "",
            "DESCRIPCION": "", 
            "AREA_DEPENDE":"",
            "NIVEL" :"",
            "TIPO_AREA" : "",
            "TITULAR" : ""
            }
        }
    },
    methods:{
        editar(){
            axios.put("http://85.187.158.121/~victormanuelca/organigrama",this.form)
            .then( data =>{
                console.log(data);
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        eliminar(){
            var enviar = {
                "ID_ORGANIGRAMA" : this.form.ID_ORGANIGRAMA,
                "token" : this.form.token
            };
            axios.delete("http://85.187.158.121/~victormanuelca/organigrama", { headers : enviar})
            .then( datos => {
                console.log(datos);
            this.$router.push("/dashboard");
            });
        }
    },
    mounted:function(){
        this.form.ID_ORGANIGRAMA = this.$route.params.id;
        axios.get("http://85.187.158.121/~victormanuelca/organigrama/"+ this.form.ID_ORGANIGRAMA)
        .then( datos => {
            this.form.AREA = datos.data[0].AREA;
            this.form.DESCRIPCION = datos.data[0].DESCRIPCION;
            this.form.dni = datos.data[0].DNI;
            this.form.AREA_DEPENDE = datos.data[0].AREA_DEPENDE;
            this.form.NIVEL = datos.data[0].NIVEL;
            this.form.TIPO_AREA = datos.data[0].TIPO_AREA;
            this.form.TITULAR = datos.data[0].TITULAR;
            this.form.fechaNacimiento = datos.data[0].FechaNacimiento;
            this.form.token = localStorage.getItem("token");
            console.log(this.form);
        })
    }  
}
</script>
<style scoped>
.left{
    text-align: left;
};
.margen{
    margin-left: 15px;
    margin-right: 15px;;
}
</style>