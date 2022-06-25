<template>
  <div class="about">
    <button @click.stop="getData">获取数据</button>
    <input type="text" v-model="data">
    <div>{{ data }}</div>
    <button @click.stop="getPostData">获取post请求数据</button>
  </div>
</template>

<script>

export default {
  name: 'AboutView',
  Data () {
    return {
      data:'wu'
    }
  },
  methods: {
    getData() {
      this.$axios.get('https://54c87z1312.zicp.fun')
      .then( res => {
        console.log(res);
        console.log(res.data);
        this.data = res.data;
      })
    },
    getPostData() {
      this.$axios.post('https://54c87z1312.zicp.fun',{
        username:admin,
        password:123456
      })
      .then(res => {
        console.log(res);
        console.log(res.data)
      })
    }
  }
}
</script>