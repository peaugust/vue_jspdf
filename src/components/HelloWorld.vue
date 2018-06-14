<template>
  <div>
    <input type="text" v-model="text">
    <button @click="createPDF()">TESTE</button>
    <pre>{{text}}</pre>
    <div id="test"></div>
  </div>
</template>

<script>
  import pdfobject from  'pdfobject'
import jsPDF from 'jspdf'
export default {
  name: 'HelloWorld',
  data: function () {
    return {
      text: ''
    }
  },
  methods: {
    createPDF () {
      var vm = this;
      console.log(vm.text);
      var doc = new jsPDF();
      doc.text(vm.text, 10, 10);
      doc.addFont("Arial", "Arial", "normal");
      doc.setFont("Arial");
      pdfobject.embed( doc.output('datauristring'), "#test");

    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .pdfobject-container { height: 500px;}
  .pdfobject { border: 1px solid #666; }
</style>
