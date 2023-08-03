<template>
    <div>
        <form @submit.prevent="handleSubmit">
            <label>Email</label>
            <input type="email" required v-model="email">

            <label>Password</label>
            <input type="password" required v-model="password">
            <div v-if="passwordError" class="error">{{ passwordError }}</div>

            <label>Role</label>
            <select v-model="role" name="selector" id="selector">
                <option value="Web Developer">Web Deveolper</option>
                <option value="Backend Developer">Backend Developer</option>

            </select>

            <div class="terms">
                <input type="checkbox" v-model="terms" required>
                <label>Accept terms and service</label>
            </div>

            <div>
                <input type="checkbox" value="male" v-model="gender">
                <label>Male</label>
                <input type="checkbox" value="female" v-model="gender">
                <label>Female</label>

            </div>

            <label>Skills</label>
            <input type="text" v-model="tempSkill" @keyup.alt="addSkill" placeholder="Enter a skill here  Alt + , to add the skill">
          
            <div class="skills" v-for="skill in skills" :key="skill" @click="deleteSkill(skill)">
                {{ skill }}
            </div>

            <div class="submit">
                <button> Create an Account
                </button>
            </div>


        </form>


    </div>
</template>
<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: '',
            terms: false,
            gender: [],
            tempSkill: '',
            skills: [],
            passwordError: '',
        }
    },

    methods: {
        addSkill(e) {

            if (e.key === ',' && this.tempSkill.length > 1 && !this.skills.includes(this.tempSkill)) {
                this.skills.push(this.tempSkill);
                this.tempSkill = '';

            }

        },

        deleteSkill(skill) {
            const index = this.skills.findIndex(s => s === skill);
            if (index !== -1) {
                this.skills.splice(index, 1);
            }

        },

        handleSubmit() {
            this.passwordError = this.password.length > 5 ? "" : "Password must be at least 6 characters"

            if (!this.passwordError) {
            console.log("form submitted")
            console.log("Email: ", this.email)
            console.log("Password: ", this.password)
            console.log("Terms accepted: ", this.terms)
            console.log("Gender: ", this.gender)
            console.log("Skills: ", this.skills)


            }
        }
    }

}
</script>
<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;

}


label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
    margin-right: 10px;
}

input,
select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}

.skills {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    color: #777;
    cursor: pointer;
    font-weight: bold;
}


button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    color: white;
    border-radius: 20px;
    font-weight: bold;
    letter-spacing: 1px;
}

.submit {
    margin-top: 20px;
    text-align: center;
}

.error {
    color:red;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    margin-top: 10px;
    
    
}


</style>