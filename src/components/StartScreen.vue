<template>
    <div class="alert alert-secondary">
        <h3>Are you ready?</h3>
        <button class="btn btn-success" @click="$emit('onStart')">
            Start
        </button>
    </div>
</template>

<script>
    export default {
        methods: {
            some(){
                alert(1);
            }
        }
    }

</script>

<style scoped>
    .alert{
        text-align: center;
    }

    h3, .btn{
        margin: 30px 0;
    }
    .btn-success{
        border-radius: 10px;
        background: rgb(60, 190, 5);
        padding: 15px 30px;
    }
    .btn-success:hover{
        background: rgb(163, 226, 179);
        padding: 15px 30px;
    }
</style>