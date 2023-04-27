<script >
import InputBar from './InputBar.vue'
import TaskListItem from './TaskListItem.vue'
import { v4 as uuidv4 } from 'uuid';
export default {
    data() {
        return {
            taskList: JSON.parse(sessionStorage.getItem('taskList')),
        }
    },
    methods: {
        getTaskFromInputBar(newTask) {
            newTask['id'] = uuidv4()
            const newTaskList = [...this.taskList, newTask]
            sessionStorage.setItem('taskList', JSON.stringify(newTaskList))
            this.taskList = JSON.parse(sessionStorage.getItem('taskList'))
        }
    },
    components: {
        InputBar,
        TaskListItem
    }
}

</script>
<template>
    <div class="bg-slate-700 w-full md:w-2/3 lg:w-5/12 h-11/12 md:h-5/6 p-5  rounded-lg  content-center">
        <InputBar @taskToList="(task) => getTaskFromInputBar(task)" />
        <ul>
            <TaskListItem @taskListEdited="(newTaskList) => taskList = newTaskList" v-for="task  in taskList"
                :task="task" />

        </ul>
    </div>
</template>