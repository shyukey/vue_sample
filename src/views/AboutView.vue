<template>
  <div class="about">
    <h1>ZipLib検証</h1>
    <input
      style="display: none"
      ref="input"
      type="file"
      accept="application/zip"
      @change="selectedFile()"
    />
    <!-- ファイルの選択 -->
    <v-btn color="btn-primary" @click="btnclick">select image</v-btn>
    <div v-if="imageData.length">
      <div class="row">
        <v-btn color="btn-primary" @click="onlyQ">Qだけ表示</v-btn>
        <v-btn color="btn-primary" @click="onlyA">Aだけ表示</v-btn>
      </div>
      <div v-for="image in resultData" :key="image.url">
        <img v-bind:src="image.url" v-bind:alt="image.name" />
      </div>
    </div>
  </div>
</template>
<script>
import JSZip from "jszip";
export default {
  props: {},
  data() {
    return {
      imageData: [],
      resultData: [],
    };
  },
  methods: {
    // selectfileボタン押下時
    btnclick() {
      this.$refs.input.click();
    },
    onlyQ() {
      this.resultData = this.imageData.filter(function(image) {
        return image.key == 'Question';
      });
    },
    onlyA() {
      this.resultData = this.imageData.filter(function(image) {
        return image.key == 'Answer';
      });
    },
    async selectedFile() {
      // ファイル読み込み後
      const regexpTxtFile = /\.(txt)/;
      const regexpImgFile = /\.(png)/;
      // this.$refs.input.files[0];がzip
      const files = this.$refs.input.files[0];
      // Zipファイル読み込み
      JSZip.loadAsync(files).then((result) => {
        console.log("sync1");
        let promises = [];
        let promises2 = [];
        // テキストファイルのみを抽出
        result.file(regexpTxtFile).forEach((file_list_txt) => {
          // テキストファイルを読み込む
          let filename = file_list_txt.name.match(/([^/]*)\./)[1];
          promises.push(
            file_list_txt.async("string").then((result) => {
              return { key: filename, list: result };
            })
          );
        });
        Promise.all(promises).then((txt_promise_result) => {
          txt_promise_result.forEach((data) => {
            data.list.split("\r\n").forEach((file) => {
              // 画像パスを読み込む
              result.file(regexpImgFile).forEach((image_data) => {
                if (image_data.name.indexOf(file) != -1) {
                  promises2.push(
                    image_data.async("blob").then((image_blob) => {
                      const imgUrl = URL.createObjectURL(image_blob);
                      return { key: data.key, name: file, url: imgUrl };
                    })
                  );
                }
              });
            });
          });
          Promise.all(promises2).then((result) => {
            console.log("全て終了");
            console.log(result);
            this.imageData = result;
          });
        });
      });
    },
  },
};
</script>
