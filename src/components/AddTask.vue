<template>
<form @submit="onSubmit" class="add-form">
    <div class="form-control">
        <input type="text" name="text" class="input" placeholder="" required="task" v-model="text" >
        <label class="label">Task</label>
    </div>
    <div class="form-control">
        <input type="text" name="day" class="input" required="day and time" placeholder="" v-model="day">
        <label class="label">Day and Time</label>
    </div>
    <div class="form-control form-control-check">
        <label>Set Reminder</label>
        <input type="checkbox" name="reminder" v-model="reminder">
    </div>
    <input  type="submit" value="Save Task" class="btn btn-block ">
</form>
</template>

<script>
export default {
    name: 'AddTask',
    props: {
        show: Boolean,
    },
    data() {
        return {
            text: '',
            day: '',
            reminder: false
        }
    },
    methods: {
        onSubmit(e) {
            e.preventDefault();
            
            if(!this.text || !this.day) {
                alert('please add a task')
                
                return
            } 
            const newTask = {
                /* id: Math.floor(Math.random() * 100000), */
                text: this.text,
                day: this.day,
                reminder: this.reminder
            }
            this.$emit('add-task', newTask)
            this.text = '',
            this.day = '',
            this.reminder = false
        }
    }
}
</script>

<style scoped>
.add-form {
margin-bottom: 40px;
}

.form-control {
margin: 20px 0;
}

.form-control input {
width: 100%;
height: 40px;
margin: 5px;
padding: 3px 7px;
font-size: 17px;
}

.form-control-check {
display: flex;
align-items: center;
justify-content: space-between;
}

.form-control-check label {
flex: 1;
}

.form-control-check input {
flex: 2;
height: 20px;
}

.label {
position: relative;
	bottom: 2.1rem;
	left: 3rem;
    padding: 2px;
}

.input:hover {
border: 2px solid rgb(18, 15, 239);
}
.input:focus ~ .label, 
.input:valid ~ .label  {
    top: -3.5rem;
    background-color: white;
}

</style>
