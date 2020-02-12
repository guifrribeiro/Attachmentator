<template>
  <q-page class="flex flex-center">
    <div ref="content">
      <img alt="Quasar logo" src="~assets/quasar-logo-full.svg">
      <h1>Teste de impressão com um arquivo pdf.</h1>
    

      <q-btn @click="createPDF">Create PDF</q-btn>
      <q-btn @click="download">Download PDF without CSS</q-btn>
      <q-btn @click="downloadWithCSS">Download PDF with CSS</q-btn>
    </div>
  </q-page>
</template>

<script>
import jsPDF from 'jspdf';
import html2canvas from 'html2canvas';

export default {
  name: 'PageIndex',
  methods: {
    createPDF() {
      let pdfName = 'test';
      var doc = new jsPDF();
      doc.text("Hello world", 10, 10);
      doc.save(pdfName + '.pdf');
    },
    download() {
      const doc = new jsPDF();
      console.log(this.$refs)
      const contentHtml = this.$refs.content.innerHTML;
      doc.fromHTML(contentHtml, 15, 15, {
        width: 170
      });
      doc.save("sample.pdf");
    },
    downloadWithCSS() {
      const doc = new jsPDF({
        orientation: 'l',
        format: 'a4',
        unit: 'mm'
      });

      var canvasElement = document.createElement('canvas');
      console.log(this.$refs.content);
      html2canvas(this.$refs.content, { canvas: canvasElement
        }).then(function (canvas) {
          const img = canvas.toDataURL("image/jpeg");
          doc.addImage(img, 'JPEG', 360, 360);
          doc.save("sample.pdf");
        });
    },
  }
}
</script>
