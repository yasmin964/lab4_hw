<!-- Header.svelte -->
<script lang="ts">
  
  export let headerLinks: { href: string; icon: string }[];
  export let headerContent: { href: string; text: string }[];
</script>

<header class="header">
  <div class="s_text">
    {#each headerLinks as link}
      <a href={link.href}>
        <img src={link.icon} alt="" width="20" height="20" />
      </a>
    {/each}
  </div>
  <div class="header__content">
    
      {#each headerContent as link}
        <a href={link.href}>{link.text}</a>
      {/each}
    
  </div>
</header>

<style>
  .header {
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 75px;
    background: rgb(34, 34, 34);
    color: white;
    width: 120%;
  }
  .s_text {
    display: flex;
    gap: 15px;
    padding-top: 15px;
  }
  .header__content {
    display: flex;
    gap: 30px;
    padding-top: 30px;
    padding-bottom: 20px;
    justify-content: center;
    font-size: 15px;
  }
</style>
