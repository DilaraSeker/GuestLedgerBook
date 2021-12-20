<template>
    <div class="float-left">
        <span class="float-right">
            {{card.title}}
            <i class="glyphicon glyphicon-pencil" @click="$emit('edit-card-item', card.id)">edit</i>
            <i class="glyphicon glyphicon-trash" @click="$emit('del-card-item', card.id)">delete</i>
        </span>
        
    </div>
</template>

<script>
    export default {
        name: "CardItem",
        props: ["card"]
    }
</script>

<style scoped>
    .glyphicon-pencil, .glyphicon-trash{
        font-size: 15px;
        padding: 4px;
    }
</style>
<form @submit="addCard">
            <input 
                class="float-left"
                type="text" 
                name="title" 
                v-model="title" 
                placeholder="Email"
            >
            <br>
            <textarea 
                class="float-left"
                name="message" 
                v-model="message" 
                placeholder="Please write your message">
            </textarea>
            <br>
            <input 
                type="submit" 
                value="Submit" 
                class="btn btn-info"
            >
        </form>