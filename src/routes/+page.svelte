<script>
    // @ts-nocheck
      import Cookies from 'js-cookie'
      import Button from "../components/Button.svelte";
    
        let login = '';
        let password = '';
        let confirmPassword = '';
        let error = '';
        let success = false;
        let role = '';
      
        const handleSubmit = async (event) => {
          event.preventDefault();
    

          try {
            const response = await fetch('http://147.45.110.199/Login', {
              method: 'POST',
              mode: 'cors',
              headers: { 'Content-Type': 'application/json' },
              body: JSON.stringify({ login, password })
            }).then((value) => {
              role = value
              console.log(role)
            });


      
            if (response.ok) {
              // Cookies.set(`role=${role}`)
              success = true;
              error = '';
              login = '';
              password = '';
              confirmPassword = '';
              // window.location.href = '/dashboard';
            } else {
              const data = await response.json();
              error = data.message || 'Произошла ошибка при авторизации';
            }
          } catch (err) {
            error = err;
          }
        };
      </script>
    
      <div class="container">
        <h1 style="text-align: center; margin-bottom: 30px">Авторизация</h1>
        <form on:submit|preventDefault={handleSubmit}>
          <div>
            <label for="login">Имя пользователя:</label>
            <input id="login" type="text" bind:value={login} required />
          </div>
          
          <div>
            <label for="password">Пароль:</label>
            <input id="password" type="password" bind:value={password} required />
          </div>
          
          
          <Button title='Войти'></Button>
          {#if error}
          <p class="error">{error}</p>
          {/if}
        </form>
        </div>
      
      
      <style>
        .container{
          max-width: 1080px;
          margin: 0px auto;
          transform: translateY(60%);
        }
        form {
          display: flex;
          flex-direction: column;
          align-items: center;
          max-width: 400px;
          margin: 0px auto;
          text-align: left;
        }
        div {
          display: flex;
          flex-direction: column;
          margin-bottom: 10px;
        }
        .error {
          color: red;
        }
        label{
          font-size: 16px;
          color: #163309;
        }
        input{
          border: 0px;
          padding: 10px;
          background-color: white;
          -webkit-box-shadow: 0px 1px 10px 2px rgba(34, 60, 80, 0.2);
          -moz-box-shadow: 0px 1px 10px 2px rgba(34, 60, 80, 0.2);
          box-shadow: 0px 1px 10px 2px rgba(34, 60, 80, 0.2);
          border-radius: 5px;
    }
    </style>