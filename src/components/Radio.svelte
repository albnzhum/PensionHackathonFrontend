<script>
    export let options;
    export let userSelected = "РЕЗУЛЬТАТЫ";
  
  
  </script>
  
  <div class="cases__ctgr _container">
    {#each options as { value, label }}
      <label for="{value}" class="ctgr__btn">
        <input
          type="radio"
          value={label}
          id="{value}"
          class="btn__radio"
          bind:group={userSelected}
        />
        <span>{label}</span>
      </label>
    {/each}
  </div>
  
  <style>
  .cases__ctgr{
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    margin-bottom: 50px;
    background-color: #fff;
    padding: 20px;
    border-radius: 15px;
  }
  .ctgr__btn{
    color: rgba(42, 38, 38, 0.6);
    transition: ease 0.3s all;
    font-size: 16px;
    font-style: normal;
    font-weight: 600;
    line-height: 100%;
    border-radius: 19px;
  
    background: #fff;
    padding: 12px 24px;
    justify-content: center;
    align-items: center;
  }
  .ctgr__btn:not(:last-child){
    margin-right: 10px;
  }
  .btn__radio{
    display: none;
  }
  .cases__ctgr input:checked + span {
    border-radius: 4px;
    background: #163309;
    transition: 0.3s ease all;
    color: #fff;
    padding: 12px 40px;
    justify-content: center;
    align-items: center;
    border: 2px solid var(--main-color, #163309);
  }
  </style>