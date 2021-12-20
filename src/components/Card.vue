<template>
    <div>
        <center>
        <b-card           
            tag="article"
            style="max-width: 50rem;"
            class="mb-1"
        > 
            <b-card-title>
                {{card.title}}
            </b-card-title>

            <b-card-text>
                {{card.message}}
            </b-card-text>
            <b-button pill class="btn btn-info float-right" variant="primary" @click="$emit('edit-card-item', card.id)">Edit</b-button>
            <b-button pill class="btn btn-info float-left" variant="primary" @click="$emit('del-card-item', card.id)">Delete</b-button>
        </b-card>
        </center>
    </div>   
</template>

<script>
    export default {
        name: "Card",
        props: ["card"]
    }
</script>

<style scoped>
    
</style>
