<template>
    <div>

        <input class="email_input" type="value">
        <input class="pass_input" type="value">
        <button class="login" @click="user_login">Log-in</button>

        <router-link to="/game">GAME</router-link>

        <p v-if="error_msg !== undefined">{{ error_msg }}</p>

    </div>
</template>

<script>
import axios from 'axios';

    export default {

        data() {
            return {
              

                error_msg: undefined,
            }
        },


        methods: {


            user_login(){


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

                console.log(`API success`);
                
                console.log(response);

                this.$router.push(`/game`);


            }).catch((error) =>{


                console.log(`API failure`);
                console.log(error);

                this.error_msg = `API failure`;

            


            });
            }



        },
        
        mounted(){

       
        }
    }
</script>

<style scoped>

</style>