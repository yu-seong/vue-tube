<template>
    <div class="search-bar">
    <input type="text" @keypress.enter="onInput">
    </div>
</template>

<script>
export default {
    name:'SearchBar',
    methods:{
        onInput(e) {
            //emit 1. 위로 커스텀 이벤트를 쏜다.
            this.$emit('input-change',e.target.value)
        },
    },
}
</script>

<style scoped>
/* scoped 옵션은 해당 컴포넌트에만 영향, 그래도 class지정은 해야한다 */
/*div.search-bar {
  border:3px solid black;
  padding:3px;
  margin:3px;
}*/
div.search-bar {
    text-align:center;
    margin:20px;

}
div.search-bar > input {
    width:75%
}
</style>