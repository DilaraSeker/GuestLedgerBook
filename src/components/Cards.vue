<template>
    <div>
        <h2>Guest List</h2>
        <div v-bind:key="card.id" v-for="card in cards">
            <Card  
                v-bind:card="card" 
                v-on:del-card-item="delCardMethod" 
                v-on:edit-card-item="editCardMethod" 
            />        
        </div>
        <div v-if="!cards.length">
            <p>No Cards!</p>
        </div>
    </div>
</template>

<script>
    import Card from "./Card";
    export default {
        name: "Cards",
        props: ["cards"],
        components: {
            Card
        },
        methods: {
            delCardMethod(id){
                //send to parent
                this.$emit('del-card-event', id);
            },
            editCardMethod(id){
                //send to parent (App.vue)
                this.$emit('edit-card-event', id)
            }
        }
    }
</script>