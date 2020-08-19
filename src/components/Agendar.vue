<template>
  <b-container>
    <h2>Nueva cita del paciente <span>{{user.name}}</span></h2>
    <h2 class="post_header"></h2>
    <br>
    <br>
    <b-row>
      <b-col md="6">
        <label for="example-datepicker">Por favor, elija una fecha</label>
        <b-form-datepicker id="example-datepicker" v-model="value" class="mb-2"></b-form-datepicker>
      </b-col>  
      <b-col md="6">
        <label for="example-datepicker">Ahora, seleccione una hora de atención</label>
        <b-form-select v-model="selected" :options="options"></b-form-select>
      </b-col>  
      <br>
      <br>
      <br>
      <b-col md="12" sm="12">
        <b-form-textarea
          id="textarea"
          v-model="text"
          placeholder="Ingrese sus síntomas..."
          rows="3"
          max-rows="6"
        ></b-form-textarea>
      </b-col>
    </b-row>
    <br>
    <b-row>
      <b-col offset-md="3" md="3">
        <button @click.prevent="$router.push('/')" type="button" class="btn btn-danger">Volver al listado de citas</button>
      </b-col>
      <b-col md="2">
        <button type="button" class="btn btn-success">Agendar cita</button>  
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import { db } from '../firebase'; 


export default {
  data() {
    return {
      value:'',
      selected: null,
        options: [
          
          { value: null, text: 'Porfavor seleccione una hora' },
          { value: '8', text: '08:00 AM' },
          { value: '9', text: '09:00 AM' },
          { value: '10', text: '10:00 AM' },
          { value: '11', text: '11:00 AM' },
          { value: '12', text: '12:00 AM' },
          { value: '1', text: '01:00 PM' },
          { value: '2', text: '02:00 PM' },
          { value: '3', text: '03:00 PM' },
          { value: '4', text: '04:00 PM' },
          { value: '5', text: '05:00 PM' }

        ]
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
    },
    user(){
      return this.$store.state.user;
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

span{
  font-weight: bold;
}

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