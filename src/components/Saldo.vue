<template>
  <div class="card">
    <div class="card-body">
      R$ {{ (saldo / 100).toFixed(2).toLocaleString('pt-br',{style: 'currency', currency: 'BRL'}) }} 
    </div>
  </div>
</template>

<script>
export default {
  name: 'Saldo',
  props: {
    saldo: Number
  },
  data: () => {
      return{
          saldo: this.props.saldo
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
