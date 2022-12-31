<template>
  <span class="tag">
      <span class="content">{{ tag }} </span>
      <span class="close" @click="$emit('removeTagEvent',index)"> X</span>
    </span>
</template>

<script>
  export default{
    props:["tag","index"]
  }
</script>

<style scoped>
  .tag {
  background-color: #ffc822;
  padding: 10px;
  color: #000;
  font-size: 14px;
}

.tag:not(:last-child) {
  margin-right: 10px;
}

.tag .close {
  font-size: 12px;
  cursor: pointer;
  font-weight: 700;
}

</style>