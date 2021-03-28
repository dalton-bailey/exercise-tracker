<template>
  <div id="app">
    <h1>Exercise Tracker</h1>
    <!-- <button>Add Workout</button> -->
    <div id="forms">
      <distance-form @add:exercise="addExercise" />
      <rep-form @add:exercise="addExercise" />
    </div>

    <exercise-list
      :exercises="exerciseExercises"
      @delete:exercise="deleteExercise"
      @edit:exercise="editExercise"
    />
  </div>
</template>

<script>
import DistanceForm from "./components/DistanceForm.vue";
import RepForm from "./components/RepForm.vue";
import ExerciseList from "./components/ExerciseList.vue";

export default {
  name: "App",
  components: {
    DistanceForm,
    RepForm,
    ExerciseList,
  },
  data() {
    return {
      exerciseExercises: [],
    };
  },
  methods: {
    addExercise(exercise) {
      const lastID =
        this.exerciseExercises.length > 0
          ? this.exerciseExercises[this.exerciseExercises.length - 1].id
          : 0;
      const id = lastID + 1;

      const newExercise = { ...exercise, id };

      this.exerciseExercises = [...this.exerciseExercises, newExercise];
    },
    deleteExercise(id) {
      this.exerciseExercises = this.exerciseExercises.filter(
        (exercise) => exercise.id !== id
      );
    },
    editExercise(id, updatedExercise) {
      this.exerciseExercises = this.exerciseExercises.map((exercise) =>
        exercise.id === id ? updatedExercise : exercise
      );
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#forms {
  display: flex;
}

#distance-form, #rep-form {
  width: 500px;
}

form {
  display: flex;
  flex-direction: column;
  /* align-items: flex-start; */
}

form input {
  padding: 10px 5px;
  margin: 10px;
}

button {
  background-color: #006381;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 20px;
  text-transform: uppercase;
  margin: 10px;
}

button:hover {
  cursor: pointer;
}
</style>
