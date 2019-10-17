<template>
    <transition-group name="slide-in">
        <div class="option"
        v-for="(option,index) in getOptions"
        :key="'opt'+index"
        :style="{'--index': index}">
            <img v-if="option.img" :src="require('../assets/icons/'+option.img)" alt="">
            <div class="title">{{ option.title }}</div>
            <div class="price">{{ option.price }}</div>
        </div>
    </transition-group>   
</template>

<script>
export default {
    props: [
        'activeConfigStep',
        'configuration'
    ],
    data: () => {
        return {
            showOptions: false
        }
    },
    computed: {
        getOptions() {
            return this.showOptions === true ?
                this.configuration[this.activeConfigStep].options : [];
        }
    },
    mounted() {
        this.showOptions = true;
    }
}
</script>

<style lang="scss" scoped>

</style>