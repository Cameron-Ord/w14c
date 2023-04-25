<template>
    <div>

        <!--displaying the values stored in the variables by the cookies-->

        <h1>{{ roll_amount_obj }}</h1>
        <h1>Wins: {{ win_counter}}</h1>
        <h1> Losses: {{ loss_counter }}</h1>

    </div>
</template>

<script>
import Cookies from 'vue-cookies';
    export default {
        data() {
            return {

              
                roll_amount_obj: undefined,

                win_counter: undefined,
                loss_counter: undefined
            }
        },

        methods:{

            roll_display_(roll_amount){


                this.roll_amount_obj = roll_amount;
            
                Cookies.set(`roll`, this.roll_amount_obj);
            




            },



            update_score_loss(loss_count_obj){


                //makes the sent loss_count_obj equal the above loss_counter variable//

                //then stores this.loss_counter in another variable which is then stored inside a cookie//

                this.loss_counter = loss_count_obj;

                Cookies.set(`loss_count`, this.loss_counter);

                //calls the display function to show the updated loss count//




            },


            update_score_win(win_count_obj){

                //makes the sent win_count_obj equal the above win_counter variable//

                //then stores this.win_counter in another variable which is then stored inside a cookie//

                this.win_counter = win_count_obj;

                Cookies.set(`win_count`, this.win_counter);

                //calls the display function to show the updated win count//



            },
        },



        mounted(){




            //when mounted, receives whats been sent, then calls each respective function//

            this.$root.$on(`win_display`, this.update_score_win);

            this.$root.$on(`loss_display`, this.update_score_loss);
        
            this.$root.$on(`roll_display`, this.roll_display_);
        
            //calls the display function on page load to ensure values are displayed//


            let cookie_wins = Cookies.get(`win_count`);

            if(cookie_wins !== undefined) {

                this.win_counter = cookie_wins;
           
            }else{

                this.win_counter = 0;
            }
         
        
            let cookie_loss = Cookies.get(`loss_count`);

            if(cookie_loss !== undefined) {

                this.loss_counter = cookie_loss;
           
            }else{

                this.loss_counter = 0;
            }

            let cookie_roll = Cookies.get(`roll`);

            if(cookie_roll !== undefined){

                this.roll_amount_obj = cookie_roll;
            }else{

                this.roll_amount_obj = 0;
            }
         
        }


    }
</script>

<style scoped>

</style>