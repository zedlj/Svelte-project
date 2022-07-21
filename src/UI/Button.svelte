<script>
    export let type = "button";
    export let href = null;
    export let mode = null;
    export let color = null;
</script>

<style>
    /* input, textarea {
        display: block;
        width: 100%;
        font: inherit;
        border: none;
        border-bottom: 2px solid #ccc;
        border-radius: 3px 3px 0 0;
        background: white;
        padding: 0.15rem 0.25rem;
        transition: border-color 0.1s ease-out;
    }

    input:focus,
    textarea:focus {
        border-color: #e40763;
        outline: none;
    }

    label {
    display: block;
        margin-bottom: 0.5rem;
        width: 100%;
    } */

    .form-control {
        padding: 0.5rem 0;
        width: 100%;
        margin: 0.25rem 0;
    }

    .success {
        color: green;
        outline: green;
    }

</style>

{#if href}
<a href="{href}">
    <slot />
</a>
{:else}
<button class="{mode} {color}" type="{type}" on:click>
    <slot />
</button>
{/if}