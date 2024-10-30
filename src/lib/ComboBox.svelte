<script lang="ts">
    import {
      createCombobox,
      melt,
      type ComboboxOptionProps,
    } from '@melt-ui/svelte';
    import { fly } from 'svelte/transition';
    
    let options: string[] = ["One", "Two", "Three", "NaN", "Five"];  
    const toOption = (option: string): ComboboxOptionProps<string> => ({ value: option, label: option, disabled: option == "NaN" });
  
    export let id: string;

    let {
      elements: { menu, input, option, label },
      states: { open, inputValue, touchedInput, selected },
      helpers: { isSelected },
    } = createCombobox<string>({
      forceVisible: true,
      positioning: {
        placement: "bottom",
        sameWidth: true,
        gutter: 0
      }
    });
  
    $: if (!$open) {
      $inputValue = $selected?.label ?? '';
    }
  
    $: filteredOptions = $touchedInput
      ? options.filter((option) => {
          const normalizedInput = $inputValue.toLowerCase();
          return option.toLowerCase().includes(normalizedInput);
        })
      : options;
</script>

<div class="layout">
    <input use:melt={$input} id={id} placeholder="number">

    <svg viewBox="0 0 100 100">            
        {#if $open}
        <path d="M30,40 L50,60 L70,40" x1="40" y1="30" x2="60" y2="50" />
        {:else}
        <path d="M40,30 L60,50 L40,70" x1="40" y1="30" x2="60" y2="50" />
        {/if}
    </svg>
</div>

{#if $open}
    <ul use:melt={$menu} transition:fly={{ duration: 150, y: -5 }}>
        <!-- svelte-ignore a11y-no-noninteractive-tabindex -->
        <div tabindex="0">
            {#each filteredOptions as opt, index (index)}
                <li use:melt={$option(toOption(opt))}>
                    <span>{opt}</span>
                    {#if $isSelected(opt)}
                        <svg viewBox="0 0 200 200">            
                            <path d="M30,122 L80,170 L170,20" stroke-linecap="round"/>
                        </svg>
                    {/if}
                </li>
            {:else}
                <li>
                No results found
                </li>
            {/each}
        </div>
    </ul>
{/if}
  
<style>
    .layout {
        display: grid;
        grid-template-columns: 1fr 22px;        

        &>input {
            grid-area: 1/1/2/3;
            font-weight: bold;
            min-height: 22px;
            border: 1px solid #ABADB3;
            outline: none;
            &:hover, &:focus-visible {
                border-color: #569DE5;
            }
        }

        &>svg {
            grid-area: 1/2/2/3;
            pointer-events: none;
        }
    }

    ul {
        background: white;
        border: 1px solid;
        border-image: var(--gradient-border) 1;
        border-top-width: 0;
        font-size: 9pt;
        padding: 0;
        margin: 0;

        &>div {
            display: flex;
            flex-direction: column;
        }

        li {
            height: 22px;
            display: flex;
            align-items: center;
            gap: 5px;

            &:not([data-disabled]) {
                font-weight: bold;
                &:hover, &:focus-within {
                    background-color: #ddd;
                }
            }

            svg {
                width: 10px;
                height: 10px;
                stroke: black;
                stroke-width: 20px;
                fill: none; 
            }
        }
    }
</style>
  
  