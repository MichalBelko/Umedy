<template>
  <div>
    <Navbar />
    <Hero />
    <section class="section">
      <div class="container">
        <h1 class="title">Featured Courses</h1>
        <div class="columns">
          <div
            v-for="course in courses"
            :key="courses._id"
            hiddenclass="column is-one-quarter"
          >
            <!-- CARD-ITEM -->
            <CourseCard :course="course" />

            <!-- CARD-ITEM-END -->
          </div>
        </div>
      </div>
    </section>
    <section class="section">
      <div class="container">
        <h1 class="title">Featured Articles</h1>
        <div class="columns">
          <div class="column is-one-quarter">
            <!-- CARD-ITEM -->
            <BlogCard />
            <!-- CARD-ITEM-END -->
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Navbar from "../components/shared/Navbar.vue";
import CourseCard from "../components/CourseCard.vue";
import BlogCard from "../components//BlogCard.vue";
import Hero from "../components/shared/Hero.vue";

import { mapState } from "vuex";

export default {
  components: { BlogCard, Hero, CourseCard, Navbar },
  computed: {
    ...mapState({
      courses: (state) => state.course.items,
    }),
  },
  async fetch({ store }) {
    await store.dispatch("course/fetchCourses");
  },
};
</script>

<style scoped lang="scss">
// Home page
.links {
  padding-top: 15px;
}
</style>
