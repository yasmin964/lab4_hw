<!-- ComicFetcher.svelte -->
<script lang="ts">
  import { onMount } from 'svelte';

  let email = '';
  let comicTitle = '';
  let comicImgSrc = '';
  let comicImgAlt = '';
  let comicDate = '';
  let showComic = false;

  async function fetchComicID(email: string): Promise<number> {
    const params = new URLSearchParams({ email });
    console.log('Fetching comic ID with email:', email); // Add logging
    const response = await fetch(`https://fwd.innopolis.university/api/hw2?${params.toString()}`);
    if (!response.ok) {
      throw new Error('Failed to fetch comic ID');
    }
    return response.json();
  }

  async function fetchComic(comicID: number): Promise<{ safe_title: string, img: string, alt: string, year: string, month: string, day: string }> {
    console.log('Fetching comic with ID:', comicID); // Add logging
    const response = await fetch(`https://fwd.innopolis.university/api/comic?id=${comicID}`);
    if (!response.ok) {
      throw new Error('Failed to fetch comic');
    }
    return response.json();
  }

  async function handleGetComic() {
    try {
      const comicID = await fetchComicID(email);
      console.log('Comic ID received:', comicID); // Add logging
      const comicData = await fetchComic(comicID);

      comicTitle = comicData.safe_title;
      comicImgSrc = comicData.img;
      comicImgAlt = comicData.alt;
      const dateString = `${comicData.year}-${comicData.month}-${comicData.day}`;
      const date = new Date(dateString);
      comicDate = date.toLocaleDateString();
      showComic = true;
    } catch (error) {
      console.error('Failed to fetch comic:', error);
      comicTitle = 'Error loading comic';
      comicImgSrc = '';
      comicImgAlt = '';
      comicDate = '';
      showComic = true;
    }
  }
</script>

<div class="comic">
  <div class="comic__head">
    <div class="comic__name">
      <h1>XKCD Comic Fetcher</h1>
    </div>
  
    <div class="comic__placeholders">
      <form id="email-form" on:submit|preventDefault={handleGetComic}>
        <input type="email" name="email" placeholder="Enter your email" bind:value={email} required />
      </form>
      <div class="comic__button">
        <button id="get-comic-btn" on:click={handleGetComic}>Get a random comic</button>
      </div>
    </div>
    
  </div>

  {#if showComic}
    <div id="comic-container">
      <h2 id="safe_title">{comicTitle}</h2>
      <img id="comic-img" src={comicImgSrc} alt={comicImgAlt} />
      <p id="comic-date">{comicDate}</p>
    </div>
  {/if}
</div>

<style>
  .comic {
    display: flex;
    justify-content: space-around;
    flex-direction: row;
    flex-wrap: nowrap;
    color: rgb(34, 34, 34);
    font-family: 'Lato', sans-serif;
    font-size: 19px;
    font-weight: 400;
    background-color: darkgray;
    
    width: 100%;
    border: dotted grey 2px;
    margin-top: 100px;
    padding: 82px;
  }

  .comic__head {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    max-width: 800px;
    margin: 0 auto;
  }

  .comic__name {
    flex: 1;
  }
  .comic__placeholders{
    display: flex;
    flex-direction: column;
    align-items: center;

  }

  .comic__button {
    flex: 1;
    text-align: right;
  }

  #safe_title {
    padding-top: 20px;
    margin-bottom: 10px;
    text-align: center;
  }

  #comic-date {
    margin-bottom: 20px;
    text-align: center;
  }

  #comic-container {
    display: block;
  }
</style>
