<template>
    <section>
        <base-card>
            <h2>{{ fullName }}</h2>
            <h3>${{ rate }}/hour</h3>
        </base-card>
    </section>
    <section>
        <base-card>
            <h2>Interested? Reach out now!</h2>
            <base-button link :to="contactLink">Contact</base-button>
        </base-card>
    </section>
    <section>
        <base-card>
            <base-badge v-for="area in areas" :key="area" :type="area" :title="area"></base-badge>
            <p>{{ description }}</p>
        </base-card>
    </section>

    <section>
        <router-view></router-view>
    </section>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
    props: ['id'],
    data() {
        return {
            selectedCoach: null
        }
    },
    computed: {
        ...mapGetters('coaches', ['coaches']),
        fullName() {
            return this.selectedCoach.firstName + ' ' + this.selectedCoach.lastName;
        },
        contactLink() {
            return this.$route.path + '/contact';
        },
        areas() {
            return this.selectedCoach.areas;
        },
        rate() {
            return this.selectedCoach.hourlyRate;
        },
        description() {
            return this.selectedCoach.description;
        }
    },
    created() {
        this.selectedCoach = this.coaches.find(coach => coach.id === this.id);
    }
}
</script>