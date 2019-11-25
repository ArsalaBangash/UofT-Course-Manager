<template>
  <div>
    <v-list-item>
      <v-list-item-content>
        <v-list-item-title>{{courseName}}</v-list-item-title>
      </v-list-item-content>

      <v-list-item-content>
        <v-list-item-title>Mark: {{courseMark}}%</v-list-item-title>
      </v-list-item-content>

      <v-list-item-content>
        <v-list-item-title>Exam Date: {{courseExamDate}}</v-list-item-title>
      </v-list-item-content>

      <v-list-item-content>
        <v-list-item-action v-on:click="removeCourse(index)">
          <v-icon>mdi-delete</v-icon>
        </v-list-item-action>
      </v-list-item-content>
    </v-list-item>
  </div>
</template>

<script>
export default {
  name: "course-list-item",
  props: {
    courseName: {
      type: String
    },
    courseMark: {
      type: Number
    },
    courseExamDate: {
      type: Date
    }
  },
  data() {
    return {
      key: "value"
    };
  }
};
</script>

<style>
</style>