<template>
    <form @submit.prevent="handleSubmit">
        <label>Email: </label>
        <input type="Email" v-model='email' required>
        <label>Password: </label>
        <input type="Password" v-model='password' required>
        <div v-if="passwordError" class="error">Password must be atleast 6 characters long</div>

        <label>Role</label>
        <select v-model="role">
            <option value="admin">Admin</option>
            <option value="user">User</option>
        </select>

        <label>Skills:</label>
        <label>Press alt+enter to add a skill</label>
        <input type="text" v-model="tempskill" @keyup.alt.enter.prevent="addskill">
        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">{{skill}}</span>
        </div>

        <div class="terms">
            <input type="checkbox" v-model='terms' required>
            <label>I agree to the terms and conditions</label>
        </div>

        <div class="submit">
            <button type="submit">Create an Account</button>
        </div>

    </form>
</template>

<script>
export default {
    data(){
        return{
            email: '',
            password: '',
            role:'user',
            terms:false,
            skills: [],
            tempskill: '',
            passwordError: false

        }
    },

    methods:{
        addskill(e){
            if(this.tempskill){
                console.log(e)
                if(!this.skills.includes(this.tempskill))
                    this.skills.push(this.tempskill)
            
                this.tempskill = ''
            }
        },

        deleteSkill(skill){
            this.skills = this.skills.filter(item => item != skill)
        },

        handleSubmit(){
            if(this.password.length < 6){
                this.passwordError = true
            }else{
                this.passwordError = false
            }
        }

    }

}
</script>

<style>

form{
    max-width: 420px;
    margin: 30px auto; 
    background: white;
    text-align: left;
    padding: 40px;  
    border-radius: 10px;  
}

label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px 0;
    font-size: 0.6rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;

}

input,select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color : #555;
}

input[type="checkbox"]{
    display: inline-block;
    width: 16px;
    margin-right: 0 10px 0 0;
    position: relative;
    top:3px;
 

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

button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;

}
.submit {
    text-align: center;
}

.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}


</style>