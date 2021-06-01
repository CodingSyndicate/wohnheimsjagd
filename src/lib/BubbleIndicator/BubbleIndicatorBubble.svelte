<script>
    export let selected = false;
</script>

<div class="diashowIndicatorBubbleContainer" class:selected />

<style>
    .diashowIndicatorBubbleContainer {
        opacity: 0.5;
        background-color: grey;
        border-radius: 50%;
        width: 7px;
        height: 7px;
        margin: 0.75em;
    }
    .selected {
        scale: 1.5;
    }
</style>
