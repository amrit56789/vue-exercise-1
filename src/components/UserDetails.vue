<template>
<div>
    <p>Name: {{ name }}</p>
    <p>Address: {{ address }}</p>
    <p>DOB: {{ dob }}</p>
    <button @click="calculateAge">Calculate Age</button>
    <p v-if="calculatedAge !== null">Age: {{ calculatedAge }}</p><br />
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
div {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 10px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

p {
    font-size: 16px;
    line-height: 1.5;
    color: #333;
    margin-bottom: 12px;
}

button {
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
    transition: background-color 0.3s ease;
    margin-bottom: 15px;
}

button:hover {
    background-color: #0056b3;
}

.error {
    color: red;
}
</style>
