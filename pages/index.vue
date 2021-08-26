<template>
  <div>
    <button @click="print">print</button>
    <div id="htmlcode"><HtmlCode /></div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {}
  },
  methods: {
    print() {
      var html = document.getElementById('htmlcode').innerHTML
      var htmlPage = `<!DOCTYPE html>
          <html lang="en">
            <head>
              <meta charset="UTF-8">
              <meta name="description" content="">
              <meta name="keywords" content="">
              <meta name="viewport" content="width=device-width, initial-scale=1.0, shrink-to-fit=no">
              <title>Hala</title>
              <link rel="stylesheet" href="https://halaaa.netlify.app/css/style.css">
              <link rel="preconnect" href="https://fonts.googleapis.com">
              <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
              <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700;900&display=swap" rel="stylesheet">
            </head>
            <body>
              ${html}
            </body>
          </html>`

      axios
        .post('https://api.html2pdf.app/v1/generate', {
          html: htmlPage,
          apiKey:
            'CdJHZtimxELFk1aWLBNvfbAa0LOE3seORPoqbwo4pGb7BO18B3uhWhd9jjuPsEGn',
        })
        .then((response) => {
          console.log(response.config)
          const fileURL = window.URL.createObjectURL(new Blob([response.data]))
          const fileLink = document.createElement('a')
          fileLink.href = fileURL
          fileLink.setAttribute('download', `fatoom.pdf`)
          document.body.appendChild(fileLink)
          fileLink.click()
        })
        .catch((err) => {
          console.log(err.message)
        })

      /*var element = document.getElementById('htmlcode')
      var opt = {
        margin: 1,
        filename: 'myfile.pdf',
        image: { type: 'jpeg', quality: 0.98 },
        html2canvas: {},
        jsPDF: { format: 'A4' },
      }
      html2pdf().set(opt).from(htmlPage).save()*/
    },
  },
}
</script>
<style scoped lang="scss"></style>
