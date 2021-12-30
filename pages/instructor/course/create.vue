<template>
  <div class="full-page-takeover-window">
    <div class="full-page-takeover-page">
      <Header :title="`Step 1 of 2`" exitLink="/instructor/courses" />
      <div class="full-page-takeover-header-bottom-progress">
        <div
          :style="{ width: progress }"
          class="full-page-takeover-header-bottom-progress-highlight"
        ></div>
      </div>
      <div class="course-create full-page-takeover-container">
        <div class="container">
          <!-- STEP 1 of FORM  -->
          <Step1 v-if="this.activeStep === 1" />
          <!-- STEP 1 END-->
          <!-- STEP 2 of FORM -->
          <Step2 v-if="this.activeStep === 2" />
          <!-- STEP 2 END -->
        </div>
        <div class="full-page-footer-row">
          <div class="container">
            <div class="full-page-footer-col">
              <div v-if="!isFirstStep">
                <a @click.prevent="decrement" class="button is-large"
                  >Previous</a
                >
              </div>
              <div v-else class="empty-container"></div>
            </div>
            <div class="full-page-footer-col">
              <div>
                <button
                  v-if="!isLastStep"
                  @click.prevent="increment"
                  class="button is-large float-right"
                >
                  Continue
                </button>
                <button
                  v-else
                  @click="() => {}"
                  class="button is-success is-large float-right"
                >
                  Confirm
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Step1 from "~/components/instructor/CourseCreateStep1";
import Step2 from "~/components/instructor/CourseCreateStep2";
import Header from "~/components/shared/Header";
export default {
  layout: "instructor",
  components: { Header, Step1, Step2 },
  data() {
    return {
      activeStep: 1,
      steps: [Step1, Step2],
    };
  },
  computed: {
    stepsLength() {
      return this.steps.length;
    },
    isLastStep() {
      return this.activeStep === this.stepsLength;
    },
    isFirstStep() {
      return this.activeStep == 1;
    },
    progress() {
      return `${(100 / this.stepsLength) * this.activeStep}% `;
    },
  },
  methods: {
    increment() {
      this.activeStep++;
    },
    decrement() {
      this.activeStep--;
    },
  },
};
</script>

<style lang="scss">
.float-right {
  float: right;
}
.empty-container {
  width: 1px;
  height: 1px;
}
.course-create {
  &-wrapper {
    margin-top: 60px;
    text-align: center;
  }
  &-headerText {
    font-weight: 500;
    line-height: 1.1;
    margin-top: 21px;
    margin-bottom: 10.5px;
    font-size: 36px;
    font-weight: 300;
  }
  &-subtitle {
    font-size: 24px;
    font-weight: 300;
    margin-top: 21px;
    margin-bottom: 10.5px;
  }
  &-form {
    margin-top: 60px;
    &-group {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    &-field {
      min-width: 552px;
    }
    .select {
      width: 100%;
      > select {
        width: 100%;
      }
    }
  }
}
</style>
