<template>
    <div class="hello">
        <DateSelect @select="selectDate"></DateSelect>
    </div>
</template>

<script>
import DateSelect from './DateSelect'
export default {
    name: 'HelloWorld',
    data() {
        return {}
    },
    components: {
        DateSelect
    },
    methods: {
        selectDate(date) {
            console.log(JSON.stringify(date))
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
