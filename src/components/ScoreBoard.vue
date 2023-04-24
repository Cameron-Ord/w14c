<template>
    <div>

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

                console.log(roll_number, `testing roll`);




            },


            Cookie_Display_WINLOSS(){

                this.display_loss = Cookies.get(`loss_count`);

                this.display_win = Cookies.get(`win_count`);

                this.display_roll = Cookies.get(`roll`);

            },

            update_score_loss(loss_count_obj){


                this.loss_counter = loss_count_obj;

                let loss_count = this.loss_counter;

                Cookies.set(`loss_count`, loss_count);

                console.log(loss_count, `testing loss`);

                this.Cookie_Display_WINLOSS();



            },


            update_score_win(win_count_obj){

                this.win_counter = win_count_obj;

                let win_count = this.win_counter;

                Cookies.set(`win_count`, win_count);

                console.log(win_count,`testing win`);

                this.Cookie_Display_WINLOSS();

            },
        },



        mounted(){

         

            this.$root.$on(`win_display`, this.update_score_win);

            this.$root.$on(`loss_display`, this.update_score_loss);
        
            this.$root.$on(`roll_display`, this.roll_display_);
        
            this.Cookie_Display_WINLOSS();
        
        }


    }
</script>

<style scoped>

</style>