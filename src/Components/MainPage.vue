<script setup>
import { ref } from 'vue';
const images = import.meta.glob('@/img/*.jpg', { eager: true });
console.log(images);
const imgUrl = Object.values(images).map(img=> img.default);
const currentImage = ref(0);
const smashCount = ref(0);
const passCount = ref(0);

function countSmash() {
    smashCount.value++;
}
function countPass() {
    passCount.value++;
}
function nextImageSmash() {
    currentImage.value = (currentImage.value + 1) % imgUrl.length;
    countSmash();
    console.log(smashCount.value);
}
function nextImagePass() {
    currentImage.value = (currentImage.value + 1) % imgUrl.length;
    countPass();
    console.log(passCount.value);
}
</script>

<template>
    <main>
        <h1>SMASH OR PASS ANIME EDITION !</h1>
        <div class="container-imgbtn">
            <div>
                <img :src="imgUrl[currentImage]" alt="Image" width="300" height="300" />
            </div>
            <div class="buttons">
                <button @click="nextImageSmash" :style="{transform: `scale(${1 + smashCount*0.5})`}">SMASH</button>
                <button @click="nextImagePass" :style="{transform: `scale(${1 + passCount*0.5})`}">PASS</button>
            </div>
        </div>
    </main>
</template>
<style scoped>
main{
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    }
.buttons{
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 20px;
    margin-top: 20px;
}
</style>
