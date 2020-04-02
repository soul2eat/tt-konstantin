<template>
    <div class="search">
        <div class="search-input">
            <img src="../assets/search.png">
            <input v-model="text" @keyup.enter="getDevice" type="text" placeholder="Определить устройства по IMEI/SN">
        </div>
        <div class="search-button">
            <input  @click="getDevice" type="button" value="Найти устройство">
        </div>
    </div>
</template>

<script>
import data from "../../data.json"

export default {
    name: "Search",
    data(){
        return {
            text: ''
        }
    },
    methods: {
        getDevice(){
            const { text, Moon, validSN } = this;
            const lowerText = text.toLowerCase();
            if(lowerText.length === 15){
                if(/^[0-9]+$/.test(lowerText) && Moon(lowerText)){
                    const device = this.getDeviceInfo();
                    device.info.IMEI = text;
                    return this.$emit("setDevice", device);
                }else{
                    return alert('Не валидный IMEI!');
                }
            }
            if(lowerText.length >=8 && lowerText.length <= 12){
                const checkSN = validSN(lowerText);
                if(!checkSN){
                    const device = this.getDeviceInfo();
                    device.info.SN = text;
                    return this.$emit("setDevice", device);
                }else{
                    return alert(checkSN);
                }
            }
            alert("Введите IMEI или серийный номер!");

        },
        validSN(sn){
            if(/^\d|o|о/.test(sn)){
                return "SN не может начинатся с цифры и не должен содержать в себе буквы O!";
            }
            if(!/^[a-zA-Z0-9]+$/.test(sn)){
                return "SN  может содержатьв себе только буквы/цифры";
            }
            return false;
        },
        getDeviceInfo(){
            const { randomInteger } = this;

            return {
                info: data.info[randomInteger(0, data.info.length-1)],
                history: data.history.reduce((val, currVal)=>{
                    
                    return randomInteger(0, 1)?[...val, currVal]:val;
                }, []),
                defects: data.defects.reduce((val, currVal)=>{
                    
                    return randomInteger(0, 1)?[...val, currVal]:val;
                }, [])
            };
            
        },
        randomInteger(min, max) {
            let rand = min + Math.random() * (max + 1 - min);
            return Math.floor(rand);
        },
        Moon(imei) {

            const arr = [];

            for(let i = 0; i < imei.length; i++) {
                if(i % 2 === 0) {
                    const m = parseInt(imei[i]) * 2;
                    if(m > 9) {
                        arr.push(m - 9);
                    } else {
                        arr.push(m);
                    }   
                } else {
                    arr.push(parseInt(imei[i]))
                }
            }
            const summ = arr.reduce((a, b) => { return a + b; });
            return Boolean(!(summ % 10));

        }
    }
}
</script>

<style scoped>
    .search{
        display: flex;
    }
    .search-input{
        display: flex;
        flex: 1;
        min-width: 100px;
        background: #FFFFFF;
        border: 0.5px solid #D4D4D4;
        box-sizing: border-box;
        box-shadow: 0px 0px 2px rgba(0, 0, 0, 0.12);
        border-radius: 5px;
        height: 40px;
        line-height: 40px;
        margin-right: 30px;
    }
    .search-input > img{
        padding: 13px 12px;
        width: 12px;
        height: 12px;
    }
    .search-input input{
        font-family: 'Roboto';
        font-style: normal;
        font-weight: normal;
        flex: 1;
        margin: 4px;
        font-size: 14px;
        border: 0px;
    }
    .search-input input::placeholder{
        font-family: 'Roboto';
        font-style: normal;
        font-weight: normal;
        color: rgba(0, 0, 0, 0.33);
        font-size: 14px;
    }
    .search-input input:focus, .search-button input{
        outline: none;
    }

    .search-button{
        line-height: 40px;
    }
    .search-button input{
        width: 150px;
        background: #0089D7;
        box-shadow: 0px 2px 2px rgba(0, 0, 0, 0.24);
        border-radius: 5px;
        border: 0;
        height: 100%;
        font-weight: 600;
        color: #FFFFFF;
    }
    .search-button input:hover{
        cursor: pointer;
    }
</style>