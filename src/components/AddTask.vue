<template>
    <div class="field">
        <label class="label">Title</label>
        <input class="input" v-model="taskModel.title"/>
    </div>
    <div class="field">
        <label class="label">Description</label>
        <input class="input" v-model="taskModel.description" >
    </div>
    <div class="field">
        <label class="label">Start Date</label>
        <input type="date" class="input" v-model="taskModel.startDate" >
    </div>
    <div class="field">
        <label class="label">End date</label>
        <input type="date" class="input" v-model="taskModel.endDate">
    </div>
    <div class="field">
        <label class="checkbox">
            <input type="checkbox" v-model="taskModel.important">
            Important
        </label>
    </div>
    <div class="field">
        <button class="button is-success" @click="$emit('add-task', taskModel)">Add task</button>
    </div>
</template>

<script>
export default{
    name: 'task-list',
    props:{
        id: Number
    },
    data(){
        const now = new Date();

        let taskModel = {
          id: this.id,
          title: 'New task',
          description: 'description',
          startDate: this.getDateString(now),
          endDate: null,
          important: false
        }
        now.setDate(now.getDate() + 1);
        taskModel.endDate = this.getDateString(now);

        return {
            taskModel: taskModel,
        }
    },
    methods:{
        getDateString(date){
            let nextMonth = 0;
            let day = date.getDate() + 1;
            let month = date.getMonth() + 1 + nextMonth;
            if(month < 10)
                month = '0' + month

            const year = date.getFullYear();
            return `${year}-${month}-${day}`;
        },
    },
    emits: ['add-task']
}
</script>