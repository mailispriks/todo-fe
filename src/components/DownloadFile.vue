<template>
  <div>
   <!-- TODO: Create visual logic for downloading file -->
  </div>
</template>
<script>
import axios from 'axios';

export default {
  data () {
    return {
      form: {
        fileType: 'PDF',
        todo: false,
        done: false
      }
    }
  },
  methods: {
    async getFile () {
      await axios({
        url: 'api/downloadFile',
        method: 'POST',
        data: this.form,
        responseType: 'arraybuffer'
      }).then(rs => {
        this.downloadBinaryFile(rs.data, rs.headers, 'Todo')
      })
    },
    downloadFile (content, headers, name) {
      const blob = new Blob([
        content
      ], { type: headers['content-type'] })
      const link = document.createElement('a')
      link.href = window.URL.createObjectURL(blob)
      link.download = !name ? headers['content-disposition'].split('filename=')[1].replace(/(^")|("$)/g, '') : name + (blob.type === 'application/pdf' ? '.pdf' : '')
      document.body.appendChild(link)
      link.click()
      document.body.removeChild(link)
    },
    downloadBinaryFile (binaryContent, headers, name) {
      this.downloadFile(new Uint8Array(binaryContent), headers, name)
    }
  }
};
</script>
<style scoped>
  .border-gray {
    border-bottom: 1px solid rgba(55, 65, 81, 0.3);
    border-radius: 0;
  }
</style>
