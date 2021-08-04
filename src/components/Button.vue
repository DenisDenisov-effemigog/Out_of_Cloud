<template>
    <div class="button">
        <div class="button__wrap">
            <button @click="clickBtn">К покупкам</button>
        </div>
    </div>
</template>

<script>
export default {
    name:"Button",
    methods:{
        clickBtn(){
            this.$emit("openModal")
        }
    }
}
</script>