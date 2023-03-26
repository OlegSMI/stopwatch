<template>
    <div class="rectangle timer">
        <TimePanel :time="time"></TimePanel>
        <PlayPanel 
        @play="play()"
        @pause="pause()"
        @stop="stop()"></PlayPanel>
    </div>
</template>

<script>
import { PlayPanel, TimePanel } from './components';
export default {
    components: {
        PlayPanel, TimePanel
    },
    data() {
        return {
            seconds: 0,
            minutes: 0,
            hours: 0,
            time: "0",
            playTimer: null
        }
    },
    methods: {
        play() {
            this.playTimer = setInterval(() => {
                this.seconds+=1
                if(this.checkFull(this.seconds)){
                    this.seconds=0;
                    this.minutes+=1;
                }
                if(this.checkFull(this.minutes)) {
                    this.hours+=1;
                    this.minutes=0;
                    this.seconds=0;
                }
                this.time=this.createTimeString()
            }, 1000)
        },

        pause() {
            clearInterval(this.playTimer)
        },

        stop() {
            clearInterval(this.playTimer);
            this.time = "0";
            this.hours=0;
            this.minutes=0;
            this.seconds=0;
            this.playTimer=null
        },

        checkFull(el) {
            return (el % 60 == 0) && el != 0
        },

        createTimeString() {
            let time;
            if(this.hours>0) {
                time=`${this.hours}:${this.minutes}:${this.seconds}`
            }
            else if(this.minutes>0) {
                time = `${this.minutes}:${this.seconds}`
            }
            else {
                time = `${this.seconds}`
            }
            return time;
        }
    },
}
</script>