<template>
  <div class="tag-container">
    <span v-for="(tag, index) in tags" :key="tag" class="tag">
      <span class="content">{{ tag }} </span>
      <span class="close" @click="deleteItem(index)"> X</span>
    </span>
    <input autofocus placeholder="Add item..." type="text" @keydown.enter="addTag" @keydown.backspace="removeTag">
    <p class="error" v-if="error">{{ duplicateTag }} is already exists</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tags: ["Vuejs", "React", "Angular", "Nodejs", "Rust", "Assembly", ".Net"],
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
      if (event.keyCode === 8) {
        console.log("backspace")
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
  }
}
</script>

<style>
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.tag-container {
  border: 1px solid #333;
  padding: 20px;
}

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

input {
  outline: none;
  height: 30px;
  width: 100px;
}

.error {
  color: rgb(182, 0, 0);
}
</style>