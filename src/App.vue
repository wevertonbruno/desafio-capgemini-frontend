<template>
  <div class="container mt-5">
    <div class="">
      <Saldo v-bind:saldo="saldo" />
      <Actions v-on:onNewTransaction="newTransaction" />
    </div>
    <Historico v-bind:historico="historico" />
  </div>
</template>

<script>

  import Saldo from './components/Saldo';
  import Historico from './components/Historico';
  import Actions from './components/Actions';

  import api from './services/api';

  export default {
    name: 'App',
    components: {
      Saldo,
      Historico,
      Actions
    },
    data: () => {
      return{
        saldo: 0,
        historico: [],
        loading: true
      }
    },

    async mounted(){
      
      try{
        const { data: dataAmmount } = await api.get('/transactions/ammount');
        const { data: dataHistory } = await api.get('/transactions');

        this.saldo = dataAmmount.ammount;
        this.historico = dataHistory.transactions;
        this.loading = false;

      }catch(err){
        console.log(err)
      }
    },

    methods: {
      newTransaction(dados){
          const { ammount, type } = dados.transaction;
          console.log(ammount)
          if(type === 'Rx')
            this.saldo += parseInt(ammount);
          else
            this.saldo -= parseInt(ammount);



          this.historico.push(dados.transaction);
      },

    }

  }
</script>

<style>

  .container{
      display: flex;
  
  }

</style>
