<template>
  <div id="nav" class="nav">
    <div class="container">
      <h1>This is Encoder and Decoder Page</h1>
      <textarea
        name="input"
        id="input"
        cols="100"
        rows="10"
        placeholder="Text here..."
        spellcheck="false"
        v-model="charset.text"
      ></textarea>
      <br>
      <select name="charset" id="option_text_charset" v-model="charset.charsetType">
        <option value="IBM00858">IBM00858</option>
        <option value="IBM437">IBM437</option>
        <option value="IBM775">IBM775</option>
        <option value="IBM850">IBM850</option>
        <option value="IBM852">IBM852</option>
        <option value="IBM855">IBM855</option>
        <option value="IBM857">IBM857</option>
        <option value="IBM862">IBM862</option>
        <option value="IBM866">IBM866</option>
        <option value="ISO-8859-1">ISO-8859-1</option>
        <option value="ISO-8859-2">ISO-8859-2</option>
        <option value="ISO-8859-4">ISO-8859-4</option>
        <option value="ISO-8859-5">ISO-8859-5</option>
        <option value="ISO-8859-7">ISO-8859-7</option>
        <option value="ISO-8859-9">ISO-8859-9</option>
        <option value="ISO-8859-13">ISO-8859-13</option>
        <option value="ISO-8859-15">ISO-8859-15</option>
        <option value="CESU-8">CESU-8</option>
        <option value="KOI8-R">KOI8-R</option>
        <option value="KOI8-U">KOI8-U</option>
        <option value="US-ASCII">US-ASCII</option>
        <option value="UTF-8">UTF-8</option>
        <option value="UTF-16">UTF-16</option>
        <option value="UTF-16BE">UTF-16BE</option>
        <option value="UTF-16LE">UTF-16LE</option>
        <option value="UTF-32">UTF-32</option>
        <option value="UTF-32BE">UTF-32BE</option>
        <option value="UTF-32LE">UTF-32LE</option>
        <option value="x-UTF-32BE-BOM">x-UTF-32BE-BOM</option>
        <option value="x-UTF-32LE-BOM">x-UTF-32LE-BOM</option>
        <option value="Windows-1251">Windows-1251</option>
        <option value="Windows-1252">Windows-1252</option>
        <option value="Windows-1253">Windows-1253</option>
        <option value="Windows-1254">Windows-1254</option>
        <option value="Windows-1257">Windows-1257</option>
        <option value="x-IBM737">x-IBM737</option>
        <option value="x-IBM874">x-IBM874</option>
        <option value="x-UTF-16LE-BOM">x-UTF-16LE-BOM</option>
      </select>
      <select name="code" id="option_text_charset" v-model="code">
        <option value="encode" selected>Encode</option>
        <option value="decode">Decode</option>
      </select>
      <button class="convert" v-on:click="convert">Convert</button>
      <br>
      <textarea
        name="output"
        id="output"
        cols="100"
        rows="10"
        placeholder="Result..."
        v-model="inf.yourCode"
      ><h1>nima</h1></textarea>
    </div>
  </div>

  <!-- code: {{code}}
<br>
  request: {{ charset }}
  <br>
  response:{{ inf }} -->
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import axios from 'axios'

export default {
  name: "App",
  components: {
    HelloWorld,
  },
  data() {
    return {
      code: "encode",
      inf: {
        yourCode: null
      },
      charset: {
        text: null,
        charsetType: "UTF-8"
      }
    }
  },
  methods: {
    convert() {
      console.log(this.inf);
      axios
        .post("http://localhost:8082/api/"+this.code,this.charset)
        .then(res => (this.inf = res.data))
    }
  }
};
</script>

<style scoped>
#nav {
  width: 100%;
}
.nav .container {
  max-width: 90%;
  padding: 20px;
  margin: auto;
}

.router {
  text-decoration: none;
  margin: 5px;
  padding: 5px;
  border-radius: 5px;
  background-color: white;
  color: #000;
  font-size: 14px;
  font-weight: 400;
  transition: all 0.4s;
}
textarea {
  margin-bottom: 20px;
  margin-top: 10px;
}
</style>
