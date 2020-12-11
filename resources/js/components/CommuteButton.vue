<template>
    <div >
        <button class="btn btn-primary ml-4" @click = "commute" v-text="buttonText"></button>
    </div>
</template>

<script>
    export default {

        props: ['userId'],

        mounted() {
            console.log('Component mounted.')
        },

        methods: {
            commute(){
               axios.post('/commute/' + this.userId)
               .then(response=>{
                   console.log(response.data);
                   this.status = ! this.status;
               })
                .catch(errors => {
                    if (errors.response.status == 401)
                        window.location = '/login';
                });
            }
        },

        computed: {
            buttonText() {
                return (this.status) ? '출근' : '퇴근';
            }
        }

    }
</script>
