<script>
// @ts-nocheck
import '../app.css'
import Cookies from 'js-cookie'
  import { onMount } from 'svelte';
  import Users from '../../components/Users.svelte';
let role = ''


onMount(async () =>{
    role = Cookies.get('role')
} )
</script>

{#if role=='user'}
<div class="container">
    Permission denied
</div>
    
{:else}
<div class="container">
    <Users></Users>
</div>
{/if}
<style>

.container{
    max-width: 1080px;
    margin: 0px auto;
    height: 100%;
    display: flex;
    flex-direction: column;
    background-color: #eee;
}

</style>