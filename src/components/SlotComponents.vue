<template>
    <div>
        <label>
            SlotComponents
        </label>
        <div>
            {{msg}}
        </div>
        <button>
            <slot>Submit</slot>
        </button>
        <div>
            <slot name="first">first</slot>
            <slot name="second">second</slot>
        </div>
    </div>
</template>

<script>
    export default {
        name:"SlotComponents",
        components: {
        },
        data(){
            return {
                msg:"Hello world"
            }
        }
    };
</script>

<style scoped>

</style>