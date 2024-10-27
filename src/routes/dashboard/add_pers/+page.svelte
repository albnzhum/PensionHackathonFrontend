<script>
    // @ts-nocheck
    
      import Button from "../../../components/Button.svelte";
    
        let fullName = '';
        let age = 0;
        let gender = '';
        let salary = 0
        let workExperience = ''
        let cityResidence = ''
        let error = '';
        let success = false;
      
        const handleSubmit = async (event) => {
          event.preventDefault();
      
          
          try {
            const response = await fetch('http://147.45.110.199/CreatePerson', {
              method: 'POST',
              mode: 'cors',
              headers: { 'Content-Type': 'application/json' },
              body: JSON.stringify({ fullName, age, gender, salary, workExperience, cityResidence })
            });
      
            if (response.ok) {
              success = true;
              error = '';
              fullName = '';
              age = 0;
              gender = '';
              salary = 0
              workExperience = ''
              cityResidence = ''
            } else {
              const data = await response.json();
              error = data.message || 'Произошла ошибка при отправке запроса';
            }
          } catch (err) {
            error = 'Ошибка подключения';
          }
        };
      </script>
    
      <div class="container">

        <h1>Добавление персоны</h1>
        <form on:submit|preventDefault={handleSubmit}>
          <div>
            <label for="fullName">Имя пользователя:</label>
            <input id="fullName" type="text" bind:value={fullName} required />
          </div>
          
          <div>
            <label for="age">Возраст:</label>
            <input id="age" type="text" bind:value={age} required />
          </div>
          
          <div>
            <label for="gender">Пол:</label>
            <input id="gender" type="text" bind:value={gender} required />
          </div>

          <div>
            <label for="salary">Зарплата:</label>
            <input id="salary" type="text" bind:value={salary} required />
          </div>

          <div>
            <label for="workExperience">Стаж работы:</label>
            <input id="workExperience" type="text" bind:value={workExperience} required />
          </div>


          <div>
            <label for="cityResidence">Место жительства:</label>
            <input id="cityResidence" type="text" bind:value={cityResidence} required />
          </div>
          
        {#if success}
          <p class="success">Пользователь добавлен!</p>
        {/if}
        
        {#if error}
          <p class="error">{error}</p>
        {/if}
          
          <Button title='Добавить'></Button>
        </form>
        </div>
      
      
      <style>
        .container{
          max-width: 1080px;
          margin: 0px auto;
        }
        body{
        background-color: #FBFBFD;
        color: #163309;
        }
        form {
          display: flex;
          flex-direction: column;
          max-width: 300px;
          margin: auto;
        }
        div {
          display: flex;
          flex-direction: column;
          margin-bottom: 10px;
        }
        .error {
          color: red;
        }
        .success{
            color: darkgreen;
        }
        label{
          font-size: 16px;
          color: #163309;
        }
        input{
          border: 0px;
          padding: 10px;
          background-color: white;
          -webkit-box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
          -moz-box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
          box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);    
    }
    </style>