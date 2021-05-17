<template>
  <div class="actions mt-3">
    <div class="form-group row">
      <div class="col-md-8">
        <input type="text" name="deposito" class="form-control" placeholder="0.00" v-model="receiveValue">
      </div>
      <div class="col-md-4">
        <button type="button" class="btn btn-primary w-100" v-on:click="handleReceive">Depositar</button>
      </div>
    </div>
    <div class="form-group row mt-2">
      <div class="col-md-8">
        <input type="text" name="saque" class="form-control" placeholder="0.00" v-model="transferValue">
      </div>
      <div class="col-md-4">
        <button type="button" class="btn btn-success w-100" v-on:click="handleTransfer">Sacar</button>
      </div>
    </div>
  </div>
</template>

<script>
import api from '../services/api';

export default {
  name: 'Actions',
  data: () => ({ transferValue: '', receiveValue: '' }),
  methods: {
    async handleReceive(){
      if(!this.receiveValue || this.receiveValue === '')
        return false;
      try{
         const { data: dataObject } = await api.post('/transactions/receive', { ammount: this.receiveValue });
         if(dataObject.success){
           const transaction = dataObject.transaction;

            this.$emit('onNewTransaction', { 
              transaction
            });

          this.receiveValue = "";
          }

      }catch(err){
          console.log(err)
        }
    },

    async handleTransfer(){
      if(!this.transferValue || this.transferValue === '')
              return false;
      try{
        const { data: dataObject } = await api.post('/transactions/transfer', { ammount: this.transferValue });
        
        if(dataObject.success){
           const transaction = dataObject.transaction;

            this.$emit('onNewTransaction', { 
              transaction
            });
            
          this.transferValue = "";
          }

      }catch(err){
          console.log(err)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
