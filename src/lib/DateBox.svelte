<script lang="ts">
    import { createDatePicker, melt } from '@melt-ui/svelte'
    import type { DateValue } from '@internationalized/date'

    let props: { id: string, value?: DateValue } = $props();
    let {
        elements: {
            calendar,
            cell,
            content,
            field,
            grid,
            heading,
            nextButton,
            prevButton,
            segment,
            trigger,
            hiddenInput
        },
        states: { months, headingValue, weekdays, segmentContents, value },
        helpers: { isDateDisabled, isDateUnavailable }
    } = createDatePicker({defaultValue: props.value, locale: "en-AU" });
</script>

<div use:melt={$field} class="box">
    {#each $segmentContents as seg}
        <div class="seg" use:melt={$segment(seg.part)}>
            {seg.value}
        </div>
    {/each}
    <input use:melt={$hiddenInput} id={props.id} />
    <div class="gap"></div>
    <button use:melt={$trigger} class="picker">
        📅
    </button>
</div>

<div use:melt={$content}>
    <div use:melt={$calendar}>
        <header>
            <button use:melt={$prevButton} class="nav" aria-label="Previous Month">
                <svg viewBox="0 0 100 100" stroke="#000">            
                    <path d="M56,25 L23,50 56,75" x1="40" y1="30" x2="60" y2="50" />
                </svg>                
            </button>
            <div use:melt={$heading}>
                {$headingValue}
            </div>
            <button use:melt={$nextButton} class="nav" aria-label="Next Month">
                <svg viewBox="0 0 100 100" stroke="#000">            
                    <path d="M33,25 L66,50 33,75" x1="40" y1="30" x2="60" y2="50" />
                </svg>    
            </button>
        </header>

        {#each $months as month}
        <table use:melt={$grid}>
            <thead aria-hidden="true">
            <tr>
                {#each $weekdays as day}
                <th>
                    {day}
                </th>
                {/each}
            </tr>
            </thead>
            <tbody>
            {#each month.weeks as days}
                <tr>
                {#each days as date}
                    <td
                    class="gridcell"
                    role="gridcell"
                    aria-disabled={$isDateDisabled(date) || $isDateUnavailable(date)}>
                    <div use:melt={$cell(date, month.value)}>
                        {date.day}
                    </div>
                    </td>
                {/each}
                </tr>
            {/each}
            </tbody>
        </table>
        {/each}
    </div>
</div>

<style>
    .box {
        font-weight: bold;
        min-height: 22px;
        border: 1px solid #ABADB3;
        &:hover, &:focus-within {
            border-color: #569DE5;
        }

        display: flex;
        align-items: center;

        max-width: 100px;
        padding: 2px;
    }
    
    .seg {
        outline: none;
        &:focus-visible {
            background-color: #ABADB3;
        }
    }

    .gap {
        flex: 1;
    }

    .picker {
        padding: 1px 1px 1px 2px;
        margin: 0;
        background: none;
        border: none;
        outline: none;
        &:focus-visible, &[data-state=open] {
            background-color: #ABADB3;
        }
    }

    [data-melt-calendar] {
        background: white;
        border: 1px solid;
        border-image: var(--gradient-border) 1;
        font-size: 9pt;

        header {
            background-color: #ddd;
            display: flex;
            align-items: center;
            justify-content: space-between;   
        }
    }

    .nav {
        padding: 0;
        outline: none;
        height: 20px;
        width: 20px;
        background: none;
        border: none;
        &:hover, &:active, &:focus-visible {
            & > svg {
                stroke: #222;
                fill: #222;
            }
        }
    }

    svg {
        width: 20px;
        height: 20px;
        stroke: #666;
        fill: #666;
    }

    .gridcell {
        min-width: 16px;
        text-align: end;
        cursor: default;

        &:hover, &:focus-within {
            background-color: #ddd;
        }

        &>div {
            outline: none;
        }
    }
</style>