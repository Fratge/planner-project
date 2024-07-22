<template>
    <form @submit.prevent="handleChange">
        <label>Title</label>
        <input type="text" v-model="projectTitle" required>
        <label>Details</label>
        <textarea v-model="projectDetails" required></textarea>
        <button>Edit project</button>
    </form>
</template>

<script>
export default {
    props: ['id'],
    data(){
        return{
            projectTitle: null,
            projectDetails: null,
        }
    },
    mounted(){
        fetch('http://localhost:3000/projects/' + this.id)
        .then((response) =>{
            return response.json()
        })
        .then((data) => {
            this.projectTitle = data.title;
            this.projectDetails = data.details;
        })
        .catch((err) => console.log(err));
    },
    methods: {
        handleChange(){
            fetch('http://localhost:3000/projects/' + this.id, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    "title": this.projectTitle,
                    "details": this.projectDetails
                })
            }).then(() => {
                this.$router.push("/");
            }).catch((err) => console.log(err));
        }
    }
}
</script>

<style>

</style>