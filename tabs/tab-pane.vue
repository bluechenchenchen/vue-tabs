<template>
  <div class="tab-pane" v-show="active">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    label: String,
    name: String,
  },
  computed: {
    active() {
      return this.$parent.currentName === this.name
    },
  },
}
</script>

<style lang="scss" scoped>

</style>


