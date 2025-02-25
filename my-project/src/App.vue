<script setup>
import { onMounted, ref } from 'vue'
import { previewBinaryFile } from './assets/utilities'

const musicPlayer = ref(null) // Initialize to null
const onMusic = ref(false)
const volume = ref(0.5)

const playMusic = () => {
  onMusic.value = !onMusic.value
  if (onMusic.value) {
    musicPlayer.value.play().catch(error => {
      console.error('Error playing music:', error)
    })
  } else {
    musicPlayer.value.pause()
  }
}
const loopMusic = () => {
  if (musicPlayer.value) {
    musicPlayer.value.loop = true;
  }
};

onMounted(() => {
  if (musicPlayer.value) {
    musicPlayer.value.load();
    musicPlayer.value.play().catch(error => {
      console.error("Error playing music:", error);
    });

    loopMusic();
  } else {
    console.error("musicPlayer");
  }
});
const changeVolume = () => {
  musicPlayer.value.volume = volume.value
}

onMounted(() => {
  // Check if musicPlayer.value is defined before accessing it
  if (musicPlayer.value) {
    musicPlayer.value.load();
    // Autoplay, handle potential errors
    musicPlayer.value.play().catch(error => {
      console.error("Error playing music:", error);
      // You might want to handle this error gracefully, e.g., display a message to the user
    });
  } else {
    console.error("musicPlayer ref is not yet available in onMounted");
  }
});


const urlDocFile = ref('')
const showPicture = ref('')
const docName = ref('')

const chooseBinaryFile = (event) => {
  docName.value = event.target.files[0].name
  if (docName.value.endsWith('.pdf') || docName.value.endsWith('.doc')) {
    urlDocFile.value = previewBinaryFile(event.target.files[0])
  } else if (docName.value.endsWith('.jpg') || docName.value.endsWith('.png') || docName.value.endsWith('.jpeg')) {
    showPicture.value = URL.createObjectURL(event.target.files[0]);
  }
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
        <p class="mt-3 text-base text-gray-500 sm:mt-5 sm:text-lg sm:max-w-xl sm:mx-auto md:mt-5 md:text-xl lg:mx-0">
          Anim aute id magna aliqua ad ad non deserunt sunt. Qui irure qui lorem cupidatat commodo. Elit sunt amet
          fugiat veniam occaecat fugiat aliqua.
        </p>
      </div>
    </div>
  </section>

  <div class="flex">
  <div class="flex rounded-t-lg  rounded-b-lg flex-col grid-col-3  items-center bg-red-100 p-1.5 ml-330">
    <p>Music:</p>
    <input type="range" min="0" max="1" step="0.01" v-model="volume" @input="changeVolume"
      class="w-28 h-28 rotate-270" />

    <div class="flex bg-blue-200 p-3">
      <label class="swap">
        <input type="checkbox" @click="playMusic" v-model="onMusic" />
        <svg class="swap-off fill-current" xmlns="http://www.w3.org/2000/svg" width="24" height="24"
          viewBox="0 0 24 24">
          <path
            d="M3,9H7L12,4V20L7,15H3V9M16.59,12L14,9.41L15.41,8L18,10.59L20.59,8L22,9.41L19.41,12L22,14.59L20.59,16L18,13.41L15.41,16L14,14.59L16.59,12Z" />
        </svg>
        <svg class="swap-on fill-current" xmlns="http://www.w3.org/2000/svg" width="24" height="24"
          viewBox="0 0 24 24">
          <path
            d="M14,3.23V5.29C16.89,6.15 19,8.83 19,12C19,15.17 16.89,17.84 14,18.7V20.77C18,19.86 21,16.28 21,12C21,7.72 18,4.14 14,3.23M16.5,12C16.5,10.23 15.5,8.71 14,7.97V16C15.5,15.29 16.5,13.76 16.5,12M3,9V15H7L12,20V4L7,9H3Z" />
        </svg>
      </label>

      <audio controls class="hidden" ref="musicPlayer">
        <source src="./assets/sample.mp3" type="audio/mp3" />
        <p>Your browser doesn't support this audio file. Here is a <a href="sample.mp3">link to the audio</a> instead.
        </p>
      </audio>
    </div>
  </div>
</div>





  <!-- Ui 
  <div class="flex space-x-2 items-center">
  <p>Music:</p>
  <label class="swap">
    <input type="checkbox" @click="playMusic" v-model="onMusic" />
    <svg class="swap-off fill-current" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
      <path d="M3,9H7L12,4V20L7,15H3V9M16.59,12L14,9.41L15.41,8L18,10.59L20.59,8L22,9.41L19.41,12L22,14.59L20.59,16L18,13.41L15.41,16L14,14.59L16.59,12Z"/>
    </svg>
    <svg class="swap-on fill-current" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
      <path d="M14,3.23V5.29C16.89,6.15 19,8.83 19,12C19,15.17 16.89,17.84 14,18.7V20.77C18,19.86 21,16.28 21,12C21,7.72 18,4.14 14,3.23M16.5,12C16.5,10.23 15.5,8.71 14,7.97V16C15.5,15.29 16.5,13.76 16.5,12M3,9V15H7L12,20V4L7,9H3Z"/>
    </svg>
  </label>

  Vertical Slider -->
  <!-- <input type="range" min="0" max="1" step="0.01" v-model="volume" @input="changeVolume" class="w-24 h-48 rotate-270" />

  <audio controls class="hidden" ref="musicPlayer">
    <source src="./assets/sample.mp3" type="audio/mp3" />
    <p>Your browser doesn't support this audio file. Here is a <a href="sample.mp3">link to the audio</a> instead.</p>
  </audio> -->
  <!-- </div> -->




  <div class="p-4">
    <div>
      <h2 class="red">Picture : <input type="file" @change="chooseBinaryFile" accept="image/*" class="mb-4 " /></h2>
    </div>
    <div v-if="showPicture" class="thumbnail-container">
      <p>🖼 รูปภาพที่เลือก:</p>
      <img :src="showPicture" target="_blank" class="bg-red-500" />
    </div>
  </div>
</template>

<style scoped></style>