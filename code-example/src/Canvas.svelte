<script>
  import { stratify, pack, hierarchy } from "d3-hierarchy";
  import Group from "./Group.svelte";

  let {
    width = 500,
    height = width,
    padding = 3,
    sizeFocused = 10,
    sizeOther = 2,
  } = $props();

  // Set up some dummy data (objects with `name` and `group`)
  const focused = ["Alice", "Bob", "Claire", "David", "Eunice"];
  const data = [
    { name: "Alice" },
    { name: "Bob" },
    { name: "Claire" },
    { name: "David" },
    { name: "Eunice" },
    { name: "Frank" },
    { name: "Gabrielle" },
    { name: "Harry" },
    { name: "Ingrid" },
    { name: "James" },
    { name: "Katy" },
  ];
  const dataWithGroups = data.map((d) => ({
    ...d,
    group: focused.includes(d.name) ? "focused" : "root",
  }));

  // Add in the "made up" nodes to group our data points under
  const dataToStratify = [
    { name: "root", group: "" },
    { name: "focused", group: "root" },
    ...dataWithGroups,
  ];

  // Compute the layout tree with sizing information
  const root = $derived.by(() => {
    // First, we "stratify" our data
    const strat = stratify()
      .id((d) => d.name)
      .parentId((d) => d.group);
    const stratifiedData = strat(dataToStratify);

    // Next, we put it in a hierarchy, summing up values for sub-trees
    const dataHierarchy = hierarchy(stratifiedData)
      .sum((d) => d.data.group === "focused" ? sizeFocused : sizeOther);

    // Last, we create a circle-pack layout of nodes
    const makePack = pack()
      .size([width, height])
      .padding(padding);
    return makePack(dataHierarchy);
  });

  console.log(root);
</script>

<svg width={width} height={height}>
  <Group nodes={[root]} />
</svg>
