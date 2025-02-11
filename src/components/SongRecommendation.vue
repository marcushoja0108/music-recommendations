<template>
  <div class="song">
    <button @click="recommendSong">Get recommendation</button>
    <div v-if="recommendation" >
        <h2>{{ recommendation.title }}</h2>
        <h3>Artist: {{ recommendation.artist }}</h3>
        <img class="songCover" :src="recommendation.img">

        <div class="star" @click="recommendation.isFavorite = !recommendation.isFavorite">
          <img v-if="recommendation.isFavorite" src="trueStar.png">
          <img v-else src="falseStar.png">
        </div>
        
        <button @click="deleting = true">Delete</button>

        <div v-if="deleting" class="deleteConfirmation">
          <p>Are you sure you want to delete {{ recommendation.title }} by {{ recommendation.artist }} ?</p>
          <div><button @click="deleteSong(recommendation.id)"> Yes</button>
          <button @click="deleting = false"> No</button></div>
        </div>
    </div>
    <div v-else>Thinking....</div>
  </div>
</template>

<script>

export default {
    props: ['songs'],
    data(){
        return {
            recommendation: null,
            deleting: false
        }
    },
    methods: {
        recommendSong() {
            const randomIndex = Math.floor(Math.random() * this.songs.length)
            this.recommendation = this.songs[randomIndex]
        },
        deleteSong(id) {
          let songToDelete = this.songs.findIndex(song => song.id == id)
          this.songs.splice(songToDelete, 1),
          this.recommendation = null
          this.deleting = false
          // console.log('deleting ' + songToDelete.title + ' by ' + songToDelete.artist)
        }
    },
    }
</script>

<style>
h2 {
  color: #7bb6f0;
  margin-top: 15px;
}

h3 {
  color: #6099b8;
  font-weight: normal;
}
.songCover{
  width: 40vh;
  border-radius: 30px;
  border: solid rgba(255, 255, 255, 0.678);
}
.song{
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;
  position: relative;
}
.star img{
  position: absolute;
  top: 170px;
  right: 10px;
  user-select: none;
  cursor: pointer;
  width: 5vh;
}

.deleteConfirmation{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;

  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  padding: 5%;
  width: 50vh;
  height: 30vh;
  font-size: x-large;
  background: rgba(145, 0, 0, 0.797);
  border-radius: 20px;
}
.deleteConfirmation button{
  margin: 10px;
  background: red;
}
</style>