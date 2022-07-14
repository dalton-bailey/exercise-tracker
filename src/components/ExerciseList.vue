<template>
  <div id="exerciseList-table">
    <h2>Exercises</h2>
    <p v-if="distanceExercises.length < 1">There are no exercises</p>
    <table v-else>
      <!-- <thead>
        <tr>
          <th>Type</th>
          <th>Time</th>
          <th>Distance</th>
        </tr>
      </thead> -->
      <tbody>
        <tr v-for="exercise in distanceExercises" :key="exercise.id">
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
            <button @click="editDistanceExercise(exercise)">Save</button>
            <button @click="cancelDistanceEdit(exercise)">Cancel</button>
          </td>

          <td v-else>
            <button @click="editDistanceMode(exercise)">Edit</button>
            <button @click="$emit('delete:exercise', exercise.id)">
              Delete
            </button>
          </td>

        </tr>


        <tr v-for="repExercise in repExercises" :key="repExercise.id">
          <td v-if="editing === repExercise.id">
             <input v-model="repExercise.type" type="text" />
          </td>
          <td v-else>{{ repExercise.type }}</td>

          <td v-if="editing === repExercise.id">
            <input v-model="repExercise.sets" type="number" />
          </td>
          <td v-else>{{ repExercise.sets }}</td>

          <td v-if="editing === repExercise.id">
            <input v-model="repExercise.reps" type="number" />
          </td>
          <td v-else>{{ repExercise.reps }}</td>

          <td v-if="editing === repExercise.id">
            <button @click="editExercise(repExercise)">Save</button>
            <button @click="cancelEdit(repExercise)">Cancel</button>
          </td>

          <td v-else>
            <button @click="editMode(repExercise)">Edit</button>
            <button @click="$emit('delete:exercise', repExercise.id)">
              Delete
            </button>
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
    distanceExercises: Array,
    repExercises: Array,
  },

  data() {
    return {
      editing: null,
      cachedExercise: null,
    };
  },
  methods: {
    editDistanceMode(exercise) {
      this.cachedExercise = Object.assign({}, exercise);
      this.editing = exercise.id;
    },
    editDistanceExercise(exercise) {
      if (
        exercise.type === "" ||
        exercise.time === "" ||
        exercise.distance === "" 
      )
        return;

      this.$emit("edit:exercise", exercise.id, exercise);

      this.editing = null;
    },
    cancelDistanceEdit(exercise) {
      Object.assign(exercise, this.cachedExercise);
      this.editing = null;
    },
  },
};
</script>

<style scoped>
</style>