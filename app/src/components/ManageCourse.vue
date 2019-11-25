<template>
  <div>
    <span class="display-1">
      Manage {{course.code}}
      <v-btn flat icon @click="selectedIndex=-1">
        <v-icon>mdi-check</v-icon>
      </v-btn>
    </span>
    <div class="row">
      <p class="title">Mark:</p>
      <v-slider class="ml-4" v-model="course.mark" persistent-hint thumb-label="always"></v-slider>
    </div>
    <div>
      <p class="title">Exam Date:</p>
      <v-date-picker v-model="course.examDate" landscape="true"></v-date-picker>
    </div>
  </div>
</template>

<script>
export default {
  name: "manage-course",
  props: ["course"]
};
</script>

<style>
</style>