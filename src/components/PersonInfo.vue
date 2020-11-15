<template>
  <div class="hello">
    <div class="err_content" v-if="errMsg.length">
      <ul>
        <li v-for="(err, index) in errMsg" :key="index">{{ err }}</li>
      </ul>
    </div>
    <p>
      <label for="user_name">姓名：</label>
      <input
        id="user_name"
        name="user_name"
        type="text"
        v-model="user_name"
        @blur="checkName"
      />
    </p>
    <p>
      <label for="user_age">年龄：</label>
      <input
        id="user_age"
        name="user_age"
        type="number"
        v-model="user_age"
        min="0"
        max="100"
        @blur="checkAge"
      />
    </p>
    <p>
      <label for="user_email">邮箱：</label>
      <input
        id="user_email"
        name="user_email"
        type="email"
        v-model="user_email"
        @blur="checkMail"
      />
    </p>
    <p>
      <label for="user_like">爱好：</label>
      <select
        name="user_like"
        id="user_like"
        v-model="user_like"
        @change="checkLike"
      >
        <option value="0">看书</option>
        <option value="1">写代码</option>
        <option value="2">看代码</option>
      </select>
    </p>
    <p></p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      errMsg: [],
      user_name: null,
      user_age: null,
      user_email: null,
      user_like: null,
      flag: true,
      totlaText: [],
    };
  },
  methods: {
    checkName(e) {
      this.errMsg = [];
      if (!this.user_name) {
        this.errMsg.push("用户姓名不能为空");
      }

      this.totlaText.push(this.user_name);
      this.$emit("reduce", this.totlaText);
      e.preventDefault(); // 通知浏览器不要执行与事件关联的默认动作
    },
    checkAge(e) {
      this.errMsg = [];
      if (!this.user_age) {
        this.errMsg.push("年龄格式输入错误");
      }

      this.totlaText.push(this.user_age);
      this.$emit("reduce", this.totlaText);
      e.preventDefault(); // 通知浏览器不要执行与事件关联的默认动作
    },
    checkMail(e) {
      this.errMsg = [];
      if (!this.user_email) {
        this.errMsg.push("邮箱不能为空");
      } else if (!this.checkEmail(this.user_email)) {
        this.errMsg.push("邮箱格式不正确");
      }

      this.totlaText.push(this.user_email);
      this.$emit("reduce", this.totlaText);
      e.preventDefault(); // 通知浏览器不要执行与事件关联的默认动作
    },
    checkLike(e) {
      this.errMsg = [];
      var obj = document.getElementById("user_like");
      var index = obj.selectedIndex;
      var user_val = obj.options[index].text;

      this.totlaText.push(user_val);
      this.$emit("reduce", this.totlaText);
      e.preventDefault(); // 通知浏览器不要执行与事件关联的默认动作
    },
    checkEmail(email) {
      var reg = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return reg.test(email);
    },
  },
  watch: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  width: 80%;
  margin: 0 auto;
}
input,
select {
  display: inline-block;
  width: 50%;
  height: 25px;
}
select {
  height: 40px;
}
button {
  width: 100px;
  background: rgb(41, 135, 243);
  color: white;
}
.err_content li {
  color: red;
}
</style>
