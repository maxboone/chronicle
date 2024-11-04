<script lang="ts">
  import User from "lucide-svelte/icons/circle-user-round";
  import CirclePlus from "lucide-svelte/icons/circle-plus";
  import Search from "lucide-svelte/icons/search";

  import LightSwitch from "./LightSwitch.svelte";
  import DocumentDropdown from "./DocumentDropdown.svelte";
  import { Button } from "$lib/components/ui/button";
</script>

<header class="w-full p-2 gap-1 border-b flex flex-row justify-between">
  <DocumentDropdown />
  <nav>
    <Button variant="outline" size="icon">
      <Search class="w-5" />
    </Button>
    <Button variant="outline" size="icon">
      <CirclePlus class="w-5" />
    </Button>
    <Button variant="outline" size="icon">
      <User class="w-5" />
    </Button>
    <LightSwitch />
  </nav>
</header>
