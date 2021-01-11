<template>
    <div>
        <p> What's your plan today? </p>
        <el-input placeholder="Plan 1" v-model="plans[0]"></el-input>
        <el-input placeholder="Plan 2" v-model="plans[1]"></el-input>
        <el-input placeholder="Plan 3" v-model="plans[2]"></el-input>
        <el-button type="text" @click="submit"> OK! </el-button>
        <p> plan: {{plans[1]}}</p>
    </div>
  
</template>

<script>
export default {
    data() {
        return {
            plans: ['', '', '']
        };
    },
    methods: {
        submit() {
            console.log('Submit!');
        },

    }

}
</script>

<style>

</style>