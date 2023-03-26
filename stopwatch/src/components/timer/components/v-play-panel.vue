<template>
    <div class="play__panel">
        <div class="play__buttons">
            <div 
                class="but play__button" 
                :class="isPlay ? 'pause' : 'play'" 
                @click="pinpoiting($event)"
            >
            </div>
            <div class="but stop__button" @click="stopPlaying()"></div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isPlay: false,
            targetTimer: null
        }
    },
    watch: {
        isPlay(value) {
            value ? 
                this.targetTimer.classList.add('active__timer') :
                this.targetTimer.classList.remove('active__timer')
        }
    },
    methods: {
        pinpoiting(e) {            
            this.targetTimer = e.target.closest(".timer");

            e.target.classList.contains("pause") ? 
                this.$emit('pause') : this.$emit('play');
            this.isPlay = !this.isPlay
        },

        stopPlaying() {
            this.isPlay=false
            this.$emit('stop')
        }
    }
}
</script>
