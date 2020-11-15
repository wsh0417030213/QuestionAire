<template>
  <div class="hello">
    <div>{{ page + 1 }} / {{ count }}</div>

    <div v-for="(item, index) in questions">
      <RadioSelect v-show="page === index" v-if="item.type=='radio'" :name="'q' + (index + '')" :title="item.title" :choices="item.choices" @pick="handlePick(arguments)"></RadioSelect>
      <MultiSelect v-show="page === index" v-else-if="item.type=='multi'" :name="'q' + (index + '')" :title="item.title" :choices="item.choices" @pick="handlePick(arguments)"></MultiSelect>
      <TypeText v-show="page === index" v-else-if="item.type=='typetext'" :name="'q' + (index + '')" :title="item.title" @pick="handlePick(arguments)"></TypeText>
      <PersonInfo v-show="page === index" v-else @reduce="errMsg"></PersonInfo>
    </div>
<br><br><br>
    <MyButton v-show="page === count -1" :banned="disabledSubmit" @click="handleSubmit">提交</MyButton>
    <MyButton v-show="page < count -1" :banned="disabledNext" @click="handleNext">下一题</MyButton>
    <MyButton v-show="page > 0" :banned="false" @click="handlePrev">上一题</MyButton>
    <MyButton @click="handleReset" :banned="false">重置</MyButton>


    <span @click='select("大连")'>大连</span>

  </div>
</template>

<script>
  import RadioSelect from './RadioSelect.vue';
  import MultiSelect from './MultiSelect.vue';
  import TypeText from './TypeText.vue';
  import MyButton from './MyButton.vue';
  import PersonInfo from './PersonInfo.vue';
export default {
  components: {
    RadioSelect,
    MultiSelect,
    TypeText,
    PersonInfo,
    MyButton
  },
  props: {
    questions: {
      type: Array,
      default: function () {
        return [];
      }
    }
  },
  name: '',
  computed: {
    count: function () {
      return this.questions.length;
    }
  },
  data () {
    return {
      page: 0,
      disabledSubmit: true,
      disabledNext: true,
      totalText:[]
    }
  },
  mounted: function () {
  },
  methods: {

    select(val) {
      let data = {
        cityname: val,
        cityaa: val
      };
      this.$emit('showCityName',data); //select事件触发后，自动触发showCityName事件
    },

    handleSubmit: function () {
  
      this.$emit('submit', this.questions, this.totalText);
     
    },
    handleNext: function () {
      if (this.page < this.count - 1) {
        this.page++;
        this.updateDisabledNext();
      }
    },
    handlePrev: function () {
      if (this.page > 0) {
        this.page--;
        this.updateDisabledNext();
      }
    },
    handleReset: function () {
      var question = this.questions[this.page];
      switch (question.type) {
        case 'radio':
          this.$children[this.page].curValue = "";
          break;
        case 'multi':
          this.$children[this.page].curValue = [];
          break;
        case 'typetext':
          this.$children[this.page].value = "";
          break;
        default:
      }
    },
    errMsg:function(totalText){
     var flag = true;
      if(totalText.length >= 4){
        flag = false;
      } else {
        flag = true;
      }
     this.disabledSubmit = flag;
     this.totalText = totalText;
    },
    handlePick: function (arg) {
      var question = this.questions[this.page];
      switch (question.type) {
        case 'radio':
        case 'multi':
          this.questions[this.page].picked = arg[0];
          break;
        case 'typetext':
          this.questions[this.page].text = arg[0];
          break;
        default:
      }
      this.updateDisabledNext();
      this.updateDisabledSubmit();
    },
    updateDisabledNext: function () {
      var flag = false;
      var item = this.questions[this.page];
      if (item.type === 'radio') {
        if (item.picked === "")
          flag = true;
      } else if (item.type === 'multi') {
        if (item.picked.length < 2)
          flag = true;
      } else {
        if (item.text.length < 10)
          flag = true;
      }
      this.disabledNext = flag;
    },
    updateDisabledSubmit: function () {
      var flag = false;
      this.questions.forEach(function (item) {
        if (item.type === 'radio') {
          if (item.picked === "")
            flag = true;
        } else if (item.type === 'multi') {
          if (item.picked.length < 2)
            flag = true;
        } else {
          if (item.text.length < 10)
            flag = true;
        }
      });
      this.disabledSubmit = flag;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
