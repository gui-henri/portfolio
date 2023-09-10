<script>
    import Hamburguer from "./Hamburguer.svelte";
    import { fly } from "svelte/transition";

    export let open = false;
    export let onClick = () => {
        open = !open;
    
    };
</script>

<div class="relative flex flex-col justify-end lg:hidden">
    <Hamburguer width={80} {open} {onClick} />

    {#if open}
        <nav transition:fly={{y: -200, duration: 300 }}>
            <div class=" w-32 ml-[-48px] bg-white absolute font-semibold flex flex-col shadow-2xl border-2 border-black text-center rounded-md">
                <a href="/" class="p-4 mt-4 mb-4">Home</a>
                <a href="/portfolio" class="p-4 mt-4 mb-4">My Portfolio</a>
                <a href="/blog" class="p-4 mt-4 mb-4">My Blog</a>
                <a href="/contact" class="p-4 mt-4 mb-2">Contact</a>
            </div>
        </nav>
    {/if}
</div>