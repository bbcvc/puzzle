<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue';
import html2canvas from 'html2canvas';

/** html转base64 */
const savePoster = () => {
  html2canvas(document.querySelector('#downPoster'), {
    useCORS: true,
    scale: 2,
  }).then((canvas: any) => {
    downloadBase64(canvas.toDataURL(), '下载图片名');
  });
};
/** 下载图片 */
const downloadBase64 = (
  dataUrl: string,
  fileName: string = 'download',
  fileExtension: string = 'png',
) => {
  // 将 base64 字符串转换为 Blob 对象
  const byteCharacters = atob(dataUrl.split(',')[1]);
  const byteArrays = [];
  for (let offset = 0; offset < byteCharacters.length; offset += 10240) {
    const slice = byteCharacters.slice(offset, offset + 10240);
    const byteNumbers = new Array(slice.length);
    for (let i = 0; i < slice.length; i++) {
      byteNumbers[i] = slice.charCodeAt(i);
    }
    const byteArray = new Uint8Array(byteNumbers);
    byteArrays.push(byteArray);
  }
  const blob = new Blob(byteArrays, { type: 'application/octet-stream' });
  const blobUrl = URL.createObjectURL(blob);
  const creatDom = document.createElement('a');
  document.body.appendChild(creatDom);
  creatDom.href = blobUrl;
  creatDom.download = `${fileName}.${fileExtension}`;
  creatDom.click();
  document.body.removeChild(creatDom);
  URL.revokeObjectURL(blobUrl);
};
</script>

<template>
  <div class="preview-img">
    <HelloWorld />
  </div>
  <div class="control">
    <button :onclick="savePoster">生成图片</button>
  </div>
</template>

<style scoped>
.preview-img {
  width: 5760px;
  margin: auto;
}
.control {
  width: 450px;
  background-color: rgba(0, 250, 250, 0.8);
  height: 60px;
  margin: auto;
  margin-top: 24px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
