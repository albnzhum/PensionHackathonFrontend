<script>
    export let casesBot
    export let casesWeb
    export let radioValue
  </script>
  
  
  <div class="cases__case">
      
        {#if radioValue === "PERSONS"}
          {#each casesBot.concat(casesWeb) as {src, title, subtitle}}
            <div class="case__block">
              <a class="case__title" target="_blank" href="{title}">{title}</a>
              <p class="case__subtitle">{subtitle}</p>
            </div>
          {/each}
        {:else if radioValue === "DIAGRAMS"}
          {#each casesWeb as {src, title, subtitle}}
            <div class="case__block">
              <img src="{src}" alt="img" class="case__img">
              <a class="case__title" target="_blank" href="{title}">{title}</a>
              <p class="case__subtitle">{subtitle}</p>
            </div>
          {/each}
        <!-- {:else if radioValue === ""}
          {#each casesBot as {src, title, subtitle}}
            <div class="case__block">
              <img src="{src}" alt="img" class="case__img">
              <p class="case__title">{title}</p>
              <p class="case__subtitle">{subtitle}</p>
            </div>
          {/each} -->
        {/if}
  </div>
  
  <style>
  
  @keyframes show {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  .cases__case{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
  
    font-family: "Noto Sans";
  }
  .case__block{
    animation: 1s show ease;
    display: flex;
    flex-direction: column;
    margin-right: 45px;
    max-width: 450px;
    max-height: 450px;
    margin-top: 60px;
    margin-bottom: 20px;
    border-radius: 30px;
  
    transition: all 0.3s ease;
    border: 1px solid #F0ECEC;
    background: #FFF;
    box-shadow: 0px 4px 42px 1px rgba(217, 217, 217, 0.20);
  }
  .case__img{
    border-radius: 30px 30px 0 0;
  
  }
  .case__title{
    overflow: hidden;
    color: var(--main-color, #3071E7);
    text-overflow: ellipsis;
    margin: 20px 20px;
  
    font-size: 15px;
    font-style: normal;
    font-weight: 400;
    line-height: normal;
    letter-spacing: 0.225px;
    text-transform: uppercase;
  }
  .case__subtitle{
    overflow: hidden;
    pointer-events: all;
    color: var(--text-primary, #313131);
    text-overflow: ellipsis;
    margin-left: 20px;
    padding-bottom: 40px;
  
    font-size: 22px;
    font-style: normal;
    font-weight: 600;
    line-height: normal;
    letter-spacing: 0.33px;
  }
  </style>