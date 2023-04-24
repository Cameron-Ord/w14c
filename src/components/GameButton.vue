<template>
    <div>

        <button @click="call_api">Roll</button>


        <button @click="logout_button">logout</button>

    </div>
</template>

<script>
import axios from 'axios';
import Cookies from 'vue-cookies';
    export default {
        
        data() {
            return {

                win_count_obj: 0,

                lose_count_obj: 0,

            }
        },
   
        methods:{


            logout_button(){


                Cookies.remove(`login_token`);

                this.$router.push(`/`);

            },


            roll(){


               let roll_amount = Cookies.get(`roll`);

               this.$root.$emit(`roll_display`, roll_amount);

               console.log(roll_amount);

               if(roll_amount >= 50){

                this.win_count_obj +=1

                this.$root.$emit(`win_display`, this.win_count_obj);


               }else if(roll_amount <50){



                console.log(`loser`);

                this.lose_count_obj +=1;

                this.$root.$emit(`loss_display`, this.lose_count_obj);


               }

               

            },


            call_api(){



                axios({


                    method: `GET`,

                    url: `http://www.randomnumberapi.com/api/v1.0/randomnumber`,



                }).then((response) =>{


                    response;

        

                    Cookies.set(`roll`, `${response[`data`][0]}`);

                    this.roll();
                    

      


                }).catch((error) =>{


                    error;

                    console.log(`api failure`);

                });

            },
   

            
        }
   

   }
</script>

<style scoped>

</style>