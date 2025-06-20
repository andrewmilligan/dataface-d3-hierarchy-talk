<script>
  import Group from "./Group.svelte";

  let { nodes, level = 0 } = $props();

  const colors = [
    "#E58606",
    "#5D69B1",
    "#52BCA3",
    "#99C945",
    "#CC61B0",
    "#24796C",
    "#DAA51B",
    "#2F8AC4",
    "#764E9F",
    "#ED645A",
    "#CC3A8E",
    "#A5AA99",
  ];

  const color = colors[level % colors.length];
</script>

{#each nodes as node}
  <circle
    cx={node.x}
    cy={node.y}
    r={node.r}
    fill={color}
    fill-opacity="0.1"
    stroke={color}
  />

  {#if node.children}
    <Group
      nodes={node.children}
      level={level + 1}
    />
  {/if}
{/each}
