<script>
import SvgIcon from '@jamescoyle/vue-icon';
import { mdiTimerSand } from '@mdi/js';
export default {
    components: {
        SvgIcon
    },
    data() {
        return {
            path: mdiTimerSand,
            duration: 0,
        }
    },
    emits: ['duration'],
    methods: {
        emitDuration() {
            if (this.duration >= 0 && this.duration <= 60) {
                this.$emit('duration', this.duration)
            } else {

            }
        }
    }
}
</script>
<template>
    <div class="  rounded bg-slate-300 flex flex-row items-center">
        <svg-icon type="mdi" :path="path"></svg-icon>
        <input v-on:change="emitDuration" v-model="duration"
            class="w-16 h-10  rounded border-none appearance-none p-2 font-medium text-xl " min="0" max="60" type="number">

    </div>
</template>