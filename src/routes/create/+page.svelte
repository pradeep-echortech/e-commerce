<script>
    
    
    import Create from "../../components/create.svelte";
	import Delete from "../../components/delete.svelte";
    import Edit from "../../components/edit.svelte";
    let activeTab = Create

</script>
<h1 class="text-center py-3">Choose Your Action</h1>
    
<div class="container">
    <div class="text-center">

        <button class="btn btn-primary" on:click={()=>(activeTab = Create)}>Create</button>
        <button class="btn btn-primary" on:click={()=>(activeTab = Edit)}>Edit</button>
        <button class="btn btn-primary" on:click={()=>(activeTab = Delete)}>Delete</button>
    </div>
	<svelte:component this={activeTab} />
</div>
    