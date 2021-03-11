<template>
    <div>
        <a-button @click="addUser" type="primart">Click</a-button>
        <div class="user-list">
            <div class="user-item" v-for="user in users" :key="user.id">
                {{ user.name }}
            </div>  
        </div>
    </div>
</template>

<script>
    export default {
        name:"UserList",
        props:{

        },
        data(){
            return {
                users:[{
                    id:"18010105",
                    name:"吕明鸿"
                }]
            }
        },
        methods:{
            addUser(e){
                var id = Math.random() * 100;
                var user = {
                    id:id,
                    name:"name" + id
                };
                this.users.push(user);
            }
        }
    }
</script>
<style scoped>
    .user-list{
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
    }
    .user-item{
        flex: 0 0 250px;
        padding: 8px 16px;
        font-size: 1rem;
        min-width: 250px;
        margin: 4px 8px;
        color: rgb(96, 204, 236);
        background: rgb(116, 114, 114);
        border-radius: 4px;
        box-shadow: 4px 4px 4px rgb(177, 177, 177);
    }
</style>