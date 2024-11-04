<script lang="ts">
  import MenuBar from "$lib/components/layout/MenuBar.svelte";
  import { ModeWatcher } from "mode-watcher";
  import "../app.css";
</script>

<!-- Contexts -->
<ModeWatcher />

<MenuBar />
<slot />
