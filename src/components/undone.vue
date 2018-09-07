<template>
  <div class="unDone">
    <div class="undone">
       <div><span>未完成</span><span class="mui-icon mui-icon-arrowdown"></span></div>
    </div>
    <div class="event-box" style="height: auto; display: block;">
      <ul v-for="(item,index) in undone" :key="index">
        <li class="event-list">
          <input type="checkbox" @click="selected(index)" :key="index">
          <div style="float:left">{{item}}</div>
          <button class="cancel-btn" @click="cancel(index)">取消</button>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  data(){
    return {
      undone:JSON.parse(localStorage.getItem('undone')),
      completed:[]
    }
  },
  methods:{
    selected(index){
      var obj = {}
      obj.name = this.undone[index];
      obj.time = new Date();
      this.completed.push(obj);
      if(localStorage.getItem('completed')){
        this.completed = this.completed.concat(JSON.parse(localStorage.getItem('undone')))
        localStorage.setItem('completed',JSON.stringify(this.completed));
      } else {
        localStorage.setItem('completed',JSON.stringify(this.completed));
      }
      this.undone.splice(index,1);
      localStorage.setItem('undone',JSON.stringify(this.undone));
      console.log(this.undone);
    }
  },
}
</script>
<style scoped>
  .undone{
    padding: 0 20px;
    overflow: hidden;
  }
  .undone > div {
    margin-top: 20px;
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
    margin-top: 8px;
  }
</style>


