<script>
export default {
    props: ['pagestatus','userName'],
    emits: ['user-name'],
    data(){
        return{
            uname: ""
        }
    },
    methods: {
        setUsername(x){
            this.$emit('user-name', x);
        }
    }
}
</script>

<template>
<div>
    <h1>MemoryGame</h1>
    <h3>Menu</h3>
    <div v-if="(userName == '')" style="width: 300px">
        <form>
        Username: <input v-model="uname" type="text" required/><br>
        <button type="submit" @click="setUsername(uname)" style="float:right">Join</button>
        </form>
    </div>
    <div v-else>
        <p>Hi {{ userName }}!</p><br>
        <button @click="$emit('pageS',1)">Play</button>
        <button @click="$emit('pageS',2)">Score</button>
        <button @click="$emit('user-name','')">Exit</button>
    </div>
</div>
</template>