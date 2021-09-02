<template>
    <li v-bind:class="{liked: joke.liked}">
    <span>
        <strong>{{id+1}}</strong>
        {{(joke.joke)}}
        
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
        getJoke(joke){
            if(joke.type ==='single'){
                return joke.joke;
            }
            else{
                return joke.setup + '\n'+joke.delivery;
            }
        }
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
