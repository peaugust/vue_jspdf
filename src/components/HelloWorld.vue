<template>
  <div>
    <h1>Insira os dados para criar um novo documento</h1>
    <button @click="newSection()">ADD</button>
    <div v-for="(section, index) in sections">
      <p>Seção {{index}} </p>
      <textarea type="text" v-model="section.text"></textarea>
    </div>
    <button @click="createPDF()">Send</button>
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
      sections: [{text:''}]
    }
  },
  methods: {
    newSection(){
      this.sections.push({text: ''});
    },
    createPDF () {
      var vm = this;
      var doc = new jsPDF();
      for(let i = 0; i < vm.sections.length; i++){
        console.log(vm.sections[i].text);
        doc.text(vm.sections[i].text, ((i+1)*10), ((i+1)*10));
      }


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
