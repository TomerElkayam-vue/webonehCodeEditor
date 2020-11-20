<template >
  <v-container id="codeApp" >
    <v-row justify="center">
        <h1> Weboneh! </h1>
    </v-row>
    <v-row justify="center">
      <codemirror  ref="cmEditor" class="rounded-xl ma-4 elevation-15" id="codeEditor" v-model="code"  :options="cmOptions" />
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'

import { codemirror } from 'vue-codemirror'

// import base style
import 'codemirror/lib/codemirror.css'

// import more codemirror resource...
import 'codemirror/mode/javascript/javascript.js'

// import theme style
import 'codemirror/theme/ayu-mirage.css'

import 'codemirror/addon/selection/mark-selection';

@Component({
  components: {
    codemirror
  }
})
export default class codeEditor extends Vue {
  cmOptions:Any = {
        tabSize: 4,
        mode: 'text/javascript',
        theme: 'ayu-mirage',
        lineNumbers: true,
        line: true,
        readOnly: true,
        styleActiveLine: true,
        styleSelectedText: true,
        styleActiveSelected: true,
        scrollbarStyle: "null",
        lineWrapping: true
        // more CodeMirror options...
      }

  mounted() {
    this.resizeEditor();
    document.addEventListener('keyup', event => {
      if (event.code === 'Space') {
          this.higlightText();
      }
    })
  }

  resizeEditor() {
    this.$refs.cmEditor.cminstance.setSize( this.$refs.cmEditor.cminstance.defaultCharWidth() * 110)
  }

  higlightText() {
      this.$refs.cmEditor.cminstance.markText(this.$refs.cmEditor.cminstance.getCursor(true), this.$refs.cmEditor.cminstance.getCursor(false), {className: "styled-background"});  
      this.$refs.cmEditor.cminstance.setSelection(this.$refs.cmEditor.cminstance.getCursor(true), this.$refs.cmEditor.cminstance.getCursor(true))
  }

  multiply(firstNumber, secondNumber) {
    return firstNumber * secondNumber;
  }
 

  code: String = `const addItemToTheList = function addItemToTheList(data) {
  localStorage.setItem("applications", JSON.stringify(JSON.parse(localStorage.getItem("applications")).concat(data)));
};

const getNextId = function getNextId() {
  let id = localStorage.getItem("id") + 1;
  localStorage.setItem("id", id);
  return id;
};

document.addEventListener("DOMContentLoaded", () => {
  const pattern = /^[a-zA-Z0-9]{4,30}$/;
  document.getElementById("name").addEventListener("input", () => {
    if (!document.getElementById("name").value.match(pattern)) {
      document.getElementById("name").classList.remove("is-valid");
      document.getElementById("name").classList.add("is-invalid");
    } else {
      document.getElementById("name").classList.remove("is-invalid");
      document.getElementById("name").classList.add("is-valid");
    }
  });

  document.getElementById("price").addEventListener("input", function () {
    if (document.getElementById("price").value.length === 0) {
      document.getElementById("price").classList.remove("is-valid");
      document.getElementById("price").classList.add("is-invalid");
    } else if (isNaN(document.getElementById("price").value)) {
      document.getElementById("price").classList.remove("is-valid");
      document.getElementById("price").classList.add("is-invalid");
    } else {
      document.getElementById("price").classList.remove("is-invalid");
      document.getElementById("price").classList.add("is-valid");
    }
  });
});

const errorMessage = document.createTextNode("Oops, something went wrong!Check your fields again.");

const CheckAll = function CheckAll() {
  if (document.getElementById("price").classList.contains("is-valid") && document.getElementById("name").classList.contains("is-valid")) {
    return true;
  }

  document.getElementById("error").appendChild(errorMessage);
  return false;
};

const addApp = function addApp() {
  if (CheckAll()) {
    addItemToTheList({
      id: getNextId(),
      imageUrl: document.getElementById("ImageUrl").value,
      name: document.getElementById("name").value,
      price: document.getElementById("price").value,
      desc: document.getElementById("description").value ? document.getElementById("description").value : "this app does not have description",
      companyName: document.getElementById("companyName").value ? document.getElementById("companyName").value : "this app does not have a company",
    });

    window.location.href = "MainPage.html";
  }
};`;

}

  
</script>

<style >
.CodeMirror {
  height: auto;
  border-radius: 35px;
  padding: 25px;
}

.styled-background {
  background-color: rgba(244, 247, 118, 0.3)
}
</style>
