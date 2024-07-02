<script lang="ts">
 
  export let bio: { name: string, description: string };
  
</script>

<div class="top__content">
  <div class="content-container">
    <div class="subtitle1">
      <h2>Bio</h2>
    </div>
    <div class="subpar1">
      <p>{bio.description}</p>
    </div>
  </div>
</div>

<style>
  .subtitle1 {
    padding-top: 60px;
    padding-left: 220px;
    font-weight: 400;
    font-size: 17px;
  }
  .subpar1 {
    float: left;
    padding-left: 440px;
    padding-top: 17px;
    width: 700px;
    font-size: 17px;
    font-weight: 400;
  }
</style>
