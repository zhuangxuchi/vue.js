<template>
    <div class="input-text">
        <span>请输入：</span>
        <input v-model="shuru" @keyup.enter="add" class="edit">
        <ul class="task">
            <li v-for="(todo,index) in todolist" :key="index">
                <input type="checkbox" @click="changeStyle(index)" v-model="todo.finish">
                <span :class="{'finish':todo.finish}">{{todo.name}}</span>
                <button class="del" :class="{'native':todo.finish}" @click="del(index)">{{todo.caozuo}}</button>
            </li>
        </ul>
        <p class="empty" v-if="!todolist.length">暂无内容</p>
    </div>
</template>
<script>
export default {
    data (){
        return {
            todolist:[],
            shuru:"",
        }
    },methods:{
        add:function(){
            this.todolist.push({
                name:this.shuru,
                finish:false,
                caozuo:"操作",
            });
            this.shuru=""
        },
        changeStyle: function(index) {
            this.todolist[index].finish=!this.todolist[index].finish;
            if(this.todolist[index].finish){
            this.todolist[index].caozuo='删除'
            }else{
            this.todolist[index].caozuo='操作'
            }
        },
        del:function(index){
            if(this.todolist[index].finish){
                this.todolist.splice(index,1)
            }
        }
    }
}
</script>
<style>
  .input-text{
    margin:0 auto;
    width: 600px;
  }
  .edit{
    /*display:block ;*/
    line-height: 35px;
    box-sizing: border-box;
    padding-left: 20px;
    border-radius: 4px;
    border:1px solid #ccc;
    box-shadow: 0 0 5px #ccc;
  }
  .task {
    margin:0 auto;
  }
  .task li{
    position: relative;
    padding: 10px 0;
    border-bottom: 1px solid #efefef;
    list-style: none;
  }

  .task li:last-child{
    border-bottom: 0;
  }
  .finish{
    text-decoration: line-through;
    color: #ccc;
  }
  .del{
    background: #1696ff;
    text-decoration: none;
    position: absolute;
    right:10%;
    font-size: 12px;
    border: 0;
    outline: 0;
    padding: 2px 5px;
    border-radius: 5px;
    color: #fff;
  }
	.native {
		background: #e21826;
	} 
  .empty{
    font-size: 18px;
    color: #b1b1b1;
    text-align: center;
    padding: 10px 0;
  }
</style>
