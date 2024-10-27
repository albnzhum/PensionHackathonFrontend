<script>
// @ts-nocheck

    import '../app.css'
    import Cookies from 'js-cookie'
    import { onMount } from 'svelte';
    let {children} = $props()
    let role = null
    onMount(async () =>{
        role = Cookies.get('role')
        if (role==null)
            window.location.replace('/')
    } )
    </script>
    
    
    {@render children()}
    
    <style>
    
    </style>