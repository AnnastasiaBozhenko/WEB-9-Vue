<template>
  <div id="list_image">
    <Items
      v-for="image of List_img"
      v-bind:image="image"

      v-on:clickimg="clickimg"
    />
  </div>
</template>

<script>
import Items from '@/components/item'
export default {
  props: ['List_img'],
  components: {
    Items
  },
  methods: {
    clickimg(id)
    {
      this.$emit('clickimg',id);
    }
  }
}
</script>