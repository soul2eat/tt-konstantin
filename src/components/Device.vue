<template>
    <div class="device-info">
        <div class="description">
            <div class="top">
                <span>УСТРОЙСТВО</span>
                <a href="">Изменить</a>
            </div>
            <div v-for="(val, key) in device" :key="key" class="list">
                <span class="name">{{key}}</span>
                <span class="value">{{val}}</span>
            </div>
            <!-- <div class="list">
                <span class="name">ТИП</span>
                <span class="value">Apple (Mobile)</span>
            </div>
            <div class="list">
                <span class="name">НАЗВАНИЕ</span>
                <span class="value">Apple iPhone 5s 16GB 2 строка при необход.</span>
            </div>
            <div class="list">
                <span class="name">ЦВЕТ</span>
                <span class="value">Silver</span>
            </div>
            <div class="list">
                <span class="name">ОБЪЕМ</span>
                <span class="value">16 Gb</span>
            </div> -->

        </div>
        <div class="barcode">
            <img id="barcode"/>
            <div>
                <input @click="print" type="button" value="Печать штрихкода">
            </div>
        </div>
    </div>
</template>

<script>
import JsBarcode from "jsbarcode"

export default {
    props: ["device"],
    methods: {
        barCode(){
            const { device}  = this;
            JsBarcode("#barcode", (device.SN || device.IMEI), {background: "#048ce600", displayValue: false});
        },
        print(){
            const barcode = document.getElementById('barcode');
            const printWindow = window.open();
            
            if(!printWindow){
                return alert("Ошибка при печати!");
            }

            printWindow.document.write('<img src="' + barcode.src + '">');
            printWindow.print();
        }
    },
    mounted(){
        this.barCode();
    },
    watch: {
        device(){
            this.barCode();
        }
    }
}
</script>

<style scoped>
    .device-info{
        margin: 40px;
        display: flex;
    }
    .description > div{
        margin-bottom: 15px;
    }

    .description{
        flex: 2;
    }
    .description  .top span{
        font-weight: bold;
        font-size: 16px;
        color: rgba(0, 0, 0, 0.45);
        padding-right: 15px;
    }

    .description  .top a{
        text-decoration: none;
        color: rgba(23, 121, 192, 0.87);
        font-size: 14px;
    }
    .list{
        display: flex;
    }
    .list .name{
        font-size: 11px;
        font-weight: bold;
        color: #9EA1A4;
        flex: 1;
        line-height: 25px;
        padding-right: 5px;
    }
    .list .value{
        color: rgba(0, 0, 0, 0.77);
        font-weight: 500;
        font-size: 17px;
        flex: 6
    }

    .barcode{
        flex: 1;
        padding-top: 20px;
    }
    .barcode img, .barcode > div{
        width: 170px;
    }
    .barcode input{
        background: #FFFFFF;
        box-shadow: 0px 14px 21px rgba(95, 104, 111, 0.06);
        border-radius: 2px;
        font-weight: 500;
        font-size: 14px;
        line-height: 16px;
        color: rgba(90, 101, 109, 0.87);
        width: 100%;
        height: 35px;
        border: none;
        cursor: pointer;
    }


</style>