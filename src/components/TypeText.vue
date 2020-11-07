<template>
  <div class="hello">

    <span>{{ title }}</span>
    <div>
      <textarea v-model="value"></textarea>
    </div>

  </div>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      default: "question0"
    },
    title: {
      type: String,
      default: "Question"
    },
    text: {
      type: String,
      default: ""
    }
  },
  name: '',
  computed: {

  },
  data () {
    return {
      value: this.text
    }
  },
  mounted: function () {
  },
  methods: {

  },
  watch: {
    value: function (val) {
      this.$emit('pick', val);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
