<script lang="ts">
  import Check from "lucide-svelte/icons/check";
  import ChevronsUpDown from "lucide-svelte/icons/chevrons-up-down";
  import { tick } from "svelte";
  import * as Command from "$lib/components/ui/command/index.js";
  import * as Popover from "$lib/components/ui/popover/index.js";
  import { Button } from "$lib/components/ui/button/index.js";
  import { cn } from "$lib/utils.js";
  import { Badge } from "../ui/badge";

  const documents = [
    {
      id: "shared/RFD-01",
      value: "RFD-01",
      title: "JetStream Message Expiry",
      description: "...",
      project: "shared",
    },
  ];

  let open = false;
  let id = "";

  $: selectedValue = documents.find((f) => f.id === id);

  // We want to refocus the trigger button when the user selects
  // an item from the list so users can continue navigating the
  // rest of the form with the keyboard.
  function closeAndFocusTrigger(triggerId: string) {
    open = false;
    tick().then(() => {
      document.getElementById(triggerId)?.focus();
    });
  }
</script>

<section>
  <Popover.Root bind:open let:ids>
    <Popover.Trigger asChild let:builder>
      <Button
        builders={[builder]}
        variant="outline"
        role="combobox"
        aria-expanded={open}
        class="w-[400px] justify-between"
      >
        {#if selectedValue}
          <span class="flex flex-row gap-2 items-center">
            {#if id}
              <Badge variant="outline">{selectedValue.id}</Badge>
              <span>{selectedValue.title}</span>
            {/if}
          </span>
        {:else}
          Select a document...
        {/if}
        <ChevronsUpDown class="ml-2 h-4 w-4 shrink-0 opacity-50" />
      </Button>
    </Popover.Trigger>
    <Popover.Content class="w-[400px] p-0">
      <Command.Root>
        <Command.Input placeholder="Search framework..." />
        <Command.Empty>No framework found.</Command.Empty>
        <Command.Group>
          {#each documents as doc}
            <Command.Item
              value={doc.id}
              onSelect={(currentValue) => {
                id = currentValue;
                closeAndFocusTrigger(ids.trigger);
              }}
            >
              {doc.title}
            </Command.Item>
          {/each}
        </Command.Group>
      </Command.Root>
    </Popover.Content>
  </Popover.Root>
</section>
