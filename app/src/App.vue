<template>
  <div id="app">
    <v-app dark>
      <v-content>
        <v-container>
          <p class="display-1">My Courses</p>
          <v-text-field
            v-model="courseToAdd"
            clearable
            label="Add Course Code"
            append-outer-icon="mdi-plus"
            @click:append-outer="addCourse"
            @keyup.enter="addCourse"
          ></v-text-field>

          <v-list v-if="courses.length > 0">
            <v-list-item-group v-model="selectedIndex">
              <course-list-item
                v-for="course in courses"
                :key="course"
                :courseName="course.code"
                :courseMark="course.mark"
                :courseExamDate="course.examDate"
                @click="selectedIndex = index"
              />
            </v-list-item-group>
          </v-list>

          <div v-if="selectedIndex >= 0" class="mt-4">
            <manage-course :course="courses[selectedIndex]" />
          </div>
        </v-container>
      </v-content>
    </v-app>
  </div>
</template>

<script>
import CourseListItem from "./components/CourseListItem";
import ManageCourse from "./components/ManageCourse";

export default {
  name: "App",
  components: {
    CourseListItem,
    ManageCourse
  },
  data() {
    return {
      courseToDeleteIndex: -1,
      courseToAdd: "",
      courses: [
        {
          code: "CSC209",
          mark: 50,
          examDate: new Date().toISOString().substr(0, 10)
        },
        {
          code: "CSC263",
          mark: 50,
          examDate: new Date().toISOString().substr(0, 10)
        },
        {
          code: "STA256",
          mark: 50,
          examDate: new Date().toISOString().substr(0, 10)
        }
      ],
      selectedIndex: 0
    };
  },
  methods: {
    addCourse() {
      if (!this.courseToAdd) return;
      this.courses.push({
        code: this.courseToAdd,
        mark: 50,
        examDate: new Date().toISOString().substr(0, 10)
      });
      this.courseToAdd = "";
    },
    removeCourse(courseIndex) {
      if (courseIndex != this.courseToDeleteIndex) {
        this.courseToDeleteIndex = courseIndex;
        return;
      }
      this.courses.splice(courseIndex, 1);
      if (courseIndex == this.selectedIndex) {
        this.selectedIndex = -1;
      }
      this.courseToDeleteIndex = -1;
    }
  }
};
</script>

<style >
.row {
  display: flex;
  align-items: center;
}
</style>
