<template>
  <div class="container">
    <div>
      <img id="content_image" v-if="image_src" :src="image_src" class="content_image"/>
    </div>
    <div>
      <input type="file" @change="onFileChange" class="input_button"/>
    </div>
    <div>
      <el-input placeholder="Please input style" v-model="text" style="width: 20vw; margin-top: 3vh;"></el-input>
    </div>
    <div>
      <el-button type="primary" @click="onSubmit" style="margin-top: 3vh;">Submit</el-button>
    </div>
    <div>
      <img id="style_transfer_image" v-if="style_transfer_image" :src="style_transfer_image" class="style_transfer_image"/>
    </div>
  </div>
</template>

<script>
export default {
  name: "UploadImageContainer",
  data() {
    return {
      contentImageWidth: 0,
      contentImageHeight: 0,
      image_src: null,
      image_file: null,
      text: '',
      style_transfer_image: null,
    };
  },
  methods: {
    onFileChange(e) {
      const file = e.target.files[0];
      let image = new Image();
      image.onload = () => {
        this.contentImageWidth = image.width;
        this.contentImageHeight = image.height;
        console.log(this.contentImageWidth, this.contentImageHeight);
        this.image_src = image.src;
        this.image_file = file;
      };
      image.src = URL.createObjectURL(file);
    },
    packData() {
      let formData = new FormData();
      formData.append('content_image', this.image_file);
      formData.append('style_text', this.text);
      return formData;
    },
    onSubmit() {
      let formData = this.packData();
      let _this = this;
     fetch('http://localhost:5001/api/transfer', {
        method: 'POST',
        body: formData,
      }).then(response => {
        response.json().then(data => {
          _this.style_transfer_image = 'data:image/jpeg;base64,' + data['images'];
        });
      });
    }
  }
}
</script>

<style scoped>
.container {
  align-content: center;
}

.content_image {
  width: 30%;
  height: 30%;
}

.style_transfer_image {
  width: 30%;
  height: 30%;
  margin-top: 3vh;
}

.input_button {
}
</style>