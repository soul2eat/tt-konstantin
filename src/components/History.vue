<template>
    <div class="history">
        <div class="top">ИСТОРИЯ</div>
        <table>
            <tbody>
                <tr v-for="(val, key) in history" :key="key">
                    <td>{{val[0]}}</td>
                    <td>{{val[1]}}</td>
                    <td>{{val[2]}}</td>
                </tr>
            </tbody>    
        </table>
    </div>
</template>

<script>
export default {
    props: ["history"]
}
</script>

<style scoped>

    .history{
        background: #FFFFFF;
        border-radius: 2px;
        margin: 80px 0px;
        padding: 30px;
    }
    .history .top{
        color: rgba(0, 0, 0, 0.45);
        font-weight: bold;
        font-size: 16px;
        line-height: 19px;
        padding-bottom: 20px;
    }
    .history table{
        width: 100%;
        color: rgba(0, 0, 0, 0.77);
        font-size: 14px;
        border-collapse: collapse;
    }
    .history table tr{
        border-collapse: collapse;
        border-bottom: 1px solid rgba(0, 0, 0, 0.15);
    }
    .history table tr > td{
        padding: 8px 0px;
    }
    .history table  tr > td:first-child{
        padding-right: 40px;
    }    
    .history table  tr > td:last-child{
        padding-left: 200px;
    }
</style>