<template>
  <section>Filter</section>
  <section>
    <base-card>
    <div class="controls">
        <base-button mode="outline">
            Refresh
        </base-button>
        <base-button :link="true" to="/register">
            Register as Coach
        </base-button>
    </div>
    <ul v-if="hasCoaches">
      <coach-item
        v-for="coach in coaches"
        :key="coach.id"
        :id="coach.id"
        :firstName="coach.firstName"
        :lastName="coach.lastName"
        :rate="coach.hourlyRate"
        :areas="coach.areas"
      >
      </coach-item>
    </ul>
    <h3 v-else>No coaches found.</h3>
    </base-card>
  </section>
</template>

<script>
import { mapGetters } from 'vuex';
import CoachItem from '../../components/coaches/CoachItem.vue';
export default {
  components: {
    CoachItem,
  },
  computed: {
    ...mapGetters('coaches', ['coaches', 'hasCoaches']),
  },
  mounted() {
    console.log('> Coaches List', this.coaches);
  },
};
</script>

<style scoped>

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.controls {
  display: flex;
  justify-content: space-between;
}

</style>