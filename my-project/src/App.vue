<script setup>
import { ref } from 'vue'
import { previewBinaryFile } from './assets/utilities' 
const musicPlayer = ref('starting')
console.log(musicPlayer.value)
const onMusic = ref(false)
const playMusic = () => {
  onMusic.value = !onMusic.value
  console.log(musicPlayer.value)
  if (onMusic.value) musicPlayer.value.play()
  else musicPlayer.value.pause()
}
const urlDocFile =ref('') 
const showPicture = ref('') 
const docName = ref('')
const chooseBinaryFile = (event) => { 
// console.log(event.target.value);
// console.log(event.target);
// console.log(event.target.files);
// console.log(event.target.files[0]);
// console.log(event.target.files[0].name);
docName.value = event.target.files[0].name
if(docName.value.endsWith('.pdf') || docName.value.endsWith('.doc')){ 
  urlDocFile.value = previewBinaryFile(event.target.files[0])
}
  else if(docName.value.endsWith('.jpg') || docName.value.endsWith('.png') || docName.value.endsWith('.jpeg')) { 
        showPicture.value = URL.createObjectURL(file);
    }
    return {showPicture , chooseBinaryFile} 
}
</script>

<template>
  <section class="sm:mt-6 lg:mt-8 mt-12 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
<div
    class="my-10 mx-auto max-w-7xl px-4 sm:mt-12 sm:px-6 md:mt-16 lg:mt-20 lg:px-8 xl:mt-28 flex gap-3 lg:flex-justify lg:flex flex-col lg:flex-row">
    <div class="sm:text-center lg:text-left">
        <h1 class="text-4xl tracking-tight font-extrabold text-gray-800 sm:text-5xl md:text-6xl">
            <span class="block xl:inline">Data to enrich your</span>
            <span class="block text-indigo-600 xl:inline">online business</span>
        </h1>
        <p
            class="mt-3 text-base text-gray-500 sm:mt-5 sm:text-lg sm:max-w-xl sm:mx-auto md:mt-5 md:text-xl lg:mx-0">
            Anim aute id magna aliqua ad ad non deserunt sunt. Qui irure qui lorem cupidatat commodo. Elit sunt amet
            fugiat veniam occaecat fugiat aliqua.
        </p>
        <!-- Button Section -->
        <div class="mt-5 sm:mt-8 sm:flex sm:justify-center lg:justify-start">
            <div class="rounded-md shadow">
                <a href="#"
                    class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-white bg-gray-800 hover:bg-gray-600 md:py-4 md:text-lg md:px-10">
                    Get started
                </a>
            </div>
            <div class="mt-3 sm:mt-0 sm:ml-3">
                <a href="#"
                    class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-gray-800 bg-indigo-100 hover:bg-indigo-200 md:py-4 md:text-lg md:px-10">
                    Live demo
                </a>
            </div>
        </div>
        <!-- End of Button Section -->
    </div>

    <!--   Image Section     -->
    <div class="lg:inset-y-0 lg:right-0 lg:w-1/2 my-4">
        <img class="h-56 w-full object-cover sm:h-72 md:h-96 lg:w-full lg:h-full" src="https://images.unsplash.com/photo-1551434678-e076c223a692?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2850&q=80" alt="">
    </div>
    <!--   End of Image Section     -->


    
</div>

</section>
<div class="bg-blue-400 border-2 border-white shadow-lg rounded-xl p-6 text-center text-white max-w-md mx-auto">
    <div class="text-2xl font-bold text-black"> h2 Template </div>
</div>

<!-- music--> 
    <div>
    <div class="flex space-x-1 items-center">
      <p>Music:</p>
      <label class="swap">
        <!-- this hidden checkbox controls the state -->
        <input type="checkbox" @click="playMusic" v-model="onMusic" />

        <!-- volume on icon -->
        <svg
          class="swap-on fill-current"
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
        >
          <path
            d="M14,3.23V5.29C16.89,6.15 19,8.83 19,12C19,15.17 16.89,17.84 14,18.7V20.77C18,19.86 21,16.28 21,12C21,7.72 18,4.14 14,3.23M16.5,12C16.5,10.23 15.5,8.71 14,7.97V16C15.5,15.29 16.5,13.76 16.5,12M3,9V15H7L12,20V4L7,9H3Z"
          />
        </svg>

        <!-- volume off icon -->
        <svg
          class="swap-off fill-current"
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
        >
          <path
            d="M3,9H7L12,4V20L7,15H3V9M16.59,12L14,9.41L15.41,8L18,10.59L20.59,8L22,9.41L19.41,12L22,14.59L20.59,16L18,13.41L15.41,16L14,14.59L16.59,12Z"
          />
        </svg>
      </label>
      <audio controls class="hidden" ref="musicPlayer">
        <source src="./assets/sample.mp3" type="audio/mp3" />
        <p>
          Your browser doesn't support this audio file. Here is a
          <a href="sample.mp3">link to the audio</a> instead.
        </p>
      </audio>
    </div>
  </div>


       
<div>
  <!-- <div class="">
    Attach File : <input type="file" accept=".pdf , .doc"@change="chooseBinaryFile"> 
    <a href="urlDocFile" target="_blank" class="bg-red-400" >{{docName}} </a>
  </div> -->
  <div class="p-4">
    <div>
      <h2 class="red"> Picture : <input type="file" @change="chooseBinaryFile" accept="image/*" class="mb-4 " /> </h2>
    </div>
   
    <div v-if="showPicture" class="thumbnail-container">
      <p>🖼 รูปภาพที่เลือก:</p>
      <img :src="showPicture" target="_blank" class="bg-red-500" />
    </div>
  </div>


</div>





</template>

<style scoped></style>