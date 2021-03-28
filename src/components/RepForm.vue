<template>
  <div id="rep-form">
    <form @submit.prevent="handleSubmit">
      <!-- <label>Exercise</label> -->
      <h2>Reps Exercise</h2>
      <input
        v-model="exercise.type"
        type="text"
        :class="{ 'has-error': submitting && invalidExercise }"
        @focus="clearStatus"
        placeholder="Exercise"
      />
      <!-- <label>Sets</label> -->
      <input
        v-model="exercise.sets"
        type="number"
        :class="{ 'has-error': submitting && invalidAmount }"
        @focus="clearStatus"
        placeholder="Sets"
      />
      <!-- <label>Reps</label> -->
      <input
        v-model="exercise.reps"
        type="number"
        :class="{ 'has-error': submitting && invalidAmount }"
        @focus="clearStatus"
        placeholder="Reps"
      />
      <!-- <label>Weight</label> -->
      <input
        v-model="exercise.weight"
        type="number"
        :class="{ 'has-error': submitting && invalidAmount }"
        @focus="clearStatus"
        placeholder="Weight"
      />
      <button>Add Exercise</button>
      <p v-if="error && submitting" class="error-message">
        Please fill out all fields
      </p>
      <p v-if="success" class="success-message">Succesfully added</p>
    </form>
  </div>
</template>

<script>
export default {
  name: "RepsForm",
  data() {
    return {
      exercise: {
        type: "",
        sets: "",
        reps: "",
        weights: "",
      },
      submitting: false,
      error: false,
      success: false,
    };
  },
  methods: {
    handleSubmit() {
      this.submitting = true;
      this.clearStatus();

      if (this.invalidExercise || this.invalidAmount) {
        this.error = true;
        return;
      }

      this.$emit("add:exercise", this.exercise);
      this.exercise = {
        name: "",
        amount: "",
      };

      this.error = false;
      this.success = true;
      this.submitting = false;
    },
    clearStatus() {
      this.success = false;
      this.error = false;
    },
  },
  computed: {
    invalidExercise() {
      return this.exercise.name === "";
    },
    invalidAmount() {
      return this.exercise.amount === "";
    },
  },
};
</script>

<style>
.error-message {
  color: red;
}

.success-message {
  color: green;
}
</style>
