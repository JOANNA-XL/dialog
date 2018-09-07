<template>
  <div class="unDone">
    <div class="undone">
       <div><span>未完成{{update}}</span><span class="mui-icon mui-icon-arrowdown"></span></div>
    </div>
    <div class="event-box" style="height: auto; display: block;">
      <ul v-for="(item,index) in undone" :key="index">
        <li class="event-list">
          <input type="checkbox" @click="selected(index)" :checked="boole">
          <div style="float:left">{{item}}</div>
          <button class="cancel-btn" @click="cancel(index)">取消</button>
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
      undone: [],
      completed:[],
      boole: false,
      cancelled:[]
    }
  },
  beforeUpdate:function(){
    console.log(this.update);
    this.update == 'inputed'?this.undone = JSON.parse(localStorage.getItem('undone')):'';
  },
  mounted:function(){
    this.undone = JSON.parse(localStorage.getItem('undone'))
  },
  methods:{
    selected(index){
      this.update = 'done';
      var obj = {}
      obj.name = this.undone[index];
      var time = new Date();
      var year = time.getFullYear();
			var month = time.getMonth() + 1 < 10 ? "0" + (time.getMonth() + 1) : time.getMonth() + 1;
			var date = time.getDate() < 10 ? "0" + time.getDate() : time.getDate();
      obj.time = year + "-" + month + "-" + date;
      this.completed.push(obj);
      if(this.getData()){
        this.completed = this.completed.concat(JSON.parse(localStorage.getItem('completed')))
       this.setData();
      } else {
        localStorage.setItem('completed',JSON.stringify(this.completed));
      }
      this.undone.splice(index,1);
      localStorage.setItem('undone',JSON.stringify(this.undone));
      // location.href = "http://localhost:8082"
    },
    cancel(index){
      this.update = 'cancel';
      if(localStorage.getItem('cancelled')){


        this.cancelled.push(this.undone[index]);




        this.cancelled = this.cancelled.concat(JSON.parse(localStorage.getItem('cancelled')));



        localStorage.setItem('cancelled',JSON.stringify(this.cancelled));
      } else {
        localStorage.setItem('cancelled',JSON.stringify(this.undone[index]));
      }


      this.undone.splice(index,1);


      localStorage.setItem('undone',JSON.stringify(this.undone));
      // location.href = "http://localhost:8082"
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


