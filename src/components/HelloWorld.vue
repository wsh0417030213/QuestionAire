<template>
  <div>
    <QuestionNaire :questions="questions" @submit="handleSubmit" @showCityName="updateCity"></QuestionNaire>
  </div>
</template>

<script>
import QuestionNaire from './QuestionNaire.vue';
export default {
  components: {QuestionNaire},
  name: 'HelloWorld',
  data () {
    return {
      toCity:"北京",
      toaa:"aa",
      questions: [
        {
          type: "radio",
          title: "你的性别",
          choices: ["男", "女","其他"],
          picked: ""
        },
        {
          type: "multi",
          title: "你的爱好",
          choices: ['篮球', '足球', '羽毛球'],
          picked: []
        },
        {
          type: "typetext",
          title: "自我介绍",
          text: ""
        },
        {
          type: "",
          title: "",
          text: ""
        }
      ]
    }
  },
  methods: {
    updateCity(data){
      this.toCity = data.cityname;  //子组件改变了父组件的值
      this.toaa = data.cityaa;  //子组件改变了父组件的值
      console.log('toCity:'+this.toCity);   //打印当前data中 toCity 的值
      alert(this.toaa)
    },
    handleSubmit(e1,e2){
      var text = "";
      text += "你是ssss" + e1[0].picked + "的\n";
      text += "你喜欢" + e1[1].picked.join("和") + "\n";
      text += "你说'" + e1[2].text + "'\n";
      text += "你姓名'" + e2[0]+ "'\n";
       text += "你年龄'" + e2[1]+ "'\n";
       text += "你邮箱'" + e2[2]+ "'\n";
       text += "你爱好'" + e2[3]+ "'\n";
      alert(text);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
