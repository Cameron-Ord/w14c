<template>
    <div>

        <input class="email_input" type="value">
        <input class="pass_input" type="value">
        <button class="login" @click="user_login">Log-in</button>

 

        <p v-if="error_msg !== undefined">{{ error_msg }}</p>

    </div>
</template>

<script>
import axios from 'axios';
import Cookies from 'vue-cookies'
    export default {

        data() {
            return {

         
                error_msg: undefined,


            }
        },


        methods: {


            user_login(login_cookie){


                let pw_input = document.querySelector(`.pass_input`);

                let pw_input_value = pw_input[`value`];

                let em_input = document.querySelector(`.email_input`);
            
                let em_input_value = em_input[`value`];







                


                     axios({


                method: `POST`,

                url: `https://reqres.in/api/login`,

                data: {

                    email: em_input_value,

                    password: pw_input_value

                }


            }).then((response) =>{
                
                response;

                console.log(`API success`);
                
                this.$router.push(`/game`);

                login_cookie = `logged in`;

                Cookies.set(`login_token`, login_cookie);

                console.log(login_cookie);



            }).catch((error) =>{


               

                error;

                console.log(`API failure`);

                this.error_msg = `Invalid login`;

                Cookies.remove(`login_token`);
            




            });
            }



        },
        
        mounted(){

       
        }
    }
</script>

<style scoped>

</style>