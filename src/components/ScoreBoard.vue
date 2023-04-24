<template>
    <div>

        <!--displaying the values stored in the variables by the cookies-->

        <h1>{{ display_roll }}</h1>
        <h1>Wins: {{ display_win }}</h1>
        <h1> Losses: {{ display_loss }}</h1>

    </div>
</template>

<script>
import Cookies from 'vue-cookies';
    export default {
        data() {
            return {

                display_roll: undefined,
                roll_amount_obj: undefined,
                display_loss: undefined,
                display_win: undefined,
                win_counter: undefined,
                loss_counter: undefined
            }
        },

        methods:{

            roll_display_(roll_amount){


                this.roll_amount_obj = roll_amount;

                let roll_number = this.roll_amount_obj;

                Cookies.set(`roll`, roll_number);

            




            },


            Cookie_Display_WINLOSS(){


                //makes the respective variables = to the data stored inside the cookies//

                this.display_loss = Cookies.get(`loss_count`);

                this.display_win = Cookies.get(`win_count`);

                this.display_roll = Cookies.get(`roll`);

            },

            update_score_loss(loss_count_obj){


                //makes the sent loss_count_obj equal the above loss_counter variable//

                //then stores this.loss_counter in another variable which is then stored inside a cookie//

                this.loss_counter = loss_count_obj;

                let loss_count = this.loss_counter;

                Cookies.set(`loss_count`, loss_count);

                //calls the display function to show the updated loss count//

                this.Cookie_Display_WINLOSS();



            },


            update_score_win(win_count_obj){

                //makes the sent win_count_obj equal the above win_counter variable//

                //then stores this.win_counter in another variable which is then stored inside a cookie//

                this.win_counter = win_count_obj;

                let win_count = this.win_counter;

                Cookies.set(`win_count`, win_count);

                //calls the display function to show the updated win count//

                this.Cookie_Display_WINLOSS();

            },
        },



        mounted(){


            //when mounted, receives whats been sent, then calls each respective function//

            this.$root.$on(`win_display`, this.update_score_win);

            this.$root.$on(`loss_display`, this.update_score_loss);
        
            this.$root.$on(`roll_display`, this.roll_display_);
        
            //calls the display function on page load to ensure values are displayed//

            this.Cookie_Display_WINLOSS();
        
        }


    }
</script>

<style scoped>

</style>