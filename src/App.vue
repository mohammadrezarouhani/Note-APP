<script setup>
  import { ref } from 'vue';
  const showModel=ref(false)
  const newNote=ref("")
  const noteList=ref([])
  const errorMessage=ref("")

  const addToNote=()=>{
    if (newNote.value.length<10){
      return errorMessage.value="Note's length must be greater than 10"
    }
    noteList.value.push({
      id:Math.floor(Math.random()*1000000),
      text:newNote.value,
      date:new Date(),
      color:'hsl('+Math.floor(Math.random()*361)+',50%,75%)'
    })
    showModel.value=false
    newNote.value=""
    errorMessage.value=""
  }

  const closeNote=()=>{
    showModel.value=false
    newNote.value=""
    errorMessage.value=""
  }

</script>

<template>
  <main>
    <div v-if="showModel" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="text-input" id="text-input" cols="30" rows="10"></textarea>
        <p>{{ errorMessage }}</p>
        <button @click="addToNote"  class="add-button">Add To Card</button>
        <button @click="closeNote" class="close-button">Close</button>
      </div>
    </div>
    
    <div class="container">
      <header>
        <h1>Note</h1>
        <button @click="showModel=true">+</button>
      </header>

      <div class="card-container">

        <div v-for="note in noteList" class="card" :style="{backgroundColor:note.color}">
          <p class="text-content">
            {{note.text}}
          </p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
  main {
    width: 100vw;
    height: 100vh;
    background-color: aliceblue;
  }

  header {
    position: relative;
    display: flex;
    align-items: baseline;
    justify-content: space-between;
    padding: 20px;
  }

  header h1 {
    font-size: 75px;
    font-weight: bold;
  }

  header button {
    width: 50px;
    height: 50px;
    padding: 10px;
    cursor: pointer;
    border-radius: 100%;
    border: none;
    color: white;
    background-color: rgb(21, 20, 20);
  }

  .container{
    padding: 80px;
  }
  .card-container {
    display: flex;
    padding: 20px;
    flex-wrap: wrap;
  }

  .card {
    width: 225px;
    height: 225px;
    padding: 10px;
    margin: 20px 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    border-radius: 15px;
    background-color: rgb(237, 182, 44);
  }

  .date{
    font-size: 12.5px;
    font-weight: bold;
  }


  .overlay{
    width: 100%;
    height: 100%;
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: rgba(0, 0, 0,0.77);
    z-index: 10;
  }

  .overlay .modal{
    width: 700px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    display: flex;
    flex-direction: column;
  }

  .overlay textarea{
      font-size: x-large;
      padding: 10px;
    }

  .overlay .modal .add-button{
    width: 100%;
    height: 35px;
    border: none;
    border-radius: 5px;
    padding: 10px 20px;
    margin-top: 15px;
    font-size: 18px;
    background-color: blueviolet;
    color: white;
    cursor: pointer;
  }

  .overlay .modal .close-button{
    width: 100%;
    height: 35px;
    border: none;
    border-radius: 5px;
    margin: 10px 0px;
    font-size: 18px;
    background-color: rgb(193,15,15);
    color: white;
    cursor: pointer;
  }

  .modal p{
    color:rgb(193,15,15) ;
  }
</style>