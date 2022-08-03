<template>
<div class="container">
<section class="todoapp">
        <header>
            <div class="txt">
            <p><b>Crée ta TODO</b></p>
            <p>que devez vous faire</p>
            </div>
           
            <div class="add">
                <input type="text" class="new-todo" placeholder="ajouter une tache" v-model="newTodo" @keyup.enter="addTodo">
                <button  v-on:click="addTodo">Ajouter</button>
            </div>
            <div class="filtre" v-show="todos.length > 1">
                <a href="#" :class="{selected: filtre =='all'}" v-on:click="changefiltre()"><b>Toutes</b></a>
                <a href="#" :class="{selected: filtre =='todo'}" v-on:click="changefiltre1()"><b>A faire</b> </a>
                <a href="#" :class="{selected: filtre =='done'}" v-on:click="changefiltre2()"><b> Faites</b></a>
            </div>
        </header>
         <div class="main" v-for="todo in filtretodo" :key="todo" :class="{completed:todo.completed}">
         <div class="list" :class="{color:todo.completed}">
            <div class="check-name">
                <input type="checkbox" v-model="todo.completed">
                <p @dblclick="editTodo(todo)"> {{todo.name}}</p>
            </div>
            <img src="../assets/close.svg" alt="" @click="deleteTodo(todo)">
         </div>
       
    </div>
    <footer>
        <span class="todocount"> <strong>{{restant}}</strong> tache a faire</span>
    </footer>

    </section>


</div>
    
</template>


<script>
export default {
data (){
    return{
        todos:[],
        newTodo:'',
        filtre:'all'
    }
},
methods:{
    editTodo(todo){
        this.editing = todo
    },
    addTodo (){
        if(this.newTodo =='' || this.newTodo ==' ' ){
            console.log('todo vide')
        }else if(this.todos.length >= 12){
          alert('Liste trop grande!')
        }else{
              this.todos.push({
            completed: false,
            name:this.newTodo
        })
        this.newTodo=''
        }
    },
    changefiltre(){
        this.filtre = "all"
    } ,changefiltre1(){
        this.filtre = "todo"
    }, changefiltre2(){
        this.filtre = "done"
    },
    deleteTodo (todo){
        this.todos = this.todos.filter(i => i !== todo)
    }
},
computed:{

    restant(){
       return this.todos.filter(todo => !todo.completed).length
    },     

    filtretodo (){
        if (this.filtre == 'todo'){
            return this.todos.filter(todo => !todo.completed)
        }else if (this.filtre == 'done'){
            return this.todos.filter(todo => todo.completed)
        }
        return this.todos
    }, 
}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');
*{
    padding: 0;
    margin: 0;
    font-family: 'Montserrat', sans-serif;
    box-sizing: border-box;
}
.container{
    width: 100%;
    height: 100vh;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
background-image: linear-gradient(to right top, #4b7737, #2a8b61, #009e91, #00aec1, #12baeb);   
}
section{
    width: 40%;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
    filter: blur(0px);
    background-color: white;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0px 0px 11px 2px rgba(43,38,38,0.56);
    max-width: 450px;
    min-width: 250px;
}
.main{
    display: flex;
    width: 100%;
}
.color{
    background-color: #464d77!important;
}
.completed{
color: gray;
text-decoration:line-through;
}
.selected{
    color: #464d77 !important;;
    font-size: 18px;
}
.filtre{
    width: 100%;
    display: flex;
    justify-content: space-around;
}
.filtre a{
    color: black;
     text-decoration: none;
}
.main img{
    opacity: 1;
    transition: opacity 1s;
    width: 30px;
    background-color: #464D77;
    border-radius: 0PX 5PX 5PX 0PX;
}

.main img:hover{
    width: 32px;
}

.txt{
    padding: 5px 0;
}
.add{
display: flex;
padding:15px 0px;
width: 100%;
}
.add input{width: 75%;
height: 25px;
box-shadow: 0px 0px 10px -2px rgba(0,0,0,0.47);
border:1.5px solid black;
border-radius: 2px;
margin: 0 5px 0 0;
}
.add button{width: 25%;}
header{
    width: 100%;
    padding: 5px 0;
}
header button{
background-color: #464D77;
color:white ;
border: 0;
}
header p{
    padding: 4px;
}
.list{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1px px;
    background-color: white;
    border-radius: 5px;
    margin: 5px 0;
box-shadow: 0px 0px 10px -2px rgba(0,0,0,0.47);
transition: background-color .5s;
font-size: 18px;
}
.check-name{
    display: flex;
}
.check-name input{
    margin: 0 5px;
}

.todocount{
    pad: 3px 0;
}

</style>