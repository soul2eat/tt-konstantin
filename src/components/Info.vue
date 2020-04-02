<template>
    <div class="info">
        <Device :device="device.info"/>
        <Defects :defects="device.defects"/>
        <History :history="device.history"/>
    </div>
</template>

<script>
import Device from './Device'
import Defects from './Defects'
import History from './History'

export default {
    props: ["device"],
    components: {
        Device,
        Defects,
        History
    }
}
</script>
