<script>
// @ts-nocheck

import { onMount } from 'svelte';
import LoadingPopup from './LoadingPopup.svelte';
import { fade } from 'svelte/transition';
import RegistrationPopup from './RegistrationPopup.svelte';

let isLoading = true
let isDeleting = false
let isRegistration = false
let data=null

onMount(async function mountData(){
    isLoading = true
    try{
        const response = await fetch('http://147.45.110.199/GetUsers', {
          method: 'GET',
          mode: 'cors',
          headers: {'Content-Type': 'application/json'},
        });
        data = await response.json();
    }catch(error){
        console.log('err GetUsers ' + error)
        await setTimeout(mountData, 3000)
    }finally{
        isLoading = false
        console.log(data)
    }

  });

async function addUser(){
    isRegistration = !isRegistration
}
async function updateUser(id){

}
async function delUser(id){

    try {
        console.log('delete' + id)
      const response = await fetch(`http://147.45.110.199/DeleteUser/${id}`, {
        method: 'DELETE'
      });

      if (!response.ok) {
        alert("Ошибка загрузки файла");
      }
      else{
        console.log(response.json())
      }
      
      data = data.filter(item => item.id !== id);
    } catch (error) {
      console.error("Произошла ошибка:", error);
}}
</script>

{#if isLoading}
    <LoadingPopup isOpen={isLoading}></LoadingPopup>
{:else if isDeleting}
    <LoadingPopup isOpen={isDeleting}></LoadingPopup>
{:else if isRegistration}
    <RegistrationPopup isOpen={isRegistration}></RegistrationPopup>
{:else}
<div class="_container">
    <div transition:fade={{ duration: 500 }} class="title">
        <h1 class="title-text">Все сотрудники</h1>

        <button onclick={addUser} class="title_btn">Добавить сотрудника</button>
    </div>

    {#each data as user}
    <div class="row">
        <div id='{user.id}'>
            <p class="row__title">{user.login}</p>
        </div>
        <div>
            <button onclick={() => updateUser(user.id)} class="row__icons-go">Редактировать</button>
            <button onclick={() => delUser(user.id)} class="row__icons-del">Удалить</button>
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