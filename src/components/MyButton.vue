<template>
  <div class="hello">

    <button class="mybutton" @click="handleClick" :disabled="banned"><slot></slot></button>

  </div>
</template>

<script>
export default {
  props: {
    fontcolor: {
      type: String,
      default: "#000"
    },
    banned: {
      type: Boolean,
      default: true
    }
  },
  name: '',
  computed: {

  },
  data () {
    return {
    }
  },
  mounted: function () {
  },
  methods: {
    getStyle: function () {
      return {
        color: this.fontcolor,
        ":active color": "#fff"
      }
    },
    handleClick: function () {
      this.$emit('click');
    }
  },
  watch: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
