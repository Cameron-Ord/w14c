<template>
    <div>

        <button @click="roll_dice">roll</button>

        <h1>{{ display_current_roll }}</h1>

        <p>Times lost:{{ loser_count }}</p>
        
        <p>Times won:{{ winner_count }}</p>

    </div>
</template>

<script>
import axios from 'axios';
import Cookies from 'vue-cookies';
    export default {
        


        data() {
            return {

                winner_count: 0,

                loser_count: 0,

                display_current_roll: undefined,

            }
        },

        methods:{

            roll_dice(){



               let roll_amount = Cookies.get(`roll`);

               console.log(roll_amount);

               this.display_current_roll = roll_amount;


               if(roll_amount >= 50){

                console.log(`winner`);

                this.winner_count += 1;

                Cookies.set(`win_count`, this.winner_count);

                console.log(this.winner_count);




               }else if(roll_amount <50){

                console.log(`loser`);

                this.loser_count += 1;

                Cookies.set(`lose_count`, this.loser_count);

                console.log(this.loser_count);


               }

               




                axios({


                    method: `GET`,

                    url: `http://www.randomnumberapi.com/api/v1.0/randomnumber`,



                }).then((response) =>{


                    response;

                    Cookies.set(`roll`, `${response[`data`][0]}`);

                    let login_status = Cookies.get(`login_token`);

                    let login_parse = JSON.parse(login_status);

                    console.log(login_parse);

                    if(login_parse === "logged in"){

                        console.log(`welcome`);

                    }else{

                        console.log(`screw you`);

                        this.$router.push(`/`);

                    }
                    
                    

      


                }).catch((error) =>{

                    console.log(error);

                });


            }


        },
    }
</script>

<style scoped>

</style>