<template>
  <div class="listOfMealPlansContainer">
    <div
    class="mealPlanInfo"
     v-for="mealPlan in allMealPlans" 
     :key="mealPlan.mealPlanId"
     >
     <div class="meanPlanContainer">
      <h3>{{ mealPlan.name }}</h3>
        <router-link
          :to="{ name: 'mealPlanDetails', params: { id: mealPlan.mealPlanId } }"
          >View Meal Plan Details</router-link
        >
      </div>
    </div>
  </div>
</template>

<script>
import mealService from "../services/MealService";

export default {
  data() {
    return {
      allMealPlans: [],
      userId: this.$store.state.user.id,
    };
  },
  created() {
    console.log("This is the user id: " + this.$store.state.user.id);
    mealService
      .getListOfMealPlans(this.$store.state.user.id)
      .then((response) => {
        if (response.status === 200) {
          this.allMealPlans = response.data;
        }
      });
  },
};
</script>

<style>

.mealPlanInfo{
  margin-left: auto;
  margin-right: auto;
}
.listOfMealPlansContainer {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  
}

.meanPlanContainer {
  justify-content: center;
  align-items: center;
  border: 6px double black;
  width: 300px;
  height: 150px;
  margin-bottom: 25px;
  margin-right: 25px;
  margin-left: 25px;
  background-color: #dee2e4;
}
</style>