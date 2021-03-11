<template>
    <div id="app">
        <div class="app-header">
            <!-- <div class="icon">
                <a-icon type="home" />
            </div> -->
            <div class="app-menu-button">
                <a-button type="primary" ghost style="margin-bottom: 16px" @click="toggleCollapsed">
                    <a-icon :type="collapsed ? 'menu-unfold' : 'menu-fold'" />
                </a-button>
            </div>
        </div>
        <div class="app-content">
            <div class="app-menu">
                <a-menu class="menu-nomal" :default-selected-keys="['1']" :inline-collapsed="collapsed"
                    :open-keys.sync="openKeys" mode="inline" @click="handleClick">
                    <a-sub-menu key="sub1" @titleClick="titleClick">
                        <span slot="title">
                            <a-icon type="mail" /><span>Navigation One</span></span>
                        <a-menu-item-group key="g1">
                            <template slot="title">
                                <a-icon type="qq" /><span>Item 1</span> </template>
                            <a-menu-item key="1">
                                Option 1
                            </a-menu-item>
                            <a-menu-item key="2">
                                Option 2
                            </a-menu-item>
                        </a-menu-item-group>
                        <a-menu-item-group key="g2" title="Item 2">
                            <a-menu-item key="3">
                                Option 3
                            </a-menu-item>
                            <a-menu-item key="4">
                                Option 4
                            </a-menu-item>
                        </a-menu-item-group>
                    </a-sub-menu>
                </a-menu>
            </div>
            <div id="component" class="component-wrapper">
                <!-- <label>文本</label>
                <a-input v-model="unprotect" type="text">
                    <a-icon slot="prefix" type="user" />
                </a-input>
                <a-button @click="btnFetchClick" type="primary">Click to fetch</a-button>
                <label>加密后数据：</label>
                <a-textarea disabled v-model="protect" placeholder="Basic usage" :rows="4" />
                <a-button @click="btnCheckClick" type="primary">解密验证</a-button> -->
                <a-tabs hideAdd default-active-key="1" type="editable-card" @change="callback">
                    <a-tab-pane v-for="tab in tabs" :key="tab.key" :tab="tab.title"  >
                        <component :is="tab.component" v-bind="tab.props" />
                    </a-tab-pane>
                </a-tabs>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from "axios";
    import HelloWorld from "./components/HelloWorld.vue";
    import ToDo from "./components/ToDo.vue";
    import UserList from "./components/UserList.vue";
    export default {
        name: 'App',
        components: {
            HelloWorld,
            UserList,
            ToDo
        },
        data() {
            return {
                data: ["1", "2", "3", "4", "5", "6"],
                tabs: [{
                    key: "1",
                    title: "文件管理",
                    component: "HelloWorld",
                    props: {
                        msg: "哈哈哈哈哈哈",
                        changeMessage:function(e){
                            console.log(e);
                        }
                    }
                },{
                    key: "2",
                    title: "代办列表信息",
                    component: "ToDo",
                    props: {
                        message: "to do msg",
                        items:["1","2"]
                    }
                },{
                    key: "3",
                    title: "用户列表",
                    component: "UserList",
                    props: {
                        message: "to do msg",
                        items:["1","2"]
                    }
                }],
                message: "Hello this is first vue app!",
                current: ['mail'],
                openKeys: ['sub1'],
                unprotect: null,
                protect: null,
                collapsed: false,
                currentView: "HelloWorld",
                currentViewProps: {
                    msg: "GG"
                }
            }
        },
        watch: {
            openKeys(val) {
                console.log('openKeys', val);
            },
            current(val) {
                console.log(`current${val}`);
            }
        },
        methods: {
            handleClick(e) {
                console.log('click', e);
            },
            btnFetchClick(e) {
                var that = this;
                axios.get('https://localhost:44433/api/dp/protect/' + this.unprotect)
                    .then(function (response) {
                        // handle success
                        console.log(response.data);
                        that.protect = response.data;
                    }).catch(function (error) {
                        // handle error
                        console.log(error);
                    }).then(function () {
                        // always executed
                    });
                console.log(e);
            },
            btnCheckClick(e) {
                var that = this;
                debugger;
                var url = "https://localhost:44433/api/dp/unprotect/" + this.protect;
                axios.get(url).then(res => {
                    console.log(res.data);
                }).catch(error => {
                    console.log(error);
                }).then(() => {
                    console.log("complete");
                })
            },
            titleClick(e) {
                console.log('titleClick', e);
            },
            toggleCollapsed() {
                this.collapsed = !this.collapsed;
            },
            callback(e) {
                console.log(e)
            },
            returnValue() {
                return "value";
            }
        },
    }
</script>

<style>
    html,
    body {
        width: 100%;
        height: 100%;
    }

    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
    }

    .app-header {
        height: 32px;
        box-sizing: content-box;
        padding: 8px 16px;
        line-height: 32px;
        border-bottom: 4px solid #2c3e50;
        display: flex;
    }

    .app-content {
        flex: 1 1 0;
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
    }

    .app-menu .menu-nomal {
        width: 250px;
        height: 100%;
    }

    .app-menu .ant-menu-inline-collapsed {
        width: auto;
    }

    .app-menu-button {
        padding: 0px 8px;
    }

    .icon {
        color: #03a9f4;
        font-size: 1rem;
        padding-left: 8px;
    }
    .component-wrapper .ant-tabs-tab{
        color: #2196f3;
        background-color: #03a9f4;
    }
    #component {
        width: 100%;
    }
    #component .ant-tabs-tab{
        color: #2c3e50;
        background-color: whitesmoke;

    }
    #component .ant-tabs-tab-active.ant-tabs-tab{
        color: whitesmoke;
        background-color: #2c3e50;
    }
</style>
