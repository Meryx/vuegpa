<template>
  <div class="calculator">
    <h1>Anwar Vue Practice</h1>
    <h3>GPA calculator</h3>
    <div class="newGPA">
      <label class="normalLabel">Current GPA:</label>
      <input style="border: 1px solid #aaaaaa; width: 10rem;" type="text" v-model.number="currentGPA"/>
      <label v-if="error" class="error">Missing input parameter!</label>
    </div>
    <div class="newGPA">
      <label class="normalLabel">Current credits:</label>
      <input style="border: 1px solid #aaaaaa; width: 10rem;" type="text" v-model.number="currentCredits"/>
    </div>
    <div class="colHeaders">
      <label id="grade">Grade</label>
      <label id="credit">Credit</label>
    </div>
    <CourseForm 
      v-for="i in numberOfCourses" 
      v-bind:key="i" 
      v-bind:courseNumber="i" 
      v-bind:isLast="i === numberOfCourses"
      v-on:close-event="handleCloseEvent"
      v-on:change-event="handleChangeEvent"
      v-bind:grade="grades[i-1]"
      v-bind:credit="credit[i-1]"
    />
    <button type="button" v-on:click="handleAddCourse">Add Course</button>
    <button type="button" v-on:click="handleCalculateGPA">Calculate!</button>
    <div class="results">
      <h3>Results</h3>
      <div class="newGPA">
        <label class="normalLabel">New GPA:</labeL>
        <label class="normalLabel">{{ newGPA }}</label>
      </div>

    </div>
    <div class="ins">
      
      <h3>Instructions</h3>
      <h3>GPA calculator for 5 point systems.  </h3>
          <ul>
            <li>A grade of [95-100] weighs 5</li>
            <li>A grade of [90-94] weighs 4.75</li>
            <li>A grade of [85-89] weighs 4.5</li>
            <li>A grade of [80-84] weighs 4</li>
            <li>A grade of [75-79] weighs 3.5</li>
            <li>A grade of [70-74] weighs 3</li>
            <li>A grade of [65-69] weighs 2.5</li>
            <li>A grade of [60-64] weighs 2</li>
            <li>A grade of [0-59] weighs 1</li>
          </ul>
       
    </div>
    

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
  .ins{
    text-align: left;
    margin-bottom: 2rem;
    margin-top: 0.5rem;
    border: 1px solid black;
  }

  .ins ul {
    padding-left: 2rem;
  }
  .error{
    background-color:#ffcccb;
    padding: 0.5rem;
    margin: 0.5rem;
    border: 3px solid red;
    border-radius: 0.5rem;
    color: red;
    font-weight: bold;
  }

  #grade{
    padding-left: 9.5rem;
  }
  #credit {
    padding-left: 3rem;
  }
  .colHeaders {
    text-align: left;
  }

  .newGPA {
    text-align: left;
    margin-bottom: 1rem;
    
  }

  .normalLabel {
    padding: 1rem;
  }
  .results {
    clear: both;
    align-items: left;
    display: flex;
    flex-direction: column;
    border: 1px solid black;
  }
  .calculator {
    margin: auto;
    max-width: 95%;
    width: 800px;
    overflow: hidden;
  }

  button {
    margin: 1rem;
    float:left;
    background-color: black;
    border-radius: 0.5rem;;
    color: white;
    height: 30px;
    width: 90px;
  }
  h3 { 
    text-align: left;
    padding: 1rem;
  }

</style>
