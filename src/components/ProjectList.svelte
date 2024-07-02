<script lang="ts">
  export let projects: { title: string, description: string }[];
</script>

<div class="ex">
  <h2 class="subtit">Some Examples of Website Projects</h2>
  <div class="examples">
    <div class="img">
      <div class="w1">
        <img src="/img/w1.png" alt="W1" width="250" height="220">
      </div>
      <div class="w2">
        <img src="/img/w2.png" alt="W2" width="290" height="220">
      </div>
    </div>
  </div>
</div>

<div class="subtitle2">
  <h2>My Background Projects</h2>
</div>
<div class="subpar2">
  <ul>
    {#each projects as project}
      <li>
        <p class="li_title">{project.title}</p>
        <p>{project.description}</p>
      </li>
    {/each}
    <li>
      These and many other works are presented in my GitHub, by clicking on the link you can get acquainted with them, I try to update it regularly.
    </li>
  </ul>
</div>

<style>
  .ex {
    padding-left: 220px;
    padding-top: 70px;
    font-weight: 400;
    font-size: 17px;
  }
  .subtit{
    
    padding-top: 120px;
  }
  .examples {
    padding-top: 30px;
    padding-left: 270px;
  }
  .img {
    display: flex;
    gap: 30px;
    align-content: center;
  }
  .w1, .w2 {
    padding-top: 15px;
  }
  .subtitle2 {
    padding-left: 220px;
    padding-top: 40px;
    font-size: 17px;
  }
  .subpar2 {
    padding-left: 440px;
    padding-right: 42px;
    font-size: 17px;
    font-weight: 400;
    padding-top: 40px;
    width: 700px;
    padding-bottom: 50px;
  }
  .li_title {
    font-weight: bold;
  }
</style>
