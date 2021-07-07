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
                            <label for="" class="control-label col-sm-3">AREA_DEPENDE</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="AREA DEPENDE" id="AREA_DEPENDE" v-model="form.AREA_DEPENDE">
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
                      <button type="button" class="btn btn-primary" v-on:click="guardar()" >Guardar</button>
                      <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                    </div> 
                </form>
            </div>
        <!-- <Footer /> -->
    </div>
</template>
<script>
import Header from '@/components/Header.vue'
//import Footer from '@/components/Footer.vue'
import axios from 'axios';
export default {
    name:"Nuevo",
    data:function(){
        return {
            form:{
                "AREA" : "",
                "DESCRIPCION": "", 
                "AREA_DEPENDE":"",
                "NIVEL" :"",
                "TIPO_AREA" : "",
                "TITULAR" : ""
            }
        }
    },
    components:{
        Header,
        //Footer
    },
    methods:{
        guardar(){
            this.form.token = localStorage.getItem("token");
            axios.post("http://85.187.158.121/~victormanuelca/organigrama",this.form)
            .then(data =>{
                console.log(data);
                this.makeToast("Hecho","Organigrama creado","success");
                this.$router.push("/dashboard");
            }).catch( e =>{
                console.log(e);
                 this.makeToast("Error","Error al guardar","error");
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        makeToast(titulo,texto,tipo) {
            this.toastCount++
            this.$bvToast.toast(texto, {
            title: titulo,
            variant: tipo,
            autoHideDelay: 5000,
            appendToast: true
            })
        }   
    }
}
</script>
<style scoped>
.left{
    text-align:  left;
}
</style>