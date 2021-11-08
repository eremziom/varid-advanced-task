<template>
    <div class="table">
        <b-table responsive hover :items="dataTable" :fields="dataFields" id="table-1" :current-page="currentPage" :per-page="10">
            <template #cell(buttons)="row">
                <div class="d-flex flex-row">
                <b-button variant="info" size="sm" class="mr-2" v-on:click="modifyDataPopUp(row.item)">
                MODIFY
                </b-button>
                <b-button variant="info" size="sm" class="mr-2" v-on:click="removeDataPopUp(row.item)">
                REMOVE
                </b-button>
                </div>
            </template>
        </b-table>
        <div>
            <b-modal id="modal-1" hide-footer :title="`Do you want to modify ${currentItem.name} ${currentItem.last_name} data?`">
                <b-button class="mt-3" variant="outline-success" block v-on:click="confirmModify(currentItem)">Yes</b-button>
                <b-button class="mt-2" variant="outline-danger" block v-on:click="cancelPopup('modal-1')">No</b-button>
            </b-modal>
        </div>
        <div>
            <b-modal id="modal-2" hide-footer :title="`Do you want to remove ${currentItem.name} ${currentItem.last_name} data?`">
                <b-button class="mt-3" variant="outline-success" block v-on:click="confirmRemove(currentItem)">Yes</b-button>
                <b-button class="mt-2" variant="outline-danger" block v-on:click="cancelPopup('modal-2')">No</b-button>
            </b-modal>
        </div>
        <b-container>
            <b-row align-h="center">
                <b-pagination
                    v-model="currentPage"
                    :total-rows="rows"
                    :per-page="10"
                    aria-controls="table-1"
                ></b-pagination>
            </b-row>
        </b-container>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'Table',
    async created(){
        await this.getAllData();
    },
    computed: {
      rows() {
        return this.dataTable.length
      }
    },
    methods: {
        async getAllData(){
            await axios
            .get('http://test01.varid.pl:4080/api/contacts')
            .then(response => (
                console.log(response),
                this.dataTable = response.data,
                console.log('data pobrana')
            ))
            .catch(e => (
                console.log(e)
            ))
            return this.dataTable
        },
        modifyDataPopUp(data){
            this.currentItem = data;
            this.$bvModal.show('modal-1');
        },
        removeDataPopUp(data){
            this.currentItem = data;
            this.$bvModal.show('modal-2');
        },
        confirmModify(data){
            this.$emit('editData', data);
            this.$bvModal.hide('modal-1');
        },
        confirmRemove(data){
            console.log('axios z delem', data);
            this.$bvModal.hide('modal-2');
        },
        cancelPopup(id){
            this.$bvModal.hide(id);
        },
    },
    data: function(){
        return{
            dataTable: [],
            dataFields: ['name', 'last_name', 'phone_number', 'email', 'country', 'city', 'address', 'buttons'],
            currentItem: '',
            currentPage: 1,
        }
    }
}
</script>

<style lang="css" scoped>
.table {
    font-size: 12px;
    max-width: 95%;
    margin: 0 auto;
}
</style>