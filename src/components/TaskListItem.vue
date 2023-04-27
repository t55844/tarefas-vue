<script>
import SvgIcon from '@jamescoyle/vue-icon';
import { mdiDeleteRestore, mdiCheckboxMarkedCircleAutoOutline } from '@mdi/js';
export default {
    props: {
        task: { id: String, text: String, duration: Number },
    },
    components: {
        SvgIcon
    },
    data() {
        return {
            pathDeleteIcon: mdiDeleteRestore,
            pathCheckIcon: mdiCheckboxMarkedCircleAutoOutline,
            typeActionIconButton: '',
            done: false

        }
    },
    emits: ['taskListEdited'],
    methods: {
        deleteButton() {

            const taskList = JSON.parse(sessionStorage.getItem('taskList'))

            const newTaskList = taskList.filter(task => task.id != this.task.id)
            sessionStorage.setItem('taskList', JSON.stringify(newTaskList))

            this.$emit('taskListEdited', newTaskList)
        },
        completedButton() {
            console.log(this.done)
            this.done = !this.done
        }
    }

}
</script>
<template>
    <li :id="task.id" class="flex flex-row justify-between items-center p-2 bg-slate-500  rounded-lg m-3">
        <div class="flex flex-row justify-between items-center w-3/4 text-white ">
            <p :class="{ done: this.done }"><strong>Task: </strong>{{ this.task.text }}</p>
            <p class=""><strong>Duration: </strong>{{ this.task.duration }} </p>
        </div>
        <div class=" w-1/5 flex flex-row justify-around   items-center">
            <button class=" hover:bg-slate-300 rounded" @click="deleteButton">
                <svg-icon type="mdi" :path="pathDeleteIcon"></svg-icon>
            </button>
            <button class=" hover:bg-slate-300 rounded" @click="completedButton">
                <svg-icon type="mdi" :path="pathCheckIcon"></svg-icon>
            </button>

        </div>

    </li>
</template>
<style>
.done {
    text-decoration: line-through;
}
</style>