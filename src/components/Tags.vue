<template>
  <div class="tag-container">
    <Tag v-for="(tag, index) in tags" :tag="tag" :index="index" :changeColor="color" @removeTagEvent="deleteItem($event)" />
    <input autofocus placeholder="Add item..." type="text" @keydown.enter="addTag" @keydown.backspace="removeTag">
    <p class="error" v-if="error">{{ duplicateTag }} is already exists</p>
  </div>
</template>

<script>
import Tag from './Tag.vue'
export default {
  components: {
    Tag
  },
  data() {
    return {
      tags: [],
      error: false,
      duplicateTag: ""
    }
  },
  methods: {
    addTag(event) {
      let inputText = event.target
      let matchedTag = false
      if (inputText.value.length > 0) {
        this.tags.forEach(tag => {
          if (tag.toLowerCase() === inputText.value.toLowerCase()) {
            matchedTag = true
          }
        })
        if (!matchedTag) {
          this.tags.push(inputText.value)
          inputText.value = ""
        } else {
          this.duplicateTag = inputText.value
          this.error = true
          setTimeout(() => {
            this.error = false
          }, 2000)
        }
      }
    },
    removeTag(event) {
      if (event.target.value.length <= 0) {
        this.tags.pop()
        // this.tags.splice(this.tags.length -1, 1)
      }
    },
    deleteItem(itemIndex) {
      // let index = this.tags.indexOf(itemIndex)
      this.tags.splice(itemIndex, 1)
    }
  },
  props: {
    modelValue:{
      required: false
    },
    color:{
      type : String,
      required: false,
      default: "primary"
    }
  },
  created() {
    if (this.modelValue) {
      if (this.modelValue.length > 0) {
        this.tags = this.modelValue.split(',')
      }
    }
  },
  watch:{
    tags(newVal){
      this.$emit("update:modelValue", newVal)
    }
  }
}
</script>

<style scoped>
.tag-container {
  margin: 20px 0;
  border: 1px solid #333;
  padding: 20px;
}

input {
  outline: none;
  height: 30px;
  width: 100px;
}

.error {
  color: rgb(182, 0, 0);
}
</style>