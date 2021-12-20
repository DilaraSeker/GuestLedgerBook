<template>
  <div id="app">
    <AddCard 
      v-bind:editCard="editCard" 
      v-on:add-card-event="addCardItem" 
      v-on:edit-card-event="editCardItemEvent" 
    />
    <div id="card">
    <Cards 
      v-bind:cards="cards" 
      v-on:edit-card-event="editCardItem" 
      v-on:del-card-event="deleteCardItem"  
    />
    </div>
  </div>
</template>

<script>

import Cards from "./components/Cards";
import AddCard from "./components/AddCard";

export default {
  name: 'App',
  components: {
     Cards,
     AddCard
  },
  data () {
    return {
      cards: [],
      editCard: {
        title: '',
        message: '',
        id: ''
      }
    }
  },
  methods: {
    addCardItem(newCard){
        this.cards = [...this.cards, newCard];
    },
    deleteCardItem(id){
      this.cards = this.cards.filter(card => card.id !== id);
    },
    editCardItem(id){
      //find the index of the email's id
      let objIndex = this.cards.findIndex(obj=> obj.id === id);
      this.editCard.title = this.cards[objIndex].title;
      this.editCard.message = this.cards[objIndex].message;
      this.editCard.id = id;
    },
    editCardItemEvent(cardItem){
      //find the index of this id's object
      let objIndex = this.cards.findIndex(obj => obj.id === cardItem.id)
      //update the item
      this.cards[objIndex].title = cardItem.title;
      this.cards[objIndex].message = cardItem.message;
    }
  },
  watch: {
    cards: {
      handler() {
        localStorage.setItem('cards',JSON.stringify(this.cards))
      },
      deep: true
    }
  },
  mounted() {
    if (localStorage.getItem("cards")){
      this.cards = JSON.parse(localStorage.getItem("cards"))
    }
  }
}
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#card{
        font-size: 15px;
        padding: 4px;
    }
@import'~bootstrap/dist/css/bootstrap.css'

</style>
