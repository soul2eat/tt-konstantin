<template>
    <div class="defects">
        <div v-for="(val, key) in defects" :key="val.name+key" class="defect">
            <div class="name">{{val.name}}</div>
            <div class="description">
                {{val.value}}
            </div>
        </div>

    </div>
</template>

<script>
export default {
    props: ["defects"]
}
</script>

<style scoped>
    .defects{
        width: 100%;
        margin: 40px 0px;

    }
    .defect{
        width: 258px;
        height: 110px;
        background: #FFFFFF;
        border-radius: 2px;
        margin: 5px 10px;
        display: inline-block;
    }

    .defect > .name{
        font-size: 16px;
        color: rgba(111, 114, 118, 0.66);
        padding: 19px 0px 15px 25px;
    }
    .defect > .description{
        font-size: 17px;
        line-height: 135%;
        color: rgba(0, 0, 0, 0.66);
        margin: 0px 25px;
    }
</style>