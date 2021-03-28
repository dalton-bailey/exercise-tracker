<template>
  <div id="distance-form">
    <form @submit.prevent="handleSubmit">
      <h2>Distance Exercise</h2>
      <!-- <label>Exercise</label> -->
      <input
        v-model="exercise.type"
        type="text"
        :class="{ 'has-error': submitting && invalidExercise }"
        @focus="clearStatus"
        placeholder="Exercise"
      />
      <!-- <label>Exercise Time</label> -->
      <input
        v-model="exercise.time"
        type="number"
        :class="{ 'has-error': submitting && invalidAmount }"
        @focus="clearStatus"
        placeholder="Time"
      />
      <!-- <label>Exercise Distance</label> -->
      <input
        v-model="exercise.distance"
        type="number"
        :class="{ 'has-error': submitting && invalidAmount }"
        @focus="clearStatus"
        placeholder="Distance"
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
  name: "DistanceForm",
  data() {
    return {
      exercise: {
        type: "",
        time: "",
        distance: "",
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
