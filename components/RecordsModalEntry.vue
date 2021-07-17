<template>
    <div>
        <b-button v-b-modal.recordsModalEntry variant="primary " >Add Record</b-button>

        <b-modal id="recordsModalEntry" title="Record Entry" ok-title="Save Record" @ok="onSubmit">
           <form action="#" >
                               <b-form-group 
                label="Name"
                label-for="name"
                >
                <b-form-input id="name" v-model="record.name"  trim></b-form-input>
                </b-form-group>

                 <b-form-group
                label="Address"
                label-for="address"
                >
                <b-form-input id="address" v-model="record.address"  trim></b-form-input>
                </b-form-group>

                 <b-form-group
                label="Birthdate"
                label-for="date_of_birth"
                >
                <b-form-input id="date_of_birth" type="date" v-model="record.date_of_birth"  trim></b-form-input>
                </b-form-group>

                 <b-form-group
                label="Gender"
                label-for="gender"
                >
                <b-form-input id="gender" v-model="record.gender"  trim></b-form-input>
                </b-form-group>

                 <b-form-group 
                label="Height"
                label-for="height"
                >
                <b-form-input id="height"  v-model="record.height"  trim></b-form-input>
                </b-form-group>

                <b-form-group 
                label="Weight"
                label-for="weight"
                >
                <b-form-input id="weight"  v-model="record.weight"  trim></b-form-input>
                </b-form-group>

                <b-form-group
                label="Blood Type "
                label-for="blood"
                >
                <b-form-select v-model="record.blood" :options="bloods"></b-form-select>
                </b-form-group>
           </form>

        </b-modal>
    </div>
</template>

<script>
export default {
    data() {
        return{
            record:{},
             bloods: [
                {value:'A', text: 'A'},
                {value:'B', text: 'B'},
                {value:'AB', text: 'AB'},
                {value:'O', text: 'O'}, 
            ]             
        }
    },
    methods:{
        async onSubmit() {
            this.$axios.post('https://lentrix.tk/cosinero/api/records', this.record)
            .then((res)=>{
                if(res.status==202) {
                    alert('Successfully added in the record')
                    this.$emit('onAdd')
                }
            })
        }
    }
}
</script>