<template>
    <div class="box" :class="{active: isActive === true}" @click="handleClick">
       <h3 v-if="isActive">Click me!</h3> 
       <h3 v-else>Wait until I become red</h3>
    </div>
    
</template>

<script>
export default {
    mounted() {
        this.startTimer = Date.now();
        this.waitTime = Math.round(1000 + Math.random() * 2000);
        setTimeout(() => {
            this.isActive = true;
        }, this.waitTime)
    },
    data() {
        return {
            userShouldClick: false,
            startTimer: 0,
            isActive: false, 
            waitTime: 0,
        }
    },
    methods: {
        handleClick() {
            const resultTime = Date.now() - this.startTimer - this.waitTime 
            if(this.isActive) this.$emit("clickedOnTime",resultTime)
            else this.$emit("clickedEarly");
        }
    }
}
</script>

<style scoped>
.active {
    background-color: #DC2626 !important;
    color: white;
}
</style>