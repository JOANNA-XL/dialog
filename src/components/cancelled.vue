<template>
  <div class="cancel">
    <div class="cancelled">
      <div><span>已取消</span><span></span></div>
    </div>
    <div class="event-box" style="height: auto; display: block;">
      <ul v-for="(item,index) in attr1" :key="index">
        <li class="event-list">
          <input type="checkbox"> 
          <div style="float:left">{{item}}</div> 
          <button class="cancel-btn">取消</button>
        </li>
      </ul>
    </div> 
  </div>
</template>
<script>
export default {
  data(){
    return {
      attr1:['d','x']
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


