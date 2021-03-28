<template>
  <div id="exerciseList-table">
    <p v-if="exercises.length < 1">There are no exercises</p>
    <table v-else>
      <thead>
        <tr>
          <th>Type</th>
          <th>Time</th>
          <th>Distance</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="exercise in exercises" :key="exercise.id">
          <td v-if="editing === exercise.id">
            <input v-model="exercise.type" type="text" />
          </td>
          <td v-else>{{ exercise.type }}</td>

          <td v-if="editing === exercise.id">
            <input v-model="exercise.time" type="number" />
          </td>
          <td v-else>{{ exercise.time }}</td>

          <td v-if="editing === exercise.id">
            <input v-model="exercise.distance" type="number" />
          </td>
          <td v-else>{{ exercise.distance }}</td>

          <td v-if="editing === exercise.id">
            <button @click="editExercise(exercise)">Save</button>
            <button @click="cancelEdit(exercise)">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(exercise)">Edit</button>
            <button @click="$emit('delete:exercise', exercise.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "ExerciseList",
  props: {
    exercises: Array,
  },
  data() {
    return {
      editing: null,
      cachedExercise: null,
    };
  },
  methods: {
    editMode(exercise) {
      this.cachedExercise = Object.assign({}, exercise);
      this.editing = exercise.id;
    },
    editExercise(exercise) {
      if (exercise.type === "" || exercise.time === "" || exercise.distance === "") return;

      this.$emit("edit:exercise", exercise.id, exercise);

      this.editing = null;
    },
    cancelEdit(exercise) {
      Object.assign(exercise, this.cachedExercise);
      this.editing = null;
    },
  },
};
</script>

<style scoped>
</style>