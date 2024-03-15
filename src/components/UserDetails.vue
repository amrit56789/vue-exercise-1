<template>
<div>
    <p>Name: {{ name }}</p>
    <p>Address: {{ address }}</p>
    <p>DOB: {{ dob }}</p>
    <button @click="calculateAge">Calculate Age</button>
    <p>Age: {{ calculatedAge }}</p>
    <button @click="checkAge">Check Age for Website Use</button>
    <p v-if="ageMessage" :class="{'error': isUnderage}">{{ ageMessage }}</p>
</div>
</template>

  
  
<script>
export default {
    name: 'UserDetails',
    props: {
        name: String,
        address: String,
        dob: String,
    },
    data() {
        return {
            calculatedAge: null,
            ageMessage: '',
            isUnderage: false,
        };
    },
    methods: {
        calculateAge() {
            const dob = new Date(this.dob);
            const diff = Date.now() - dob.getTime();
            const ageDate = new Date(diff);
            this.calculatedAge = Math.abs(ageDate.getUTCFullYear() - 1970);
        },
        checkAge() {
            if (this.calculatedAge < 18) {
                this.ageMessage = 'You are under age.';
                this.isUnderage = true;
            } else {
                this.ageMessage = 'You are ok to use the website.';
                this.isUnderage = false;
            }
        }
    }
}
</script>
  
  
<style scoped>
.error {
    color: red;
}
</style>
