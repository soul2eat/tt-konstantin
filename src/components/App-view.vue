<template>
    <div class="content">
        <Header/>
        <Search v-on:setDevice="device = $event" />
        <Info v-if="device" :device="device" />
    </div>
</template>

<script>
import Header from './Header'
import Search from './Search'
import Info from './Info'

export default {
    name: "App-view",
    data(){
        return {
            device: null
        }
    },
    components: {
        Header,
        Search,
        Info
    }
}
</script>

<style scoped>
    .content{
        padding: 0px 40px;
        flex: 1;
    }
    .content > div{
        margin: 40px 0px;
    }
</style>