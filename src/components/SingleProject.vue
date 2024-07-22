<template>
    <div class="project" :class="{projectDone: this.data.complete }">
        <div class="actions">
            <h3 @click="toggleContent">{{ data.title }}</h3>
            <div class="icons">
                <router-link :to="{ name: 'EditProject', params: { id: this.data.id }}">
                    <span class="material-icons">edit</span>
                </router-link>
                <span class="material-icons" @click="deleteProject">delete</span>
                <span class="material-icons" @click="completeProject" :class="{tick: this.data.complete }">done</span>
            </div>
        </div>
        <div class="details" v-if="showContent">
            <p>{{ data.details }}</p>
        </div>
    </div>
</template>
  
<script>
  
export default {
    props:['data'],
    data(){
        return {
            showContent: false,
        }
    },
    methods: {
        toggleContent(){
            this.showContent = !this.showContent;
        },
        deleteProject(){
            fetch('http://localhost:3000/projects/' + this.data.id, {
                method: 'DELETE'
            }).then(() => this.$emit('delete', this.data.id))
        },
        completeProject(){
            fetch('http://localhost:3000/projects/' + this.data.id, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                "complete" : !this.data.complete
                })
            })
            .then(response => {
                return response.json();
            })
            .then(data => {
                this.$emit('complete', this.data.id);
            })
            .catch(error => console.log(err));
        }
    }
}
</script>
  
<style>
.project{
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.5);
    border-left: 4px solid #e90074;
}

.projectDone{
    border-left: 4px solid #5dff5d !important;
}

h3{
    cursor: pointer;
}

.actions{
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.material-icons{
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
}

.material-icons:hover{
    color: #777;
}

.tick{
    color: #5dff5d;
}

</style>