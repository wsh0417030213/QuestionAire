<template>
  <div class="hello">
    <div>
      <span>{{ title }}</span>
      <div v-for="(choice, index) in choices">
        <input type="radio" v-model="curValue" :value="choices[index]" :id="values[index]">
        <label :for="values[index]">ss{{ choice }}</label>
      </div>
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
    choices: {
      type: Array,
      default: function () {
        return ["C1", "C2", "C3"]
      }
    }
  },
  name: '',
  computed: {

  },
  data () {
    var _this = this;
    var values = [];
    this.choices.forEach(function (item, index) {
      values.push(_this.name + (index + ''));
    });
    return {
      values: values,
      curValue: ""
    }
  },
  mounted: function () {
  },
  methods: {

  },
  watch: {
    curValue: function (val) {
      this.$emit('pick', val);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
