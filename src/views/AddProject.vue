<template>
  <form @submit.prevent="pushToDb">
    <label>Title</label>
    <input type="text" v-model="projectTitle" required>
    <label>Details</label>
    <textarea v-model="projectDetails" required></textarea>
    <button>Add project</button>
  </form>
</template>

<script>
export default {
    data(){
        return{
            projectTitle: null,
            projectDetails: null,
        }
    },
    methods: {
        async pushToDb(){
            let project = {
                title: this.projectTitle,
                details: this.projectDetails,
                complete: false,
            }

            fetch('http://localhost:3000/projects', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(project)
            }).then(() => {
                this.$router.push("/");
            }).catch((err) => console.log(err));
        }
    }
}
</script>

<style>
  form {
    background: white;
    padding: 20px;
    border-radius: 10px;
  }
  label {
    display: block;
    color: #252525;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0
  }
  input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
  }
  textarea {
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
  }
  form button {
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: white;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
  }
</style>