<template>
    <div>
        <center>
        <b-form  @submit="addCard" class="bootstrap-form" style="max-width: 20rem;">
            <b-form-group >
                
                <b-form-input
                    type="text" 
                    name="title" 
                    v-model="title" 
                    placeholder="Email" 
                ></b-form-input>
                <b-form-textarea
                    type="textarea" 
                    name="message" 
                    v-model="message" 
                    placeholder="Please write your message"
                ></b-form-textarea>
                <b-button
                    type="submit" 
                    value="Submit" 
                    variant="primary"
                    class="btn btn-info"
                >SUBMİT</b-button>

            </b-form-group>
        </b-form>
        </center>
    </div>
</template>

<script>
    export default {
        name: "AddCard",
        props: ['editCard'],
        data () {
            return {
                title: '',
                message: '',
                id: '',
                edit: false
            }
        },
        methods: {
            addCard(e){
                e.preventDefault();
                if (this.edit === false){
                    const newCard = {
                        title: this.title,
                        message: this.message,
                        id: Math.floor(Math.random() * 100)
                    };
                    if (newCard.title !== '' && newCard.message !== ''){
                        this.$emit('add-card-event', newCard);
                    }
                    this.title = ''
                    this.message = ''
                }else{
                    //edit card
                    const  cardItem = {
                        title: this.title,
                        message: this.message,
                        id: this.id
                    };
                    //send to parent (App.vue)
                    this.$emit('edit-card-event', cardItem);
                    // clear input field
                    this.title = '';
                    this.message= '',
                    this.edit = false;
                }
            }
        },
        watch: {
            editCard:{
                handler() {
                    this.title = this.editCard.title;
                    this.message = this.editCard.message;
                    this.id = this.editCard.id;
                    this.edit = true
                },
                deep: true
            },
            title:{
                handler(){
                    if(this.title === ''){
                        this.edit = false;
                    }
                }
            },
            message:{
                handler(){
                    if(this.message === ''){
                        this.edit = false;
                    }
                }
            }
        }

    }
</script>

<style scoped>

</style>
