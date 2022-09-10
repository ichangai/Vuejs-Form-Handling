<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email">

    <label>Password:</label >
    <input type="password" required v-model="password">
    <div class="error" v-if="passwordError">{{ passwordError }}</div>

    <label for="">Role</label>
    <select v-model="role">
        <option value="developer">Developer</option>
        <option value="engineer">Engineer</option>
    </select>

    <label>Skills</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill">

    <div v-for="skill in skills" :key="skill" class="pill">
     <span @click="deleteSkill(skill)">{{ skill }}</span> 
    </div>

    <div class="terms">
        <input type="checkbox" v-model="terms" required>
        <label for="">Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button> Create An Account </button>
    </div>

  </form>
  <p> <span>Your Email:</span>  {{ email }}</p>
  <p> <span>Your Role: </span> {{ role }}</p>
  <p> <span>Terms:</span> {{ terms }}</p>
</template>

<script>

export default {
    data(){
        return {
            email: '',
            password: '',
            role: 'developer',
            terms: false,
            tempSkill: '',
            skills: [],
            passwordError: '',

        }
    },
    methods: {
      addSkill(e){
        // console.log(e)
        if(e.key === ',' && this.tempSkill){
          if(!this.skills.includes(this.tempSkill)){
            this.skills.push(this.tempSkill)
          }
          this.tempSkill = ''
        }
      },
      deleteSkill(skill){
        this.skills = this.skills.filter((item) => {
          return skill !== item
        })
      },
      handleSubmit(){
        // console.log('form submitted')
        this.passwordError = this.password.length > 5 ? 
        '' : 'Password must be atleast 6 chars long'

        if(!this.passwordError){
          console.log('email: ', this.email),
          console.log('password: ', this.password),
          console.log('role: ', this.role),
          console.log('skills: ', this.skills),
          console.log('terms: ', this.terms)
        }
      }
    }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600&display=swap');
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
      }
      input, select {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
        font-family: 'Poppins', sans-serif;
      }
      input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
      }

      p{
        font-family: 'Poppins', sans-serif;
        margin: 0 0 10 0;
      }

      span{
        font-weight: bold;
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
      button{
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
        font-family: 'Poppins', sans-serif;
      }
      .submit{
        text-align: center;
      }
      .error{
        color: red;
        font-size: 0.8rem;
        font-weight: bold;
        margin-top: 10px;
        font-family: 'Poppins', sans-serif;
      }
</style>