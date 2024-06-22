<script>
  import { themes } from "./themes.js";
  import { onMount } from "svelte";

  let themeIndex =
    parseInt(localStorage.getItem("BLOGS_THEME_INDEX")) ||
    Math.floor(Math.random() * themes.length);
  localStorage.setItem("BLOGS_THEME_INDEX", themeIndex.toString());

  $: theme = themes[themeIndex];

  function changeTheme() {
    themeIndex = (themeIndex + 1) % themes.length;
    localStorage.setItem("BLOGS_THEME_INDEX", themeIndex.toString());
  }

  let blogs = [];
  onMount(async () => {
    blogs = await fetch(
      "https://raw.githubusercontent.com/nobleknightt/bucket/main/blogs.json",
    ).then((response) => response.json());
  });
</script>

<main
  class="w-screen h-screen p-4 flex flex-col items-center gap-8 {theme.backgroundColor} {theme.textColor} overflow-x-hidden"
>
  <div class="w-full flex gap-4 justify-between">
    <h1 class="w-full flex-1 text-6xl font-bold text-center">Blogs</h1>
    <button
      class="cursor-pointer {theme.backgroundColor_Card} w-24 font-semibold py-1 m-auto rounded-md"
      on:click={changeTheme}>{theme.name}</button
    >
  </div>
  <ul class="w-full grid grid-cols-[repeat(auto-fit,minmax(16rem,1fr))] gap-4">
    {#each blogs as blog}
      <li
        class="p-2 flex flex-col gap-2 {theme.backgroundColor_Card} rounded-lg"
      >
        <a href={blog.url} class="text-2xl font-medium flex-1" target="_blank"
          >{blog.name}</a
        >
        <ul class="flex flex-wrap gap-2">
          {#each blog.tags as tag}
            <span class="{theme.backgroundColor_Tag} rounded-md px-2"
              >{tag}</span
            >
          {/each}
        </ul>
      </li>
    {/each}
  </ul>
</main>
