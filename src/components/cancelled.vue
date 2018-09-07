<template>
  <div class="cancel">
    <div class="cancelled">
      <div><span>已取消</span><span></span></div>
    </div>
    <div class="event-box" style="height: auto; display: block;">
      <ul v-for="(item,index) in cancelled" :key="index">
        <li class="event-list">
          <div style="float:left;text-decoration:line-through">{{item}}</div>
          <button class="cancel-btn" @click="reset(index)">恢复</button>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  props:['update'],
  data(){
    return {
      cancelled:[],
      undone:[]
    }
  },
  beforeUpdate:function(){
    console.log(this.update);
    this.update == 'cancel'?this.cancelled = JSON.parse(localStorage.getItem('cancelled')):'';
  },
  mounted:function(){
    this.cancelled = JSON.parse(localStorage.getItem('cancelled'));
  },
  methods:{
    // 点击取消改变localstorage的内容
    reset(index){
      this.update = 'input';
      if(localStorage.getItem('undone')){
        this.undone.push(this.cancelled[index]);
        this.undone = this.undone.concat(JSON.parse(localStorage.getItem('undone')));
        localStorage.setItem('undone',JSON.stringify(this.undone));
      } else {
        localStorage.setItem('undone',JSON.stringify(this.cancelled[index]));
      }
      this.cancelled.splice(index,1);
      localStorage.setItem('cancelled',JSON.stringify(this.cancelled));
      // location.href = "http://localhost:8082";
    }
  }
}
</script>
<style scoped>
  .cancelled{
    padding: 0 20px;
    overflow: hidden;
  }
  .cancelled > div {
    margin-top: 1px;
    background-color: #00b0f0;
    height: 40px;
    line-height: 40px;
    color: #fff;
    padding: 0 10px;
  }
  .event-box> ul {
    border: 1px solid #ccc;
    padding-left: 10px;
    padding-right: 10px;
    margin: 0 20px;
    overflow: hidden;
  }
  .event-box>ul>li {
    height: 40px;
    line-height: 40px;
    position: relative;
  }
  .cancel-btn{
    float: right;
    margin-top: 8px;
  }
</style>


