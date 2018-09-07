<template>
  <div class="complet">
    <div class="completed">
      <div><span>已完成</span><span></span></div>
    </div>
    <div class="event-box" style="height: auto; display: block;">
      <ul v-for="(item,index) in completed" :key="index">
        <li class="event-list">
          <input type="checkbox" checked>
          <div style="float:left">{{item.name}}</div>
          <span class="cancel-btn">{{item.time | formatDate}}</span>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  data(){
    return {
      completed:JSON.parse(localStorage.getItem('completed'))
    }
  },
  created(){
    console.log(JSON.parse(localStorage.getItem('completed')))
  },
  methods:{

  },
  filters:{
    formatDate(time){
      var year = time.getFullYear();
			var month = time.getMonth() + 1 < 10 ? "0" + (time.getMonth() + 1) : time.getMonth() + 1;
			var date = time.getDate() < 10 ? "0" + time.getDate() : time.getDate();
			return year + "-" + month + "-" + date;
    }
  }
}
</script>
<style scoped>
  .completed{
    padding: 0 20px;
    overflow: hidden;
  }
  .completed > div {
    margin-top: 1px;
    background-color: #00b0f0;
    height: 40px;
    line-height: 40px;
    color: #fff;
    padding: 0 10px;
  }
  .event-box> ul {
    border: 1px solid #ccc;
    padding-left: 30px;
    padding-right: 10px;
    margin: 0 20px;
    overflow: hidden;
  }
  .event-box>ul>li {
    height: 40px;
    line-height: 40px;
    position: relative;
  }
  .event-box>ul>li>input{
    width: 15px;
    height: 15px;
    position: absolute;
    top: 13px;
    left: -20px;
  }
  .cancel-btn{
    float: right;
  }
</style>


