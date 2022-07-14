<template>
  <div id="distance-form">
    <form @submit.prevent="handleSubmit">
      <h2>Distance Exercise</h2>
      <label>Exercise</label>
      <input
        v-model="distanceExercise.type"
        type="text"
        :class="{ 'has-error': submitting && invalidType }"
        @focus="clearStatus"
        placeholder="Type"
      />
      <label>Time</label>
      <input
        v-model="distanceExercise.time"
        type="number"
        :class="{ 'has-error': submitting && invalidTime }"
        @focus="clearStatus"
        placeholder="Time"
      />
      <label>Distance</label>
      <input
        v-model="distanceExercise.distance"
        type="number"
        :class="{ 'has-error': submitting && invalidDistance }"
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
      distanceExercise: {
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

      if (this.invalidType || this.invalidTime || this.invalidDistance) {
        this.error = true;
        return;
      }

      this.$emit("add:distanceExercise", this.distanceExercise);
      this.distanceExercise = {
        type: "",
        time: "",
        distance: "",
      };

      this.error = false;
      this.success = true;
      this.submitting = true;
    },
    clearStatus() {
      this.success = false;
      this.error = false;
    },
  },
  computed: {
    invalidType() {
      return this.distanceExercise.type === "";
    },
    invalidTime() {
      return this.distanceExercise.time === "";
    },
    invalidDistance() {
      return this.distanceExercise.distance === "";
    }
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
