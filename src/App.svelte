<script>
  import blogs from "./blogs.json";

  const themes = [
    {
      name: "Slate",
      backgroundColor: "bg-slate-50",
      backgroundColor_Card: "bg-slate-100",
      backgroundColor_Tag: "bg-slate-200",
      textColor: "text-slate-950",
    },
    {
      name: "Gray",
      backgroundColor: "bg-gray-50",
      backgroundColor_Card: "bg-gray-100",
      backgroundColor_Tag: "bg-gray-200",
      textColor: "text-gray-950",
    },
    {
      name: "Zinc",
      backgroundColor: "bg-zinc-50",
      backgroundColor_Card: "bg-zinc-100",
      backgroundColor_Tag: "bg-zinc-200",
      textColor: "text-zinc-950",
    },
    {
      name: "Neutral",
      backgroundColor: "bg-neutral-50",
      backgroundColor_Card: "bg-neutral-100",
      backgroundColor_Tag: "bg-neutral-200",
      textColor: "text-neutral-950",
    },
    {
      name: "Stone",
      backgroundColor: "bg-stone-50",
      backgroundColor_Card: "bg-stone-100",
      backgroundColor_Tag: "bg-stone-200",
      textColor: "text-stone-950",
    },
    {
      name: "Red",
      backgroundColor: "bg-red-50",
      backgroundColor_Card: "bg-red-100",
      backgroundColor_Tag: "bg-red-200",
      textColor: "text-red-950",
    },
    {
      name: "Orange",
      backgroundColor: "bg-orange-50",
      backgroundColor_Card: "bg-orange-100",
      backgroundColor_Tag: "bg-orange-200",
      textColor: "text-orange-950",
    },
    {
      name: "Amber",
      backgroundColor: "bg-amber-50",
      backgroundColor_Card: "bg-amber-100",
      backgroundColor_Tag: "bg-amber-200",
      textColor: "text-amber-950",
    },
    {
      name: "Yellow",
      backgroundColor: "bg-yellow-50",
      backgroundColor_Card: "bg-yellow-100",
      backgroundColor_Tag: "bg-yellow-200",
      textColor: "text-yellow-950",
    },
    {
      name: "Lime",
      backgroundColor: "bg-lime-50",
      backgroundColor_Card: "bg-lime-100",
      backgroundColor_Tag: "bg-lime-200",
      textColor: "text-lime-950",
    },
    {
      name: "Green",
      backgroundColor: "bg-green-50",
      backgroundColor_Card: "bg-green-100",
      backgroundColor_Tag: "bg-green-200",
      textColor: "text-green-950",
    },
    {
      name: "Emerald",
      backgroundColor: "bg-emerald-50",
      backgroundColor_Card: "bg-emerald-100",
      backgroundColor_Tag: "bg-emerald-200",
      textColor: "text-emerald-950",
    },
    {
      name: "Teal",
      backgroundColor: "bg-teal-50",
      backgroundColor_Card: "bg-teal-100",
      backgroundColor_Tag: "bg-teal-200",
      textColor: "text-teal-950",
    },
    {
      name: "Cyan",
      backgroundColor: "bg-cyan-50",
      backgroundColor_Card: "bg-cyan-100",
      backgroundColor_Tag: "bg-cyan-200",
      textColor: "text-cyan-950",
    },
    {
      name: "Sky",
      backgroundColor: "bg-sky-50",
      backgroundColor_Card: "bg-sky-100",
      backgroundColor_Tag: "bg-sky-200",
      textColor: "text-sky-950",
    },
    {
      name: "Blue",
      backgroundColor: "bg-blue-50",
      backgroundColor_Card: "bg-blue-100",
      backgroundColor_Tag: "bg-blue-200",
      textColor: "text-blue-950",
    },
    {
      name: "Indigo",
      backgroundColor: "bg-indigo-50",
      backgroundColor_Card: "bg-indigo-100",
      backgroundColor_Tag: "bg-indigo-200",
      textColor: "text-indigo-950",
    },
    {
      name: "Violet",
      backgroundColor: "bg-violet-50",
      backgroundColor_Card: "bg-violet-100",
      backgroundColor_Tag: "bg-violet-200",
      textColor: "text-violet-950",
    },
    {
      name: "Purple",
      backgroundColor: "bg-purple-50",
      backgroundColor_Card: "bg-purple-100",
      backgroundColor_Tag: "bg-purple-200",
      textColor: "text-purple-950",
    },
    {
      name: "Fuchsia",
      backgroundColor: "bg-fuchsia-50",
      backgroundColor_Card: "bg-fuchsia-100",
      backgroundColor_Tag: "bg-fuchsia-200",
      textColor: "text-fuchsia-950",
    },
    {
      name: "Pink",
      backgroundColor: "bg-pink-50",
      backgroundColor_Card: "bg-pink-100",
      backgroundColor_Tag: "bg-pink-200",
      textColor: "text-pink-950",
    },
    {
      name: "Rose",
      backgroundColor: "bg-rose-50",
      backgroundColor_Card: "bg-rose-100",
      backgroundColor_Tag: "bg-rose-200",
      textColor: "text-rose-950",
    },
  ];

  let themeIndex = 0;
  $: theme = themes[themeIndex];

  function changeTheme() {
    themeIndex = (themeIndex + 1) % themes.length;
  }
</script>

<main
  class="w-screen h-screen p-4 pb-1 flex flex-col items-center gap-8 {theme.backgroundColor} {theme.textColor}"
>
  <div class="flex gap-4 justify-between w-full">
    <h1 class="flex-1 text-6xl font-bold w-full text-center">Blogs</h1>
    <button
      class="cursor-pointer {theme.backgroundColor_Tag} w-24 font-semibold py-1 m-auto rounded-md"
      on:click={changeTheme}>{theme.name}</button
    >
  </div>
  <ul class="w-full grid grid-cols-[repeat(auto-fill,minmax(16rem,1fr))] gap-4">
    {#each blogs as blog}
      <li
        class="w-full p-2 flex flex-col gap-2 {theme.backgroundColor_Card} rounded-lg"
      >
        <div>
          <a href={blog.url} class="text-2xl font-medium">{blog.name}</a>
        </div>
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
