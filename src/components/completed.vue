<template>
  <div class="complet">
    <div class="completed">
      <div><span>已完成</span><span></span></div>
    </div>
    <div class="event-box" style="height: auto; display: block;">
      <ul v-for="(item,index) in completed" :key="index">
        <li class="event-list">
          <input type="checkbox" checked @click="select(index)">
          <div style="float:left">{{item.name}}</div>
          <span class="cancel-btn">{{item.time}}</span>
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
      completed:[],
      undone:[]
    }
  },
  beforeUpdate:function(){
    console.log(this.update);
    this.update == 'done'?this.completed = JSON.parse(localStorage.getItem('completed')):'';
  },
  mounted:function(){
    this.completed = JSON.parse(localStorage.getItem('completed'))
  },
  methods:{
    select(index){
       this.update = 'undone';
      if(localStorage.getItem('undone')){
      this.undone.push(this.completed[index].name);
      this.undone = this.undone.concat(JSON.parse(localStorage.getItem('undone')));
      localStorage.setItem('undone',JSON.stringify(this.undone));
      } else {
        localStorage.setItem('undone',JSON.stringify(this.completed[index].name));
      }
      this.completed.splice(index,1);
      localStorage.setItem('completed',JSON.stringify(this.completed));
      // location.href = "http://localhost:8082"
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


