<template>
  <div class="container">
        <div class="card o-hidden border-0 shadow-lg my-5">
            <div class="card-body p-0">
                <div class="row">
                    <div class="col-lg-5 d-none d-lg-block bg-primary">
                        <div class="col mx-auto text-center">
                            <br>
                            <img src="../assets/Logo.png" id="logo">
                        </div>
                    </div>
                    <div class="col-lg-7">
                        <div class="p-5">
                            <div class="text-center">
                                <h1 class="h4 text-gray-900 mb-4">Seja bem vindo!</h1>
                            </div>
                            <hr>

                            
                                <!-- Login -->
                                <div>
                                   
                                    <div class="form-group left-inner-addon">
                                        <i class="fa fa-user"></i>
                                        <input 
                                            type="text" 
                                            id="usuario" 
                                            name="usuario"
                                            v-model="usuario"
                                            class="form-control" 
                                            placeholder="Digite seu Login" 
                                            required>
                                    </div>
                                    <!-- Senha -->
                                    <div class="form-group left-inner-addon">
                                        <i class="fas fa-lock"></i>
                                        <input 
                                            type="password" 
                                            id="senha" 
                                            name="senha"
                                            v-model="senha"
                                            class="form-control"
                                            placeholder="Digite sua senha" 
                                            required>
                                    </div>

                                    <button type="submit" class="btn btn-primary btn-lg btn-block" @click="logar()">Entrar</button>

                                    <hr>

                                    <div class="text-center">
                                        <a class="small text-primary">Verifique seu agendamento</a>
                                    </div>

                                    <footer>
                                        <p class="mt-5 mb-3 text-muted text-center">AgendeConsulta &copy; 2021</p>
                                    </footer>
                                </div>
                            
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
   
data() {
    return {
            nome: "",
            usuario: "",
            senha: "",
            usuarios: [],
            usuarioArray: [],
            baseURI:"http://localhost:3000/usuarios",
            baseLogin: "http://localhost:3000/usuarios/login"  
    }
},
    methods:{
        logar() {
            axios.post(this.baseLogin,
            {
                usuario: this.usuario,
                senha: this.senha,
            },
            { 
                withCredentials: true 
            }).then((result) => {
          
            let userId = this.getCookie("userId");
            
            if (userId) {
                localStorage.setItem("user", JSON.stringify(result.data));
            }
            
            this.$router.replace('pagina-inicial')
            //this.$router.go();
            });
        },

        getCookie(name) {
            let match = document.cookie.match(new RegExp(name + "=([^;]+)"));
            if (match) return match[1];
            return;
        },
    },
}
</script>

<style>
.botoes{
    width: 400px;
    position: relative;
    left: 35%;
}

.line {
    display: inline-block;
}

.bt{
    width: 100px;
}

.ml-2{
    text-align: center;
}

.left-inner-addon {
    position: relative;
}
.left-inner-addon i {
    position: absolute;
    padding: 10px 12px;
    pointer-events: none;
    /*color: ;*/
}
.left-inner-addon input.form-control {
    padding-left: 30px;
}

input[type="date"]:before {
    content: attr(placeholder) !important;
    color: #666;
    margin-right: 0.5em;
}

input[type="date"]:focus:before,
input[type="date"]:valid:before {
    content: "";
}

#register-image{
    background-color: #023e8a;
    background-position:center;
    background-size:cover;
}

#logo {
    width: 100%;
}

.img-arredondada {
    border-radius: 50%;
    background-position: -15px -15px;
    height: 195px;
    width: 195px;
    background-image: url(../assets/Avatar.png);
}

</style>