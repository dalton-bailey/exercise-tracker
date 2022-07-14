<template>
  <div id="app">
    <h1>Exercise Tracker</h1>
    <div id="forms">
      <distance-form @add:distanceExercise="addDistanceExercise" />
      <rep-form @add:repExercise="addRepExercise" />
    </div>

    <exercise-list
      :distanceExercises="distanceExerciseExercises"
      :repExercises="repExerciseExercises"
      @deleteRep:exercise="deleteRepExercise"
      @editRep:exercise="editRepExercise"
      @deleteDistance:exercise="deleteDistanceExercise"
      @editDistance:exercise="editDistanceExercise"
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
      distanceExerciseExercises: [],
      repExerciseExercises: [],
    };
  },
  methods: {
    addDistanceExercise(distanceExercise) {
      const lastID =
        this.distanceExerciseExercises.length > 0
          ? this.distanceExerciseExercises[this.distanceExerciseExercises.length - 1].id
          : 0;
      const id = lastID + 1;

      const newExercise = { ...distanceExercise, id };

      this.distanceExerciseExercises = [...this.distanceExerciseExercises, newExercise];
    },
    deleteDistanceExercise(id) {
      this.distanceExerciseExercises = this.distanceExerciseExercises.filter(
        (distanceExercise) => distanceExercise.id !== id
      );
    },
    editDistanceExercise(id, updatedExercise) {
      this.distanceExerciseExercises = this.distanceExerciseExercises.map((distanceExercise) =>
        distanceExercise.id === id ? updatedExercise : distanceExercise
      );
    },

    addRepExercise(repExercise) {
      const lastID =
        this.repExerciseExercises.length > 0
          ? this.repExerciseExercises[this.repExerciseExercises.length - 1].id
          : 0;
      const id = lastID + 1;

      const newExercise = { ...repExercise, id };

      this.repExerciseExercises = [...this.repExerciseExercises, newExercise];
    },
    deleteRepExercise(id) {
      this.repExerciseExercises = this.repExerciseExercises.filter(
        (repExercise) => repExercise.id !== id
      );
    },
    editRepExercise(id, updatedExercise) {
      this.repExerciseExercises = this.repExerciseExercises.map((repExercise) =>
        repExercise.id === id ? updatedExercise : repExercise
      );
    },
  },

  
};
</script>

<style>
body {
  display: flex;
  justify-content: center;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  max-width: 1200px;
}

#forms {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

#distance-form,
#rep-form {
  width: 500px;
}

form {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 90%;
  max-width: 100%;
}

form input {
  padding: 10px 5px;
  margin: 2px 0 15px 0;
  width: 97%;
}

button {
  background-color: #006381;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  align-self: flex-end;
  margin-left: 10px;
}

button:hover {
  cursor: pointer;
}
th {
  width: 100px;
  text-align: left;
}
</style>
