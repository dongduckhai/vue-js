<template>
  <b-container>
    <b-card header="Form Submit">
      <b-form @submit.prevent="onSubmit">

        <b-form-group label="Name:">
          <b-form-input v-model="form.name" placeholder="Enter name">
          </b-form-input>
        </b-form-group>

        <b-form-group label="Email address:">
          <b-form-input v-model="form.email" type="email" placeholder="Enter email">
          </b-form-input>
        </b-form-group>

        <b-form-group label="Password:">
          <b-form-input v-model="form.password" type="password">
          </b-form-input>
        </b-form-group>

        <b-form-group label="Gender">
          <b-form-radio v-model="form.gender" name="gender" value="male">Male</b-form-radio>
          <b-form-radio v-model="form.gender" name="gender" value="female">Female</b-form-radio>
          <b-form-radio v-model="form.gender" name="gender" value="other">Other</b-form-radio>
        </b-form-group>

        <b-form-group label="Languages:">
          <b-form-checkbox-group v-model="form.languages" :options="languageList">           
          </b-form-checkbox-group>
        </b-form-group>

        <b-form-group label="Birthday" id="selectDate">
          <b-row>
            <b-col md="4" class="d-flex">
              <b-form-select v-model="form.year" @change="get_days()">
                <option v-for="n in get_quantity_year" :value="n + 1899" :key="n">
                {{ n + 1899 }} 
                </option>
              </b-form-select> 
              <span class="ml-2">YEAR</span>
            </b-col>
            <b-col md="4" class="d-flex">
              <b-form-select v-model="form.month" @change="get_days()">
                <option v-for="n in 12" :value="n" :key="n">
                {{ n }}
                </option>
              </b-form-select>
              <span class="ml-2">MONTH</span>
            </b-col>
            <b-col md="4" class="d-flex">
              <b-form-select v-model="form.day">
                <option v-for="n in form.days_max" :value="n" :key="n">
                {{ n }} 
                </option>
              </b-form-select>
              <span class="ml-2">DAYS</span>
            </b-col>
          </b-row>
        </b-form-group>

        <b-form-group label="Avatar:"   >
          <b-form-file v-model="form.avatar" placeholder="Choose a file or drop it here..." >
        </b-form-file>
        </b-form-group>
        

        <b-form-textarea class="mb-3"  v-model="form.note" placeholder="Note something..." rows="3" max-rows="6">         
        </b-form-textarea>

        <b-button type="submit" variant="success">Submit</b-button>
      </b-form>
    </b-card>
  </b-container>
</template>

<script>
import languageList from './const/languages';
export default {
  name: "app",
  data() {
    return {
      form: {
        name: "",
        email: "",
        password: "",
        gender: null,
        languages: [],
        avatar: null,
        note: "",
        year: 1900,
        month: 1,
        day: 1,
        days_max: '',
      },
      languageList: languageList
    };
  },
  created() {
    this.get_days();
  },
  computed: {
    get_quantity_year() {
      let currentYear = new Date().getFullYear();
      return parseInt(currentYear) - 1900 + 1;
    } 
  },
  methods: {
    onSubmit(event) {
      console.log(this.form.name)
      console.log(this.form.email)
      console.log(this.form.password)
      console.log(this.form.gender)
      console.log(this.form.languages)
      let birthday = new Date(this.form.year, this.form.month, this.form.day)
      console.log(birthday.toLocaleDateString())
      console.log(this.form.note)
    },     
    get_days(){
      this.form.days_max = new Date(this.form.year, this.form.month, 0).getDate(); 
    },
  },
};
</script>
<style>
.card-header {
  text-align: center;
  color: white;
  background-color: #28a745;
}
.container {
  margin: 20px auto;
  width: 700px;
}
</style>