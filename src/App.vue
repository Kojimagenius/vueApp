<template>
  <div id="app">
    <h1>Joke app</h1>
    <SearchPannel
    v-on:search="search"/>
    <hr>
    <JokesList
    v-bind:jokes="jokes"
    v-bind:liked="false"
    v-bind:likedJokes="likedJokes"
    v-on:like="like"/>
  </div>
  
</template>

<script>
import JokesList from '@/components/JokesList.vue'
import SearchPannel from '@/components/SearchPannel.vue'
export default {
  name: 'App',
  data(){
    return{
      likedJokes:[],
      jokes:[
        
      ]
    }
  },
  components: {
    JokesList,
    SearchPannel
  },
  mounted(){
        fetch('https://v2.jokeapi.dev/joke/Any?type=single&amount=2')
        .then(response => response.json())
        .then(json=>setTimeout(()=>{
          let fixedJokes = []
          for(let jk of json.jokes){
            jk.liked = false
            fixedJokes.push(jk);
          }
          this.jokes = fixedJokes;
          },1000))
    },
   methods: {
        like(id){
          this.jokes[id].liked = !this.jokes[id].liked;
            if(localStorage.getItem('liked-jokes')){
                
                try{
                     this.likedJokes = JSON.parse(localStorage.getItem('liked-jokes'))
                     this.likedJokes.push(this.jokes[id].joke)
                     this.saveJokes()
                }catch(e){
                    console.log('smth wrong with local storage')
                }

            }else{
                this.likedJokes = []
                this.likedJokes.push(this.jokes[id].joke)
                this.saveJokes()
            }
        },
        saveJokes(){
            const parsed = JSON.stringify(this.likedJokes);
            localStorage.setItem('liked-jokes', parsed);
        },
        search(text){
          
        }
    },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
