<template>
    <div>
        <h1>{{ welcome_user }}</h1>

        <button @click="call_api">roll</button>

        <h1>{{ display_current_roll }}</h1>

        <p>Times lost:{{ display_losses }}</p>
        
        <p>Times won:{{ display_wins }}</p>

        <button @click="logout_button">logout</button>


        <h1>{{ unwanted }}</h1>

    </div>
</template>

<script>
import axios from 'axios';
import Cookies from 'vue-cookies';
    export default {
        


        data() {
            return {

                unwanted: undefined,

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
                
                //updates and displays values stored in respective cookies//

               

                this.display_wins = Cookies.get(`win_count`);

                this.display_losses = Cookies.get(`loss_count`);

                this.display_current_roll = Cookies.get(`roll`);

            },


            logout_button(){

                //removes login cookie and pushes user to '/''//

                Cookies.remove(`login_token`);

                this.$router.push(`/`);

            },


            call_api(){



                axios({


                    method: `GET`,

                    url: `http://www.randomnumberapi.com/api/v1.0/randomnumber`,



                }).then((response) =>{


                    response;

                    //if the api succeeds, creates a roll cookie containing the number given//

                    Cookies.set(`roll`, `${response[`data`][0]}`);


                    this.roll();
                    

      


                }).catch((error) =>{

                    //if API fails, prints a message to console.
                    error;

                    console.log(`api failure`);

                });

            },


            roll(win_count, loss_count){


                //making the roll amount = to the value stored in the cookie, then displaying it//

               let roll_amount = Cookies.get(`roll`);

               console.log(roll_amount);

               this.display_current_roll = roll_amount;



               if(roll_amount >= 50){


                //if roll amount is 50 or greater, adds a win, then calls the updatescoreboard() function to display it//

                console.log(`winner`);

                this.win_count_obj +=1;

                win_count = this.win_count_obj;

                Cookies.set(`win_count`, win_count);

                this.updatescoreboard();


               }else if(roll_amount <50){


                //if roll amount is less than 50, adds a loss, then calls the updatescoreboard() function to display it//

                console.log(`loser`);

                this.lose_count_obj +=1;

                loss_count = this.lose_count_obj;

                Cookies.set(`loss_count`, loss_count);


                this.updatescoreboard();


               }

               

            }


        },

        created(){




        },

        mounted(){


            //updates on page load//


            this.updatescoreboard();


            //checks if the user is logged in on page load, if user is not logged in, returns them to login page//

                    let login_status = Cookies.get(`login_token`);

                    let login_parse = JSON.parse(login_status);

                    console.log(login_parse);

                    if(login_parse === "logged in"){

                       console.log(`welcome`)

                       this.welcome_user = `Welcome, user`
                        

                    }else{

                     
                        this.unwanted = "YOU AREN'T LOGGED IN, BEGONE MONSTER!!!";


                        this.$router.push(`/`);

                    }
        }
    }
</script>

<style scoped>

</style>