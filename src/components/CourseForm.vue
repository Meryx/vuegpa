<template>
  <div class="course">
      <label>Course #{{ courseNumber }}</label>
      <input type="text"  name="grade" v-on:input="handleChangeEvent">
      <input type="text"  name="credit" v-on:input="handleChangeEvent">
      <button v-if="isLast" v-on:click="$emit('close-event')" class="close" type="button">&#10006;</button>
  </div>

</template>

<script>
export default {
    name: 'CourseForm',
    props: {
        courseNumber: Number,
        isLast: Boolean,
        grade: Number,
        credit: Number,
    },
    methods: {
        handleChangeEvent: function (event) {
            
            if(/\D/.test(event.target.value)){
                event.target.value = event.target.value.slice(0, -1)
                return;
            }
            this.$emit('change-event', event, this.courseNumber)
        }
    }
}
</script>

<style scoped>
    .close{
        width: 20px;
        margin: 0;
        padding: 0;
        height: 20px;

    }
    .course{
        display: flex;
        background-color: #aaaaaa;
        padding: 0.5rem;
        margin: 0  1.5rem 1.5rem 1.5rem;
        align-items: center;
        border-radius: 0.5rem;
    }
    label {
        vertical-align: top;
        width: 5.5rem;
    }
    input {
        background-color: white;
        margin-left: 2rem;
        width: 3.5rem;
        height: 1.5rem;
    }
</style>