<script>
    //hook
    import { onMount } from "svelte"; 

    export let urlResultado;
    
    let textarea;

    onMount(() => {
        textarea.select() //seleccion de la variable
        document.execCommand("copy") //comando de copiar
    })
</script>

<textarea bind:value={urlResultado} bind:this={textarea}></textarea>