<template>
  <b-container>
    <h2>Nueva cita del paciente <span>{{user.name}}</span></h2>
    <h2 class="post_header"></h2>
    <br>
    <br>
      <b-form @submit.prevent="agendarCita">
        <b-row>
          <b-col md="6">
            <label for="example-datepicker">Por favor, elija una fecha</label>
            <b-form-datepicker required  v-model="value_date" :date-disabled-fn="dateDisabled"></b-form-datepicker>
          </b-col>  
          <b-col md="6">
            <label for="example-datepicker-2">Ahora, seleccione una hora de atención</label>
            <b-form-select required class="validate" v-model="selected_hour" :options="options"></b-form-select>
          </b-col>  
          <br>
          <br>
          <br>
          <b-col md="12" sm="12">
            <b-form-textarea
              required class="validate"
              id="textarea"
              maxlength="20"
              v-model="text_area_sintoma"
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
            <button type="submit" class="btn btn-success">Agendar cita</button>  
          </b-col>
        </b-row>
      </b-form>
  </b-container>
</template>

<script>
import { db } from '../firebase'; 
import firebase from 'firebase/app';
 


export default {
  data() {
    return {
      text_area_sintoma:'',
      value_date:'',
      selected_hour: null,
      options: [

          { value: null, text: 'Porfavor seleccione una hora' },
          { value: '08:00 AM', text: '08:00 AM' },
          { value: '09:00 AM', text: '09:00 AM' },
          { value: '10:00 AM', text: '10:00 AM' },
          { value: '11:00 AM', text: '11:00 AM' },
          { value: '12:00 PM', text: '12:00 PM' },
          { value: '01:00 PM', text: '01:00 PM' },
          { value: '02:00 PM', text: '02:00 PM' },
          { value: '03:00 PM', text: '03:00 PM' },
          { value: '04:00 PM', text: '04:00 PM' },
          { value: '05:00 PM', text: '05:00 PM' }

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
  },
  methods: {
    dateDisabled(ymd, date) {
      // Disable weekends (Sunday = `0`, Saturday = `6`) and
      // disable days that fall on the 13th of the month
      const weekday = date.getDay()
      // Return `true` if the date should be disabled
      return weekday === 0 || weekday === 6 
    },
    
    agendarCita(){
      const user = firebase.auth().currentUser;
      db.collection("citas_dostor").add({
        fecha: this.value_date,
        hora: this.selected_hour,
        nombre: user.displayName,
        sintoma: this.text_area_sintoma
        
      });
      // reset values
      this.value_date = "";
      this.selected_hour = null;
      this.text_area_sintoma = '';

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