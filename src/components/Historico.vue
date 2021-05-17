<template>
  <div class="card flex-1">
    <div class="card-header">
      Historico de Transações
    </div>
    <div class="card-body">
      <table class="table table-striped">
        <tr v-for="transacao in formatedHistorico" :key="transacao.id">
          <td>{{ transacao.type }}</td>
          <td>R$ {{ transacao.ammount }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Historico',
  props: {
    historico: Array
  },
  data: () => {
    return {
        historico: this.props.historico
      }
  },
  methods:{
    parseAmmount(ammount){
      return (ammount / 100).toFixed(2).toLocaleString('pt-br',{style: 'currency', currency: 'BRL'})
    }
  },
  computed: {
      formatedHistorico(){
        return this.historico.map( transaction => ({
          ...transaction,
          type: transaction.type === 'Rx' ? 'Depósito' : 'Saque',
          ammount: this.parseAmmount(transaction.ammount)
        }))
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .flex-1{ flex: 1; margin-left: 10px;}
</style>
