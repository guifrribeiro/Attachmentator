<template>
  <q-page class="flex flex-center">
    <div ref="content">
      <img alt="Quasar logo" src="~assets/quasar-logo-full.svg">

      <q-btn @click="downloadWithCSS">Download PDF</q-btn>
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
      const contentHtml = this.$refs.content.innerHTML;
      doc.fromHTML(contentHtml, 15, 15, {
        width: 170
      });
      doc.save("sample.pdf");
    },
    downloadWithCSS() {
      const doc = new jsPDF();

      var canvasElement = document.createElement('canvas');
      html2canvas(this.$refs.content, { canvas: canvasElement
        }).then(function (canvas) {
          const img = canvas.toDataURL("image/jpeg", 0.8);
          doc.addImage(img, 'JPEG', 20, 20);
          doc.save("sample.pdf");
        });
    }
  }
}
</script>
