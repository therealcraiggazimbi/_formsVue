<template>
  <form @submit.prevent="_handleSubmit">
    <label> Email: </label>
    <input type="email" v-model="_email" />

    <label> Password: </label>
    <input type="password" v-model="_password" />
    <label>Role</label>
    <select v-model="_role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label for="">Skills</label>
    <input type="text" v-model="_tempSkills" @keyup="_addSkill" />
    <div v-for="skill in _skills" :key="skill" class="pill">
      <span @click="_deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="_terms" />
      <label>Accept Terms &amp; Conditions</label>
    </div>

    <div class="submit">
      <button>Ceate an Account</button>
    </div>
  </form>
  <p>{{ _email }}</p>
  <p>{{ _password }}</p>
  <p>{{ _role }}</p>
  <p>{{ _terms }}</p>
</template>

<script>
export default {
  data() {
    return {
      _email: "",
      _password: "",
      _role: "",
      _terms: false,
      _tempSkills: "",
      _skills: [],
    };
  },

  methods: {
    _addSkill(e) {
      if (e.key === "," && this._tempSkills) {
        if (!this._skills.includes(this._tempSkills)) {
          this._skills.push(this._tempSkills);
          this._tempSkills = "";
        }
      }
    },

    _deleteSkill(skill) {
      this._skills = this._skills.filter((item) => {
        return item !== skill;
      });
    },

    _handleSubmit() {
      console.log("submite");
    },
  },
};
</script>

<style scoped>
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
