<template>
<ModalItm ref="modal">
<form class="app-form">
<div class="form-control">
    <label class="label">Title</label>
    <input v-model="form.title" class="form-input" type="text">
</div>
<div class="form-control form-control-last">
    <label class="label">Description</label>
    <textarea 
    v-model="form.description" 
    cols="30"
    rows="5"
    class="form-input"
    >
    </textarea>
</div>
<div class="app-error">
    <div class="form-error">
        {{formError}}
    </div>
</div>
<button @click="SubmitForm" type="button" class="app-button is-primary">Confirm</button>
</form>
    </ModalItm>
</template>

<script>
import ModalItm from './ModalItm.vue';
export default {
    components: { ModalItm },
    data() {
        return {
            form: {
                title: '',
                description: ''
            },
            formError: ''
        }
    },
    computed:{
        isFormValid(){
            return this.form.title.length > 8 && 
            this.form.description.length > 10 ? true : false 
        },
        modal(){
            return this.$refs.modal
        }
    },
    methods: {
        SubmitForm() {
            if(this.isFormValid){
                this.formError = ''
                this.$emit('formSubmitted', { ...this.form })
                this.modal.close()
                this.resetForm()
            }else{
                this.formError = 'Form Error ! Title needs to be longer than 8 chracters and description sholud be longer than 10 chracters'
            }
        },
        resetForm(){
            this.form.title = ''
            this.form.description = ''
        }
    }
}
</script>

<style scoped>
.form-error{
    margin-bottom: 10px;
}
</style>