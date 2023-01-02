<template>
  <span class="tag" :class="currentColor">
      <span class="content">{{ tag }} </span>
      <span class="close" @click="$emit('removeTagEvent',index)"> X</span>
    </span>
</template>

<script>
  export default{
    props:["tag","index", "changeColor"],

    data(){
      return{
        currentColor: null
      }
    },
    mounted(){
      this.currentColor = this.changeColor
    }
  }
</script>

<style scoped>
  .tag {
  padding: 10px;
  font-size: 14px;
  position:relative
}

.tag:not(:last-child) {
  margin-right: 10px;
}

.tag .close {
  font-size: 10px;
  cursor: pointer;
  font-weight: 700;
  position: absolute;
  top: 0;
}

.success{
  background-color: #d4edda;
  color: #155724;
}

.primary{
  background-color: #cce5ff;
  color: #004085;
}

</style>