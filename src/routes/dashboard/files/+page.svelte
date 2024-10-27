
<script>
// @ts-nocheck

  import Files from "../../../components/Files.svelte";

 
let dict = {}
dict['key'] = 0
dict['value'] = "string"
let key = 0
let value = "string"
// @ts-ignore
let file = null;
async function Generate(){
  const response = await fetch('http://147.45.110.199/GeneratePdf', {
        method: 'POST',
        mode: 'cors',
        headers: {'Content-Type': 'application/json'},
        body: [{key: 0, value: "string"}]
      });
}

// @ts-ignore

</script>
<button onclick={Generate}>загрузить</button>
<div class="container">

    <Files></Files>

</div>

<style>
.container{
    max-width: 1080px;
    margin: 0px auto;
    display: flex;
    flex-direction: column;
    background-color: #fff;
}

</style>