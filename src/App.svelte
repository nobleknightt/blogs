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
      class="cursor-pointer {theme.backgroundColor_Card} w-28 font-semibold py-1 m-auto rounded-md flex items-center justify-center pl-2"
      on:click={changeTheme}
    >
      <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960" width="24px" fill={`${theme.hexCode}`}><path d="M480-80q-82 0-155-31.5t-127.5-86Q143-252 111.5-325T80-480q0-83 32.5-156t88-127Q256-817 330-848.5T488-880q80 0 151 27.5t124.5 76q53.5 48.5 85 115T880-518q0 115-70 176.5T640-280h-74q-9 0-12.5 5t-3.5 11q0 12 15 34.5t15 51.5q0 50-27.5 74T480-80Zm0-400Zm-220 40q26 0 43-17t17-43q0-26-17-43t-43-17q-26 0-43 17t-17 43q0 26 17 43t43 17Zm120-160q26 0 43-17t17-43q0-26-17-43t-43-17q-26 0-43 17t-17 43q0 26 17 43t43 17Zm200 0q26 0 43-17t17-43q0-26-17-43t-43-17q-26 0-43 17t-17 43q0 26 17 43t43 17Zm120 160q26 0 43-17t17-43q0-26-17-43t-43-17q-26 0-43 17t-17 43q0 26 17 43t43 17ZM480-160q9 0 14.5-5t5.5-13q0-14-15-33t-15-57q0-42 29-67t71-25h70q66 0 113-38.5T800-518q0-121-92.5-201.5T488-800q-136 0-232 93t-96 227q0 133 93.5 226.5T480-160Z"/></svg>
      <span class="grow px-2">{theme.name}</span>
    </button>
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
