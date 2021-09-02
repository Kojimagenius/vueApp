<template>
<div>
    <ul>
    {{jokes}}
        <JokeItem
        v-for="(joke, ind) of jokes"
        v-on:like="like"
        v-bind:id="ind"
        v-bind:joke="joke"
        v-bind:liked="liked"
        v-bind:key="joke.id"
        />
    </ul>
</div>
</template>
<script>
    import JokeItem from '@/components/JokeItem.vue'
    export default {
    props:['jokes', 'likedJokes', 'liked'],
    components: {
        JokeItem
        },
        methods:{
            like(id){
                this.$emit('like', id)
            }
        },
   
    

    }
    
</script>
<style scoped>
ul{
    list-style:none;
    margin:0;
    padding:0;
}
</style>