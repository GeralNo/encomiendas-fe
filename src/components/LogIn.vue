<template>
    <div class="logIn_user">
        <div class="container_logIn_user">
            <h2>Iniciar Sesión</h2>

            <form v-on:submit.prevent="processLogInUser" >
                <input type="text" v-model="user.username" placeholder="Usuario">
                <br>
                <input type="password" v-model="user.password" placeholder="Contraseña">
                <br>
                <button type="submit">Iniciar Sesión</button>
            </form>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "LogIn",
    data: function(){
        return {
            user: {
                username:"",
                password:""
            }
        }   
    },

    methods: {
        processLogInUser: function(){
            axios
            .post("https://group1proyect-be.herokuapp.com/login/", this.user,{
                headers: {},
            })
            .then((result) => {
                let dataLogIn = {
                    username: this.user.username,
                    token_access: result.data.access,
                    token_refresh: result.data.refresh,
                    };
                    this.$emit('completedLogIn', dataLogIn);
                })
                .catch((error) => {

                    if (error.response.status == "401")
                        alert("ERROR 401: Credenciales Incorrectas.");
                });
            }
        }
    }
</script>

<style>

.logIn_user{
    margin-top: 0;
    padding: 0%;
    height: 100%;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

.container_logIn_user {
    border: 1px solid #bfbfbf;
    border-radius: 25px;
    width: 25%;
    height: 50%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: -2rem;
    margin-bottom: -4rem;
}

.logIn_user h2{
    color: #00000;
}

.logIn_user form{
    width: 70%;
}

.logIn_user input {
    height: 40px;
    width: 100%;
    box-sizing: border-box;
    padding: 10px 20px;
    margin: 5px 0;
    border-radius: 25px;
    border: 1px solid #bfbfbf;
    color: #00000;
}

form input:focus {
    border: 1px solid #E5E7E9;
}

.logIn_user button {
    width: 100%;
    height: 40px;
    color: #E5E7E9;
    background: #5372F0;
    border: 1px solid #E5E7E9;
    border-radius: 25px;
    padding: 10px 25px;
    margin: 5px 0;
}

.logIn_user button:hover {
    color: #E5E7E9;
    background: #2c52ed;
    border: 1px solid #E5E7E9;
}

</style>