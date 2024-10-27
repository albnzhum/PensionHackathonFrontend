<script>
// @ts-nocheck

import { onMount } from 'svelte';
import LoadingPopup from './LoadingPopup.svelte';
import { fade } from 'svelte/transition';
  import Load from './Load.svelte';

let data = null;
let file = null;
let isLoading = true;
let isDeleting = false;

onMount(async function mountData(){
    isLoading = true
    try{
      console.log('onmount')
        const response = await fetch('http://147.45.110.199/GetAllFiles', {
          method: 'GET',
          mode: 'cors',
          headers: {'Content-Type': 'application/file'},
        });
        data = await response.json();
    }catch(error){
        console.log('err getAllFiles ' + error)
    }finally{
        isLoading = false
        console.log(data)
    }

  });

// @ts-ignore
function handleFileChange(event) {
    event.preventDefault();
  file = event.target.files[0];
}
async function getData(){
    console.log('getData')
}
async function deleteData(id){
  isDeleting = true
    try {
        console.log('delete')
      const response = await fetch(`http://147.45.110.199/DeleteFile/${id}`, {
        method: 'DELETE'
      });

      if (!response.ok) {
        alert("Ошибка загрузки файла");
      }
      else{
        console.log('ok')
      }
      
      data = data.filter(item => item.id !== id);
    } catch (error) {
      console.error("Произошла ошибка:", error);
    }finally{
      isDeleting=false
    }
}
async function uploadData(){
  handleFileChange()
    const formData = new FormData();
    formData.append("file", file);

    try {
        console.log('start upload file')
      const response = await fetch('http://147.45.110.199/UploadFile', {
        method: 'POST',
        mode: 'cors',
        body: formData
      });
      if (response.ok) {
        alert("Файл успешно загружен!");
      } else {

        alert("Ошибка загрузки файла");
      }
    } catch (error) {
            console.log(error)
      console.error("Ошибка:", error);
      alert("Ошибка при отправке файла");
    }
  }
</script>
{#if isLoading}
    <Load isOpen={isLoading}></Load>
{:else}
<div class="_container">
    <div transition:fade={{ duration: 500 }} class="title">
      <h1 class="title_text">Все загруженные файлы</h1>
      <form method="post" enctype="multipart/form-data" >
        <label class="title_btn">
            <input onchange={(event) => uploadData(event)} type="file" name="file" accept=".csv">		
            <span>Загрузить файл</span>
        </label>
      </form>
  </div>

  {#each data as file}
  <div class="row">
      <div id='{file.id}'>
          <p class="row__title">{file.fileName}</p>
      </div>
      <div>
          <button onclick={getData} class="row__icons-go">Загрузить</button>
          <button onclick={() => deleteData(file.id)} class="row__icons-del">Удалить</button>
      </div>
  </div> 
  {/each}
</div>

{/if}


<style>
._container{
  background-color: #fff;
  border-radius: 15px;
  width: 100%;
  min-height: 100%;
}
.title{
    display: flex;
    align-content: center;
    justify-content: space-between;
    margin: 0;
    border-bottom: 3px solid #f5f5f5;
    padding: 15px 30px;
    align-items: center;
}
.title_text{
  font-size: 28px;

  font-weight: 600;
}
.title_btn{
    font-size: 16px;
    outline: none;
    text-decoration: none;
    cursor: pointer;
    color: #fff;
    border: 3px solid #0d2005;
    border-radius: 10px;
    padding: 10px;
    background-color: #163309;
    transition: 0.3s ease all;
    margin-right: 20px;
}
.title_btn input[type=file] {
    position: absolute;
    z-index: -1;
    opacity: 0;
    display: block;
    width: 0;
    height: 0;
}
.title_btn:hover{
    transition: 0.3s ease all;
    opacity: 0.7;
}
.row{
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 10px;
  padding: 5px 30px;
  border-bottom: 1px solid #f5f5f5;
}
.row__title{
    font-size: 15px;
}
.row__icons-go{
    cursor: pointer;
    color: #fff;
    border: 3px solid #628042;
    border-radius: 10px;
    padding: 10px;
    background-color: #8DA870;
    transition: 0.3s ease all;
    margin-right: 20px;
}
.row__icons-go:hover{
    transition: 0.3s ease all;
    opacity: 0.7;
}
.row__icons-del{
    cursor: pointer;
    color: #fff;
    border: 3px solid #610f21;
    border-radius: 10px;
    padding: 10px;
    background-color: #6b1a2b;
    transition: 0.3s ease all;
}
.row__icons-del:hover{
    transition: 0.3s ease all;
    opacity: 0.7;
}
</style>