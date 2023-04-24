<template>
    <div>
        <h1>{{ welcome_user }}</h1>

        <button @click="roll_dice">roll</button>

        <h1>{{ display_current_roll }}</h1>

        <p>Times lost:{{ display_losses }}</p>
        
        <p>Times won:{{ display_wins }}</p>

        <button @click="logout_button">logout</button>

    </div>
</template>

<script>
import axios from 'axios';
import Cookies from 'vue-cookies';
    export default {
        


        data() {
            return {

                welcome_user: undefined,

                display_current_roll: undefined,

                win_count_obj: 0,

                lose_count_obj: 0,

                display_wins: undefined,

                display_losses: undefined

            }
        },

        methods:{

            updatescoreboard(){
                

                this.display_wins = Cookies.get(`win_count`);

                this.display_losses = Cookies.get(`loss_count`);


            },


            logout_button(){


                Cookies.remove(`login_token`);

                this.$router.push(`/`);

            },


            roll_dice(win_count, loss_count){

               let roll_amount = Cookies.get(`roll`);

               console.log(roll_amount);

               this.display_current_roll = roll_amount;



               if(roll_amount >= 50){

                console.log(`winner`);

                this.win_count_obj +=1;

                win_count = this.win_count_obj;

                Cookies.set(`win_count`, win_count);

                this.updatescoreboard();


               }else if(roll_amount <50){

                console.log(`loser`);

                this.lose_count_obj +=1;

                loss_count = this.lose_count_obj;

                Cookies.set(`loss_count`, loss_count);


                this.updatescoreboard();


               }

               




                axios({


                    method: `GET`,

                    url: `http://www.randomnumberapi.com/api/v1.0/randomnumber`,



                }).then((response) =>{


                    response;

                    Cookies.set(`roll`, `${response[`data`][0]}`);


                    

      


                }).catch((error) =>{

                    console.log(error);

                });


            }


        },

        created(){




        },

        mounted(){




            this.updatescoreboard();

                    let login_status = Cookies.get(`login_token`);

                    let login_parse = JSON.parse(login_status);

                    console.log(login_parse);

                    if(login_parse === "logged in"){

                       console.log(`welcome`)

                       this.welcome_user = `Welcome, user`
                        

                    }else{

                     

                        this.$router.push(`/`);

                    }
        }
    }
</script>

<style scoped>

</style>