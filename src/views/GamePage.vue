<template>
    <div>

        <button @click="roll_dice">roll</button>

        <h1>{{ display_current_roll }}</h1>

    </div>
</template>

<script>
import axios from 'axios';
import Cookies from 'vue-cookies';
    export default {
        


        data() {
            return {

                display_current_roll: undefined,

            }
        },

        methods:{

            roll_dice(){



               let roll_amount = Cookies.get(`roll`);


               this.display_current_roll = roll_amount;





                axios({


                    method: `GET`,

                    url: `http://www.randomnumberapi.com/api/v1.0/randomnumber`,



                }).then((response) =>{


                    console.log(response);

                    Cookies.set(`roll`, `${response[`data`][0]}`);



                }).catch((error) =>{

                    console.log(error);

                });


            }


        },
    }
</script>

<style scoped>

</style>