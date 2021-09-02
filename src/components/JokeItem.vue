<template>
    <li v-bind:class="{liked: joke.liked}">
    <span>
        <strong>{{id+1}}</strong>
        {{joke.joke}}
        
    </span>
    <button v-on:click="$emit('like',id)">&hearts;</button>
    </li>
</template>
<script>
export default{
    props:{
        id: Number,
        joke:{
        type: Object,
        required: true
        }
    },
    methods: {
        //like(){
            //console.log(this.todo.liked)
          //  this.todo.liked = !this.todo.liked;
           // this.$emit('like', id)
        //}
    }
}
</script>
<style scoped>
li{
    border: 1px solid black;
    display: flex;
    justify-content: space-between;
    padding: .5rem 2rem;
}
.liked{
    background-color: red;
}
</style>
