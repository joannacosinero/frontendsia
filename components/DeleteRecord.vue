<template>
    <div>
        <b-modal id="deleteRecord" title="Record Entry" ok-title="Delete Record" @ok="onDelete" ok-variant="danger">
            Are you sure you want to delete this record? <br>
            
        </b-modal>
    </div>
</template>
<script>
export default {
  props:{
      record:{}
  },
  methods:{
        async onDelete() {
            this.$axios.delete('https://lentrix.tk/cosinero/api/records/' + this.record.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Record deleted')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>





