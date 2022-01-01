<template>
  <div class="course-create-wrapper">
    <div class="course-create-headerText">
      What category best fits the knowledge you'll share?
    </div>
    <h2 class="course-create-subtitle">
      If you're not sure about the right category, you can change it later.
    </h2>
    <form class="course-create-form">
      <div class="course-create-form-group">
        <div class="course-create-form-field">
          <div class="select is-large">
            <select
              @change="emitFormData"
              @blur="$v.form.category.$touch()"
              v-model="form.category"
            >
              <option value="default">Select Category</option>
              <option
                v-for="category in categories"
                :value="category._id"
                :key="category._id"
              >
                {{ category.name }}
              </option>
            </select>
            <div
              v-if="$v.form.category.$error || form.category == 'default'"
              class="form-error"
            >
              <span v-if="!$v.form.category.required" class="help is-danger"
                >Category is required</span
              >
            </div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import { store } from "vuex";
import { required } from "vuelidate/lib/validators";
export default {
  computed: {
    categories() {
      return this.$store.state.category.items;
    },
    isValid() {
      return !this.$v.invalid && this.form.category !== "default";
    },
  },
  data() {
    return {
      form: {
        category: "default",
      },
    };
  },
  validations: {
    form: {
      category: {
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

<style>
option[value="default"] {
  display: none;
}
.help.is-danger {
  text-align: left;
}
</style>
