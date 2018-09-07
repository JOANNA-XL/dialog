<template>
  <div class="input">
    <input v-model="event" type="text" placeholder="待办事项">
    <input type="button" @click="getValue" value="提交">
  </div>
</template>
<script>
export default {
  data(){
    return {
      event:'',
      eventList:[]
    }
  },
  // var _this = this,
  methods: {
    getValue(){
      if(this.event){
        this.eventList.push(this.event);
        this.event = '';
        if(localStorage.getItem('undone')){
          this.eventList = this.eventList.concat(JSON.parse(localStorage.getItem('undone')));
          localStorage.setItem('undone',JSON.stringify(this.eventList))
        }else{
          localStorage.setItem('undone',JSON.stringify(this.eventList))
        }
      }
      
    }
  },
}
</script>
<style>
  .input {
    position: relative;
    margin: 60px 20px 20px 20px;
    text-align: center;
    
  }
  input {
    height: 40px;
    border: 1px solid #ccc;
    border-radius: 5px;
    position: absolute;
    font-size: 18px;
    padding-left: 10px;
    bottom: 0;
  }
  input:first-of-type{
    width: 230px;
    left: 0;

  }
  input:last-of-type{
    right: 0;
    margin: 0;
    width:80px;
    background-color: #00b0f0;
    color: #fff;
    font-size: 18px;
  }
</style>

