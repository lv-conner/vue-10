<template>
    <div>
        <a-button @click="addUser" type="primary">Click</a-button>
        <a-button @click="changeUser" type="primary">change</a-button>
        <div class="user-list">
            <div class="user-item" v-for="user in users" :key="user.id">
                {{ user.name }}
            </div>  
        </div>
        <div>
            <a-table size="small" :columns="columns" :data-source="data" bordered>
                <template slot="name" slot-scope="text">
                  <a>{{ text }}</a>
                </template>

              </a-table>
        </div>
    </div>
</template>

<script>
    const columns = [
        {
            title: 'Name',
            dataIndex: 'name',
            scopedSlots: { customRender: 'name' },
        },
        {
            title: 'Cash Assets',
            className: 'column-money',
            dataIndex: 'money',
        },
        {
            title: 'Address',
            dataIndex: 'address',
        },
    ];

    const data = [
        {
            key: '1',
            name: 'John Brown',
            money: '￥300,000.00',
            address: 'New York No. 1 Lake Park',
        },
        {
            key: '2',
            name: 'Jim Green',
            money: '￥1,256,000.00',
            address: 'London No. 1 Lake Park',
        },
        {
            key: '3',
            name: 'Joe Black',
            money: '￥120,000.00',
            address: 'Sidney No. 1 Lake Park',
        },
    ];
    export default {
        name:"UserList",
        props:{

        },
        data(){
            return {
                users:[{
                    id:"18010105",
                    name:"吕明鸿"
                }],
                data,
                columns
                
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
            },
            changeUser(e){a
                var a = this.users[0];
                a.name = "tim lv" + Math.random();
                a.id = 18010106
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