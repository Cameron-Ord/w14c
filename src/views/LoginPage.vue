<template>
    <div>

        <input class="email_input" type="value">
        <input class="pass_input" type="value">
        <button class="login" @click="user_login">Log-in</button>

 
        <!--if error_msg is not undefined, it will display-->

        <p v-if="error_msg !== undefined">{{ error_msg }}</p>

    </div>
</template>

<script>
import axios from 'axios';
import Cookies from 'vue-cookies';
    export default {

        data() {
            return {

         
                error_msg: undefined,


            }
        },


        methods: {


            user_login(login_cookie){

                //creating the login input boxes//

                let pw_input = document.querySelector(`.pass_input`);

                //making pw_input_value and em_input_value equal the value typed into the input box..//

                let pw_input_value = pw_input[`value`];

                let em_input = document.querySelector(`.email_input`);
            
                let em_input_value = em_input[`value`];


                     axios({


                method: `POST`,

                url: `https://reqres.in/api/login`,

                data: {

                    //posting the values stored in the variables//

                    email: em_input_value,

                    password: pw_input_value

                }


            }).then((response) =>{
                
                //if API returns successfully, moves user to game page and creates a login token cookie containing json data//
                response;

                console.log(`API success`);

                this.$router.push(`/game`);

                login_cookie = "logged in";

                let login_json = JSON.stringify(login_cookie);

                Cookies.set(`login_token`, login_json);

                console.log(login_cookie);



            }).catch((error) =>{


                //if login fails, gives error_msg a string value, and removes any existing login cookies//
               

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