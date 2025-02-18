<template>
  <div >
    <h1 class="title">Listen here</h1>
    
    <SongRecommendation :songs='songs'/>

    <button @click="editing = true">Add new song</button>
    <div v-if="editing">
      <input type="text" placeholder="Title" v-model="newSong.title">
      <input type="text" placeholder="Artist" v-model="newSong.artist">
      <input type="file" @change="handleFile">
    
      <button @click="addSong">Add song</button>
    </div>

</div>
</template>

<script>
import SongRecommendation from './components/SongRecommendation.vue';


export default {
  data() {
    return{
      songs: [
        {
          id: 1,
          title: "Chicken Fried",
          artist: "Zac Brown Band",
          img: "Covers\\Zac Brown Band - Chicken Fried.PNG",
          isFavorite: true
        },
        {
          id: 2,
          title: "Take Me Home, Country Roads",
          artist: "John Denver",
          img: "Covers\\John Denver - Take me Home, Country Roads.PNG",
          isFavorite: false
        },
        {
          id: 3,
          title: "Jolene",
          artist: "Dolly Parton",
          img: "Covers\\Dolly Parton - Jolene.PNG",
          isFavorite: false
        },
        {
          id: 4,
          title: "Tennessee Whiskey",
          artist: "Chris Stapleton",
          img: "Covers\\Chris Stapleton - Tennessee Whiskey.PNG",
          isFavorite: false
        },
        {
          id: 5,
          title: "Wagon Wheel",
          artist: "Old Crow Medicine Show",
          img: "Covers\\Old Crow Medicine Show - Wagon Wheel.PNG",
          isFavorite: false
        },
        {
          id: 6,
          title: "Friends in Low Places",
          artist: "Garth Brooks",
          img: "Covers\\Garth Brooks - Friends in Low Places.PNG",
          isFavorite: false
        }
      ],
      editing: false,
      newSong: {
        id: 7,
        title: '',
        artist: '',
        img: '',
        isFavorite: false
      },
      
    }
  },
  methods: {
        handleFile(event){
          const file = event.target.files[0]
          if(file){
            this.newSong.img = URL.createObjectURL(file)
          }
        },
        addSong(){
          this.songs.push(this.newSong)
          this.newSong = {artist: '', title: ''}
          this.editing = false
        },
       
        getRecommendation(){
          this.recommend = true
        }
      },
  components: {SongRecommendation}
}
</script>


<style>
body{
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0;
    margin: 0;
    background: rgb(44, 44, 44);
    color: white;
    text-align: center;
}
.title{
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

button {
  background-color: #ff4a71;
  color: white;
  border: none;
  padding: 10px 15px;
  margin: 10px 0;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

button:hover {
  background-color: #c83a59;
}

input {
  width: calc(100% - 20px);
  padding: 8px;
  margin: 5px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 14px;
}
</style>
