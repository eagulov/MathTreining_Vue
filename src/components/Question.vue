<template>
    <div class="alert">
        <h3>{{ x }} + {{ y }} = ?</h3>
        <hr>
        <div class="buttons">
            <button class="btn btn-success"
                    v-for="number in answers"
                    :key="number"
                    @click="onAnswer(number)">
                {{ number }}
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['settings'],
        data(){
            return {
                x: mtRand(this.settings.from, this.settings.to),
                y: mtRand(this.settings.from, this.settings.to)
            }
        },
        computed: {
            good(){
                return this.x + this.y;
            },
            answers(){
                let res = [this.good];
                while(res.length < this.settings.variants){
                    let number = mtRand(this.good - this.settings.range, this.good + this.settings.range);

                    if(res.indexOf(number) === -1){
                        res.push(number);
                    }
                }
                return res.sort(function(){
                    return Math.random() > 0.5;
                });
            } 
        },
        methods: {
            onAnswer(number){
                // console.log(number)
                if(number == this.good){
                    // console.log('success')
                    this.$emit('success');
                }
                else{
                    this.$emit('error', `${this.x} + ${this.y} = ${this.good}!`);
                }
            }
        }
    }
    
    function mtRand(min, max){
        let diff = max - min;
        return Math.floor(Math.random() * (diff + 1)) + min;
    }
</script>

<style scoped>
    .alert{
        padding-top: 20px;
        background-color: rgb(174, 220, 238)
    }

    .buttons{
        display: flex;
        justify-content: space-around;
    }
    .btn{
        margin: 20px 0;
    }

</style>