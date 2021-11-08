<template>
    <div>
        <b-container class="form">
            <b-form @submit="onSubmit" @reset="onReset">
            <b-form-group
                class="label"
                id="input-group-1"
                label="Name"
                label-for="input-1"
            >
                <b-form-input
                class="input"
                id="input-1"
                v-model="name"
                placeholder="Name"
                required
                ></b-form-input>
            </b-form-group>
            <b-form-group
                class="label"
                id="input-group-2"
                label="Last Name"
                label-for="input-2"
            >
                <b-form-input
                class="input"
                id="input-2"
                v-model="last_name"
                placeholder="Last Name"
                required
                ></b-form-input>
            </b-form-group>
            <b-form-group
                class="label"
                id="input-group-3"
                label="Phone Number"
                label-for="input-3"
            >
                <b-form-input
                class="input"
                id="input-3"
                v-model="phone_number"
                placeholder="Phone Number"
                required
                ></b-form-input>
            </b-form-group>
            <b-form-group
                class="label"
                id="input-group-4"
                label="Email"
                label-for="input-4"
            >
                <b-form-input
                class="input"
                id="input-4"
                v-model="email"
                placeholder="Email"
                required
                ></b-form-input>
            </b-form-group>
            <b-form-group
                class="label"
                id="input-group-5"
                label="Country"
                label-for="input-5"
            >
                <b-form-input
                class="input"
                id="input-5"
                v-model="country"
                placeholder="Country"
                required
                ></b-form-input>
            </b-form-group>
            <b-form-group
                class="label"
                id="input-group-6"
                label="City"
                label-for="input-6"
            >
                <b-form-input
                class="input"
                id="input-6"
                v-model="city"
                placeholder="City"
                required
                ></b-form-input>
            </b-form-group>
            <b-form-group
                class="label"
                id="input-group-7"
                label="Address"
                label-for="input-7"
            >
                <b-form-input
                class="input"
                id="input-7"
                v-model="address"
                placeholder="Address"
                required
                ></b-form-input>
            </b-form-group>
            <div class="d-flex justify-content-around">
                <b-button id="add-new-item" type="submit" variant="info">ADD NEW ITEM</b-button>
                <!-- <b-button type="reset" variant="danger">Reset</b-button> -->
                <b-button id="edit-item" v-on:click="onEdit" variant="info">EDIT ITEM</b-button>
            </div>
            </b-form>
            <div>
                <b-modal id="modal-3" hide-footer :title="`Do you want to add this data?`">
                    <b-button class="mt-3" variant="outline-success" block v-on:click="confirmAdd()">Yes</b-button>
                    <b-button class="mt-2" variant="outline-danger" block v-on:click="cancelPopup('modal-3')">No</b-button>
                </b-modal>
            </div>
            <div>
                <b-modal id="modal-4" hide-footer :title="`Do you want to reset data?`">
                    <b-button class="mt-3" variant="outline-success" block v-on:click="confirmReset()">Yes</b-button>
                    <b-button class="mt-2" variant="outline-danger" block v-on:click="cancelPopup('modal-4')">No</b-button>
                </b-modal>
            </div>
            <div>
                <b-modal id="modal-5" hide-footer :title="`Do you want to edit this data?`">
                    <b-button class="mt-3" variant="outline-success" block v-on:click="confirmEdit()">Yes</b-button>
                    <b-button class="mt-2" variant="outline-danger" block v-on:click="cancelPopup('modal-5')">No</b-button>
                </b-modal>
            </div>
        </b-container>
    </div>
</template>

<script>
export default {
    name: 'Form',
    props: ['currentData'],
    created(){
        if(this.currentData !== {}){
            console.log('edit', this.currentData);
            this.name = this.currentData.name;
            this.last_name = this.currentData.last_name;
            this.phone_number = this.currentData.phone_number;
            this.email = this.currentData.email;
            this.country = this.currentData.country;
            this.city = this.currentData.city;
            this.address = this.currentData.address;
        }
    },
    mounted(){
        if(this.currentData){
            document.getElementById("add-new-item").disabled = true;
            document.getElementById("edit-item").disabled = false;
        }   else {
            document.getElementById("add-new-item").disabled = false;
            document.getElementById("edit-item").disabled = true;
        }
    },
    methods: {
        onSubmit(){
            event.preventDefault();
            this.$bvModal.show('modal-3');
        },
        onReset(){
            event.preventDefault();
            this.$bvModal.show('modal-4');
        },
        onEdit(){
            event.preventDefault();
            this.$bvModal.show('modal-5');
        },
        async confirmAdd(){
            console.log('axios z dodaniem do bazy');
            this.$bvModal.hide('modal-3');
        },
        confirmReset(){
            this.name = '';
            this.last_name = '';
            this.phone_number = '';
            this.email = '';
            this.country = '';
            this.city = '';
            this.address = '';
            this.$bvModal.hide('modal-4');
        },
        async confirmEdit(){
            console.log('axios z educją do bazy');
            this.$bvModal.hide('modal-5');
        },
        cancelPopup(id){
            this.$bvModal.hide(id);
        }
    },
    data: function(){
        return{
            name: '',
            last_name: '',
            phone_number: '',
            email: '',
            country: '',
            city: '',
            address: '',
        }
    }
    
}
</script>
<style lang="css" scoped>
    .form{
        max-width: 500px;
        margin-bottom: 40px;
    }
    .input::placeholder {
        font-size: 10px;
        font-style: italic;
    }
    .label{
        color: #0869af;
    }
</style>
