<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <a-input v-model="state">

        </a-input>
        <a-input v-model="noState">

        </a-input>
        <div class="cc">
            <label>
                {{inputText}}
            </label>
            <label>
                {{now}}
            </label>
            <label>
                {{getNow()}}
            </label>
            <a-button @click="logClick" type="primary">
                CLick
            </a-button>
        </div>

    </div>
</template>

<script>
    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        data(){
            return {
                state:"ok",
                noState:null,
            }
        },
        computed:{
            inputText:function(){
                return this.state;
            },
            now:function(){
                return new Date();
            }
        },
        watch:{
            state:function(value){
                console.log(value);
                this.noState = "not" + value;
            }
        },
        methods:{
            logClick(e){
                console.log(this);
                console.log(this.inputText);
            },
            getNow(){
                return new Date();
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }
    .cc{
        display: flex;
        flex-direction: column;
    }

    a {
        color: #42b983;
    }
</style>
