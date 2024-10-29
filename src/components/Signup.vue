<template>
  <form @submit.prevent="handleSubmit">
    <label>Email :</label>
    <input type="email" required v-model="email" />

    <label>Password :</label>
    <input type="password" required v-model="password" />
    <div class="error" v-if="passwordError">{{ passwordError }}</div>

    <label>Role : </label>
    <select v-model="role">
      <option value="web designer">web Designer</option>
      <option value=" web developer">web developer</option>
    </select>

    <label>Skills (press alt + comma to add):</label>
    <input type="text" v-model="tempSkills" @keyup.alt="addSkills" />
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="deleteSkills(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label>Accept Terms and Conditions</label>
    </div>

    <div class="submit">
      <button>Create an account</button>
    </div>
  </form>
  <div>
    <h5>Email    {{ email }}</h5>
    <h5>password {{ password }}</h5>
    <h5>role     {{ role }}</h5>
    <h5>skills   {{ tempSkills }}</h5>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: "",
      skills: [],
      tempSkills: "",

      passwordError: null,
    };
  },
  methods: {
    addSkills($event) {
      if ($event.key === "," && this.tempSkills) {
        if (!this.skills.includes(this.tempSkills)) {
          this.skills.push(this.tempSkills);
        }
        this.tempSkills = "";
      }
    },
    deleteSkills(skills) {
      this.skills = this.skills.filter((item) => {
        return skills !== item;
      });
    },
    handleSubmit() {
      this.passwordError =
        this.password.length > 5
          ? ""
          : "The password  must be at least 6 characters";
      if (!this.passwordError) {
        console.log("email: ", this.email);
        console.log("password: ", this.password);
        console.log("role: ", this.role);
        console.log("skills: ", this.skills);
        console.log("terms accepted: ", this.terms);
      }
    },
  },
};
</script>

<style>
form {
  width: 700px;
  margin: 10px 150px;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.9em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
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
  border-radius: 20px;
  padding: 10px;
  color: white;
  font-weight: bold;
  font-size: 1em;
  background-color: blue;
  margin-left: 40px;
}
</style>
