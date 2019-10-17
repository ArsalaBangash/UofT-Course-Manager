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
            append-outer-icon="add"
            @click:append-outer="addCourse"
          ></v-text-field>

          <v-list v-if="courses.length > 0">
            <v-list-item-group v-model="selectedIndex">
              <v-list-item
                @click="selectedIndex = index"
                v-for="(course, index) in courses"
                :key="course"
              >
                <v-list-item-content>
                  <v-list-item-title>{{course.code}}</v-list-item-title>
                </v-list-item-content>

                <v-list-item-content>
                  <v-list-item-title>Mark: {{course.mark}}%</v-list-item-title>
                </v-list-item-content>

                <v-list-item-content>
                  <v-list-item-title>Exam Date: {{course.examDate}}</v-list-item-title>
                </v-list-item-content>

                <v-list-item-content>
                  <v-list-item-action v-on:click="removeCourse(index)">
                    <v-icon v-if="index != courseToDeleteIndex">delete</v-icon>
                    <v-btn v-if="index === courseToDeleteIndex">Sure?</v-btn>
                  </v-list-item-action>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
          <!-- <v-list v-if="courses.length > 0">
            <v-list-tile
              @click="selectedIndex = index"
              v-for="(course, index) in courses"
              :key="course"
            >
              <v-list-tile-content>{{course.code}}</v-list-tile-content>
              <v-list-tile-content>Mark: {{course.mark}}%</v-list-tile-content>
              <v-list-tile-content>Exam Date: {{course.examDate}}</v-list-tile-content>
              <v-list-tile-action v-on:click="removeCourse(index)">
                <v-icon v-if="index != courseToDeleteIndex">delete</v-icon>
                <v-btn v-if="index === courseToDeleteIndex">Sure?</v-btn>
              </v-list-tile-action>
            </v-list-tile>
          </v-list>-->
          <div v-if="selectedIndex >= 0" class="mt-4">
            <span class="display-1">
              Manage {{courses[selectedIndex].code}}
              <v-btn flat icon @click="selectedIndex=-1">
                <v-icon>check</v-icon>
              </v-btn>
            </span>
            <div class="row">
              <!--             <v-btn raised><v-icon left>computer</v-icon>Add Assignment</v-btn> -->
              <p class="title">Mark:</p>
              <v-slider
                class="ml-4"
                v-model="courses[selectedIndex].mark"
                persistent-hint
                thumb-label="always"
              ></v-slider>
            </div>
            <div>
              <!--             <v-btn raised><v-icon left>computer</v-icon>Add Assignment</v-btn> -->
              <p class="title">Exam Date:</p>
              <v-date-picker v-model="courses[selectedIndex].examDate" landscape="true"></v-date-picker>
            </div>
          </div>
        </v-container>
      </v-content>
    </v-app>
  </div>
</template>

<script>
export default {
  name: "App",
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
