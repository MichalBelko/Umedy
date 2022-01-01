<template>
  <div class="course-create-wrapper">
    <div class="course-create-headerText">
      Please choose title of your Course.
    </div>
    <h2 class="course-create-subtitle">
      No worries, you can change title later.
    </h2>
    <form @input="emitFormData" class="course-create-form">
      <div class="course-create-form-group">
        <div class="field course-create-form-field control has-icons-right">
          <TextInputWithCount
            :v="$v.form.title"
            :maxLength="50"
            v-model="form.title"
          />
          <div v-if="$v.form.title.$error" class="form-error">
            <span v-if="!$v.form.title.required" class="help is-danger"
              >Title is required</span
            >
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import TextInputWithCount from "~/components/form/TextInputWithCount";
import { required } from "vuelidate/lib/validators";
export default {
  data() {
    return {
      form: {
        title: "",
      },
    };
  },
  components: { TextInputWithCount },
  computed: {
    isValid() {
      return !this.$v.$invalid;
    },
  },
  validations: {
    form: {
      title: {
        required,
      },
    },
  },
  methods: {
    emitFormData() {
      this.$emit("stepUpdated", { data: this.form, isValid: this.isValid });
    },
  },
};
</script>

<style scoped>
.help.is-danger {
  text-align: left;
}
</style>
