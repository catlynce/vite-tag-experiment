<template>
  <p>{{label}}</p>
  <div class="tags-wrapper">
    <div class="box">
      <ul>
        <li v-for="tag in tags" :key="tag">
          {{ tag }}
          <span @click="remove(tag)">&times;</span>
        </li>
        <li class="input">
          <input v-model="tag" @keypress.enter="add">
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { ref, toRefs } from 'vue';

export default {
  props: {
    label: {
      type: String,
      default: 'Insert tags',
    }
  },
  setup(props) {
    const { label } = toRefs(props);
    const tag = ref('');
    const tags = ref([]);
    const paddingLeft = ref(0);

    const add = function() {
      tags.value.push(tag.value)
      // paddingLeft.value += tag.value.length * 8 + 30
      tag.value = ''
    }

    const remove = function(tag){
      const idx = tags.value.findIndex((el) => el == tag)
      tags.value.splice(idx, 1);
    }

    return {
      tag, tags, add, remove, paddingLeft, label
    }
  }
}
</script>

<style lang="sass" scoped>
  .tags-wrapper
    position: relative
    display: flex
    margin: 0 auto
    padding: 10px
    width: 500px
    background-color: rgba(0,0,0,.15)
    border-radius: 3px

    .box
      display: flex
      flex-wrap: wrap
      align-items: flex-start
      justify-content: flex-start
      width: 100%
      min-height: 50px
      background-color: #fff
      border: 1px solid #707070


      ul
        margin: 0
        padding: 0
        list-style: none inside none
        display: inline-flex
        justify-content: flex-start
        align-items: flex-start
        flex-wrap: wrap

        li
          display: inline-block
          width: auto
          padding: 2px 6px
          margin: 2px
          color: #fff
          background-color: #404040
          border: 1px solid #707070
          border-radius: 6px

          span
            cursor: pointer

        .input
          padding: 0
          background-color: transparent
          border: none

          input
            display: inline-block
            margin: 5px
            padding: 5px
            height: 20px
            background-color: #f3f3f3
            border: none

            &:focus
              outline: none
</style>