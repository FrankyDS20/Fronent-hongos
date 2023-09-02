<template>
    <q-page class="fullscreen-page" padding>
        <div>
            <h3 style="color: black; background-color: yellow;">
  BIENVENIDOS
</h3>
        </div>
      <div
        id="drop-area"
        @dragover.prevent="handleDragOver"
        @dragleave="handleDragLeave"
        @drop="handleDrop"
        class="drop-area"
      >
        <p class="centered-text">Arrastra una imagen aquí o haz clic para seleccionar una.</p>
        <input
          type="file"
          ref="fileInput"
          style="display: none"
          @change="handleFileChange"
        />
      </div>
      <div class="image-container" v-if="imagePreview">
        <img :src="imagePreview" alt="Preview" class="preview-image" />
        <div>
        <q-btn  @click="predict" label="predecir" color="primary" />
        <p v-if="predictionResult">Resultado de la predicción: {{ predictionResult }}</p>
      </div>
      
    </div>
    <q-btn @click="openFileInput" label="Subir Imagen" color="primary" class="upload-button" />
    </q-page>
  </template>
  
  <script>
  export default {
    data() {
      return {
        imagePreview: "",
        predictionResult: "",
      };
    },
    methods: {
      openFileInput() {
        this.$refs.fileInput.click();
      },
      handleFileChange(e) {
        const file = e.target.files[0];
        if (file) {
          this.loadImage(file);
        }
      },
      handleDragOver(e) {
        e.preventDefault();
        e.currentTarget.classList.add("active");
      },
      handleDragLeave(e) {
        e.currentTarget.classList.remove("active");
      },
      handleDrop(e) {
        e.preventDefault();
        e.currentTarget.classList.remove("active");
        const file = e.dataTransfer.files[0];
        if (file) {
          this.loadImage(file);
        }
      },
      loadImage(file) {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.imagePreview = e.target.result;
        };
        reader.readAsDataURL(file);
      },
      predict() {
        // Simulación de la lógica de predicción
        this.predictionResult = "Clase A"; // Reemplaza esto con tu lógica real
      },
    },
  };
  </script>
  
  <style scoped>
  .fullscreen-page {
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  
  .drop-area {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 70%; /* Adjust the height as needed */
    border: 2px dashed #ccc;
    cursor: pointer;
  }
  
  .drop-area.active {
    border-color: #007bff;
  }
  
  .centered-text {
    margin: 0;
  }
  
  .image-container {
    margin-top: 10px;
    text-align: center;
  }
  
  .preview-image {
  width: 400px; /* Set the desired width */
  height: 400px;
  max-height: 100%; /* Adjust the height as needed */
}
  .upload-button {
    margin-top: 10px;
  }
  </style>