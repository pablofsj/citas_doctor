<template>
  <b-container>
    <h2>Las citas del Doc</h2>
    <h2 class="post_header"></h2>
    <br>
    <br>
    <b-row>
      <b-col md="12" class="my-1">
        <b-form-group
          label="Buscar :"
          label-cols-md="1"
          label-align-md="left"
          label-size="md"
          label-for="filterInput"
        >
          <b-input-group size="sm">
            <b-form-input
              v-model="filter"
              type="search"
              id="filterInput"
            ></b-form-input>
            <b-input-group-append>
              <b-button :disabled="!filter" @click="filter = ''">Limpiar</b-button>
            </b-input-group-append>
          </b-input-group>
        </b-form-group>
      </b-col>  
      <b-col md="12" sm="12">
        <b-table :filter="filter" head-variant="dark" striped hover :items="citas_dostor" :fields="titulos_tabla"></b-table>
      </b-col>
    </b-row>
    <button @click.prevent="$router.push('agendar')" type="button" class="btn btn-success">Deseo agendar una cita con el Doc</button>
  </b-container>
</template>

<script>
import { db } from '../firebase'; 


export default {
  data() {
    return {
      titulos_tabla: [
        { key: 'fecha', sortable: true},
        { key: 'hora', sortable: true},
        { key: 'nombre', sortable: true},
        { key: 'edad', sortable: true},
        { key: 'sintoma', sortable: true}
      ],
      filter: null
    }
  },
  firestore() { 
    return {
      citas_dostor: db.collection('citas_dostor')
    }
  },
  computed: {
    sortOptions() {
      // Create an options list from our fields
      return this.fields
        .filter(f => f.sortable)
        .map(f => {
          return { text: f.label, value: f.key }
        })
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


.post_header{
position: relative;
content: "";
width: 100px;
margin: 0 auto;
margin-top: 10px;
border: 2px solid #151e2d;
display: block;
}
</style>