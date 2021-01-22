<template>
  <div class="courseRow">
      <input type="text" id="course-name" name="course-name" placeholder="e.g. CPCS202"/>
      <input type="text" id="grade" name="grade" v-on:input="handleChangeEvent">
      <input type="text" id="credit" name="credit" v-on:input="handleChangeEvent">
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
    button {
        position: relative;
        border-radius: 0.125rem;
        border-width: 0;
        outline: none;
        padding: 0.5rem 1rem;
        background-color: #FFFFFF;
        font-weight: bold;

        overflow: hidden;
    }
    .close {
        border: none;
        padding: 0;
        margin-left: 0.5rem;
    }
    #course-name {
        margin-right: 0.5rem;
        width: 6rem;
    }
    #grade {
        margin-right: 0.5rem;
    }
    .courseRow {
        margin-bottom: 1rem;
    }
    input {
        width: 3.1rem;
    }
</style>