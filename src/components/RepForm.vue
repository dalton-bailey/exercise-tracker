<template>
  <div id="rep-form">
    <form @submit.prevent="handleSubmit">
      <h2>Reps Exercise</h2>
      <label>Exercise</label>
      <input
        v-model="repExercise.type"
        type="text"
        :class="{ 'has-error': submitting && invalidType }"
        @focus="clearStatus"
        placeholder="Type"
      />
      <label>Sets</label>
      <input
        v-model="repExercise.sets"
        type="number"
        :class="{ 'has-error': submitting && invalidSets }"
        @focus="clearStatus"
        placeholder="Sets"
      />
      <label>Reps</label>
      <input
        v-model="repExercise.reps"
        type="number"
        :class="{ 'has-error': submitting && invalidReps }"
        @focus="clearStatus"
        placeholder="Reps"
      />
      <label>Weight</label>
      <input
        v-model="repExercise.weight"
        type="number"
        :class="{ 'has-error': submitting && invalidWeight }"
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
  name: "RepForm",
  data() {
    return {
      repExercise: {
        type: "",
        sets: "",
        reps: "",
        weight: "",
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

      if (this.invalidType || this.invalidSets || this.invalidReps || this.invalidWeight) {
        this.error = true;
        return;
      }


      this.$emit("add:repExercise", this.repExercise);
      this.repExercise = {
        type: "",
        sets: "",
        reps: "",
        weight: "",
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
    invalidType() {
      return this.repExercise.name === "";
    },
    invalidSets() {
      return this.repExercise.sets === "";
    },
    invalidReps() {
      return this.repExercise.reps === "";
    },
    invalidWeight() {
      return this.repExercise.weight === "";
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
