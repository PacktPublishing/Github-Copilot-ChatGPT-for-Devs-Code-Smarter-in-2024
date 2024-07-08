<template>
    <div class="square" @click="$emit('square-click')">
        {{ value }}
    </div>
</template>
  
<script>
export default {
    name: 'Square',
    props: ['value', 'clickSquare'],
}
</script>
  
<style scoped>
.square {
    border: 1px solid #000;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
}
</style>