<template>
  <tr>
    <th scope="row">{{myIndex}}</th>
    <td><label><input :checked="check" v-on:change="$emit('change', $event.target.checked)" type="checkbox" class="form-check-input" id="exampleCheck1">{{title}}</label></td>
    <td><button class="btn btn-danger" @click="onRemove">X</button></td>
  </tr>
</template>

<script>
export default {
  props: {
    title: String,
    check: Boolean,
    myIndex: Number
  },
  methods: {
    onRemove(e){
      this.$emit('remove');
    }
  }
}

</script>

<style>

</style>