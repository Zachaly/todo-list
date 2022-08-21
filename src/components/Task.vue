<template>
    <div :class="[task.important ? 'has-background-warning' : 'has-background-light', 'card p-1 mb-2']"
        @dblclick="onDoubleClick">
        <header class="card-header">
            <p class="card-header-title">{{ task.title }}</p>
            <button class="button is-danger m-1" @click="$emit('remove-task', task.id)">
                <span>
                    Remove
                </span>
            </button>
        </header>
        <div class="card-content">
            <div class="card-content">
                <p>{{task.description}}</p>
            </div>
        </div>
        <div class="card-footer">
            <div class="card-footer-item">
                <p class="has-text-left">
                    Started: {{task.startDate}}
                </p>
            </div>
            <div class="card-footer-item">
                <p class="has-text-left">
                    End before: {{task.endDate}}
                </p>
            </div>
        </div>
    </div>
</template>

<script>

export default{
    name: 'TaskItem',
    props:{
        taskProp: Object
    },
    data(){
        return {
            task: null
        }
    },
    created(){
        this.task = this.taskProp
    },
    methods:{
        onDoubleClick(){
            this.task.important = !this.task.important;
        }
    },
    emits: ['remove-task']
}
</script>
