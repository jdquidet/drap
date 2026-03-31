<script lang="ts">
  import AvailableDraftees from '$lib/features/drafts/draftees/available/index.svelte';
  import DraftedDraftees from '$lib/features/drafts/draftees/drafted/index.svelte';
  import InterestedDraftees from '$lib/features/drafts/draftees/interested/index.svelte';
  import { Badge } from '$lib/components/ui/badge';
  import type { Lab } from '$lib/features/drafts/types';

  interface Props {
    draftId: string;
    round: number;
    lab: Lab;
  }

  const { draftId, round, lab }: Props = $props();
</script>

<div
  class="grid w-full gap-2 border-b px-1 py-2 text-left last:border-0 lg:grid-cols-[minmax(0,1fr)_auto] lg:items-start"
>
  <div class="grid min-w-0 gap-2 lg:grid-cols-[auto_minmax(0,1fr)] lg:items-start lg:gap-3">
    {#if lab.quota !== 0}
      <Badge
        variant="outline"
        class="h-fit border-warning bg-warning/10 font-mono text-xs uppercase"
      >
        {lab.quota} maximum
      </Badge>
    {/if}
    {#if lab.quota === 0}
      <h5 class="text-lg leading-5 font-medium text-muted-foreground">{lab.name}</h5>
    {:else}
      <h5 class="text-lg leading-5 font-medium">{lab.name}</h5>
    {/if}
  </div>
  <div class="flex gap-1 lg:self-start">
    <!-- Members -->
    <DraftedDraftees {draftId} {lab} />
    <!-- Preferred -->
    <AvailableDraftees {draftId} {round} {lab} variant="see-preferred" />
    <!-- Interested -->
    <InterestedDraftees {draftId} {round} {lab} />
  </div>
</div>
