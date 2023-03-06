<template>
    <form @submit.prevent="handleSubmit">
        <label>Email</label>
        <input type="email" v-model="email" name="email" required>

        <label>Password</label>
        <input type="password" v-model="password" name="password" required>
        <div v-if="passwordError">
            {{ passwordError }}
        </div>

        <label>Role</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <label>Skills:</label>
        <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
        <div v-for="skill in skills" :key="skill" class="pill" @click="removeSkill(skill)">
            {{ skill }}
        </div>

        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <label>Accept terms and condition</label>
        </div>

        

        <button type="submit">Submit</button>
    </form>
</template>

<script>
    export default {
        data() {
            return {
                email: '',
                password: '',
                role: 'developer',
                terms: false,
                tempSkill: '',
                skills: [],
                passwordError: ''
            }
        },
        methods: {
            addSkill(e) {
                if(e.key === ";" && this.tempSkill) {
                    if(!this.skills.includes(this.tempSkill)) {
                        this.skills.push(this.tempSkill)
                    }
                    this.tempSkill = ""
                }
            },
            removeSkill(skill) {
                this.skills = this.skills.filter((item) => {
                    return skill !== item
                })
            },
            handleSubmit() {
                //validate password
                this.passwordError = this.password.length > 5 ? '' : 'Password must be atleast 6 chars long'
                if(!this.passwordError) {
                    console.log('Hooray!')
                }
            
            }
        }
    }
</script>

<style>
    form {
        max-width: 410px;
        margin:30px auto;
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
    }

    input, select {
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

    .pill {
       display: inline-block;
       margin: 20px 10px 0 0;
       padding: 6px 12px;
       background: #eee;
       border-radius: 20px;
       font-size: 12px;
       letter-spacing: 1px;
       font-weight: bold;
       color: #777;
       cursor: pointer; 
    }
</style>