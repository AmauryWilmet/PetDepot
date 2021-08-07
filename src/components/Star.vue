<template>
    <i v-if="selected===false" :class="outlineStar" @mouseover="mouseEnterStar" @click="clickStar"></i>
    <i v-else :class="star" @mouseover="mouseEnterStar" @click="clickStar"></i>
</template>

<script>
export default {
    name: 'Star',
    props: ['selected', 'starId'],
    data() {
        return {
            outlineStar: "far fa-star",
            star: "fa fa-star",
        }
    },
    methods: {
        mouseEnterStar(event) {
            this.$emit('mouseEnterStar', this.starId);
        },
        clickStar(event) {
            this.$emit('clickStar', this.starId);
        },
    },
}
</script>