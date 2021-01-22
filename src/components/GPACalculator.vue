<template>
  <div class="container">

    <!--- Title --->
    <h1>Anwar Vue Practice</h1>

    <!--- Main Form --->
    <form v-on:submit.prevent="handleCalculateGPA">
      <fieldset>
        <legend>GPA Calculator</legend>

        <!--- Error Message --->
        <label v-if="error" class="error">&#9447; One or more course fields are empty.</label>

        <!--- Current GPA Form --->
        <div class="verticalInputContainerRow">

          <div class="verticalInputContainer">
            <label for="GPAcalculator-currentGPA">Current GPA</label>
            <input id="GPAcalculator-currentGPA" name="GPAcalculator-currentGPA" type="text" v-model.number="currentGPA"/>
          </div>

          <div class="verticalInputContainer">
            <label for="GPACalculator-currentCredits">Current Credits</label>
            <input id="GPACalculator-currentCredits" name="GPACalculator-currentCredits" type="text" v-model.number="currentCredits"/>
          </div>

        </div>

        

        <!--- Calculator Headers --->
        <div class="column-header-row">
          <label id="column-header-course-name" class="column-header" >Course Name</label>
          <label id="column-header-grade" class="column-header">Grade</label>
          <label id="column-header-credit" class="column-header">Credit</label>
        </div>
      
        <!--- Course List --->
        <ul>
          <li is="CourseForm" 
            v-for="i in numberOfCourses" 
            v-bind:key="i" 
            v-bind:courseNumber="i" 
            v-bind:isLast="i === numberOfCourses"
            v-on:close-event="handleCloseEvent"
            v-on:change-event="handleChangeEvent"
            v-bind:grade="grades[i-1]"
            v-bind:credit="credit[i-1]"
          />
        </ul>

        <div class="buttons">
          <button id="add-course-button" type="button" v-on:click="handleAddCourse">Add Course</button>
          <button id="calculate-gpa-button" type="submit">Calculate!</button>
        </div>

        <div class="results">
          <label id="result">{{ newGPA }}</label>
        </div>
      </fieldset>
    </form>
  </div>
</template>

<script>
import CourseForm from './CourseForm.vue'
const getNormalizedGrade = (grade) => {
  if(grade >= 95){
    return 5
  }
  if(grade >= 90){
    return 4.75
  }
  if(grade >= 85){
    return 4.5
  }
  if(grade >= 80){
    return 4
  }
  if(grade >= 75){
    return 3.5
  }
  if(grade >= 70){
    return 3
  }
  if(grade >= 65){
    return 2.5
  }
  if(grade >= 60){
    return 2
  }
  return 1
}
export default {
  data: function() {
    return {
      numberOfCourses: 3,
      newGPA: '',
      grades: [NaN, NaN, NaN],
      credit: [NaN, NaN, NaN],
      currentGPA: 0,
      currentCredits: 0,
      error: false,
    }
  },
  name: 'GPACalculator',
  components: {
    CourseForm,
  },
  methods: {
    handleAddCourse: function () {
      this.numberOfCourses = this.numberOfCourses + 1
      this.grades = this.grades.concat(NaN)
      this.credit = this.credit.concat(NaN)
    },
    handleCloseEvent: function() {
      this.numberOfCourses = this.numberOfCourses - 1
      this.grades = this.grades.slice(0, -1)
      this.credit = this.credit.slice(0, -1)
    },
    handleCalculateGPA: function() {
      const valid = 
      this.grades.filter(item => isNaN(item)).length === 0
      && this.credit.filter(item => isNaN(item)).length === 0

      if(!valid){
        this.error = true
        return
      }
      this.error = false

      const reducer = (sum, i) => sum + i
      const temp = this.credit.reduce(reducer)
      const totalCredits = this.currentCredits + temp
      const currentPoints = this.currentGPA * this.currentCredits
      const newPoints = 
        Array(this.numberOfCourses).fill(0).map(
          (_, i) => {
            return getNormalizedGrade(this.grades[i]) * this.credit[i]
          }
        ).reduce(
          (sum, i) => {
            return sum + i
          }, 0
        )
      this.newGPA = ((currentPoints + newPoints)/totalCredits).toFixed(2)
      
      
    },
    handleChangeEvent: function(event, key) {
      if(event.target.name === 'grade'){
        this.grades[key-1] = parseFloat(event.target.value)
      }else{
        this.credit[key-1] = parseFloat(event.target.value)
      }
    }
    
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  ul {
    padding-left: 0;
    margin-top: 0;
  }

  legend { 
    font-weight: bold;
  }


  .results {
    padding-left: 1rem;
  }

  .container {
    width: 24rem;
    margin: auto;
    max-width: 95%;
  }

  .error {
    display: block;
    margin-top: 1rem;
    padding: 1rem;
    background-color: #B00020;
    color: #FFFFFF;
    font-weight: 700;
  }
  .verticalInputContainer {
    display: flex;
    flex-direction: column;
    margin-right: 0.33rem;
  }

  .verticalInputContainer input {
    width: 7rem;
  }
  .verticalInputContainer label {
    font-weight: bold;
    margin-bottom: 0.125rem;
  }

  .verticalInputContainerRow {
    display: flex;
    flex-direction: row;
    align-items: center;
    margin-top: 1rem;
    margin-bottom: 1rem;
  }
  
  .verticalInputContainerRow::after {
    content: "";
    display: block;
    clear: both;
  }

  .column-header-row {
    margin-bottom: 0.125rem;
  }


  .column-header-row::after {
    content: "";
    display: block;
    clear: both;
  }

  .column-header {
    display: block;
    float: left;
    font-weight: bold;
  }
  
  .buttons { 
    margin-bottom: 1rem;
  }

  #column-header-course-name {
    width: 7rem;
    margin-right: 0.8rem;
  }

  #column-header-grade {
    width: 3.1rem;
    margin-right: 1.6rem;
  }

  button {
    position: relative;
    border-radius: 0.125rem;
    border-width: 0;
    outline: none;
    box-shadow: 0 1px 4px rgba(0,0,0,0.6);
    transition: background-color 0.2s;
    padding: 0.75rem 1.5rem;

    font-weight: bold;

    overflow: hidden;
  }

  button:before {
    content: "";

    position: absolute;
    top: 50%;
    left: 50%;

    display: block;
    width: 0;
    padding-top: 0;

    border-radius: 100%;

    background-color: rgba(236, 240, 241, 0.3);

    -webkit-transform: translate(-50%, -50%);
    -moz-transform: translate(-50%, -50%);
    -ms-transform: translate(-50%, -50%);
    -o-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);

  }

  button:active:before {
    width: 120%;
    padding-top: 120%;

    transition: width .2s ease-out, padding-top .2s ease-out;

  }

  #add-course-button {
    background-color: rgb(255, 255, 255, 1);
    color: #00B147;
    margin-right: 1rem;
  }

  #calculate-gpa-button {
    background-color: rgba(0, 229, 117, 1);
  }

  #calculate-gpa-button:hover, #calculate-gpa-button:focus {
    background-color: rgba(0, 229, 117, 0.8);
  }

  #result {
    font-weight: bolder;
    font-size: 3rem;
  }



</style>
