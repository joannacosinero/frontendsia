<template>
    <div>
        <NavBar />
        <EditRecord :record="selectedRecord" />
        <DeleteRecord :record="selectedRecord" @onDeleted="getAll"/>
        <div class="container">
            <h1>
                Records
                <RecordsModalEntry class="float-right" @onAdd="getAll"/>
            </h1>

            <table class="table table-bordered table-stripped">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Name</th>
                        <th>Address</th>
                        <th>Birthdate</th>
                        <th>Gender</th>
                        <th>Height</th>
                        <th>Weight</th>
                        <th>Blood</th>
                        <th>&nbsp;</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="record in records" :key="record.id">
                        <td>{{record.name}}</td>
                        <td>{{record.address}}</td>
                        <td>{{record.date_of_birth}}</td>
                        <td>{{record.gender}}</td>
                        <td>{{record.height}}</td>
                        <td>{{record.weight}}</td>
                        <td>{{record.blood}}</td>
                        
                        <td>
                            <b-button @click="onEdit(record)" variant="info" size="sm">
                                Edit
                            </b-button>
                        </td>
                        <td>
                            <b-button @click="onDelete(record)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    
    data() {
        return {
            records: [],
            selectedRecord: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('https://lentrix.tk/cosinero/api/records')
            .then((res)=>{
                if(res.status==200) {
                    this.records =res.data
                }
            })
        },
        onEdit(selectedRecord) {
            this.selectedRecord = selectedRecord;
            this.$bvModal.show('editRecord')
        },
        onDelete(selectedRecord) {
            this.selectedRecord = selectedRecord;
            this.$bvModal.show('deleteRecord')
        }
    },
    created() {
        this.getAll()
    }
}
</script>