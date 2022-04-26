<template>
    <div class="home">
        <h1>Home</h1>
        <input type="text" v-model="search">
        <p>search term {{ search }}</p>
        <div v-for="name in matchingNames" :key="name">{{ name }}</div>
        <button @click="handleWatching">Stop watching</button>
    </div>
</template>

<script>
import { ref, computed } from '@vue/reactivity'
import { watch, watchEffect } from '@vue/runtime-core'
export default {
    name: 'Home',
    setup(){
        const search = ref('')
        const names = ref(['mario', 'yoshi', 'luigi', 'toad', 'bowser', 'koopa', 'peach'])

        const matchingNames = computed(() => {
            return names.value.filter((name) => name.includes(search.value))
        })

        const stopWatching = watch(search, () => {
            console.log('watch function run');
        })

        const stopEffect = watchEffect(() => {
            console.log('watcheffect function run', search.value);
        })

        const handleWatching = () => {
            stopWatching()
            stopEffect()
        }

        return{
            search, names, matchingNames, handleWatching
        }
    }
}
</script>

<style>

</style>