<template>
    <span>{{ this.prefix + Number.parseFloat(this.value).toFixed(this.precision) }}</span>
</template>

<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'price',
    props: {
        value: Number,
        prefix: {
            type: String,
            default: '$'
        },
        precision: {
            type: Number,
            default: 2
        }
    }
}
</script>