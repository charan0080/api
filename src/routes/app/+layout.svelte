<script lang="ts">
    import { goto } from '$app/navigation';
    import '@fortawesome/fontawesome-free/css/all.min.css';
    import Header from '../../components/Header.svelte';

  let issidebar=false
    function goToDashboard() {
      goto('/app/dashboard');
    }
  
    function goToDetails() {
      goto('/app/details');
    }

    function goToUserListing() {
    goto('/app/users');
  }
  function openSidebar() {
		issidebar = true;
	}

	function closeSidebar() {
		issidebar = false;
	}
  
  </script>
<Header on:menuToggle={() => issidebar = !issidebar} />

  
  <div class="flex min-h-screen bg-white">
 

    {#if issidebar}

    <div class="side fixed  inset-0 w-64 text-white p-6 space-y-4 shadow-lg z-30 lg:hidden">
        <div class="py-2">
   
</div>
        <button on:click={goToDashboard} class="block w-full text-left px-4 py-2 rounded hover:bg-blue-600 transition">Dashboard</button>
        <button on:click={goToDetails} class="block w-full text-left px-4 py-2 rounded hover:bg-blue-600 transition">Details</button>
        <button on:click={goToUserListing} class="block w-full text-left px-4 py-2 rounded hover:bg-blue-600 transition">User Listing</button>
    </div> {/if}
    <aside class="sidebar hidden lg:block w-64 text-white p-6 space-y-4 shadow-lg">
        <button on:click={goToDashboard} class="block w-full text-black text-left px-4 py-2 rounded-full hover:scale-110  transition-transform duration-300 ">Dashboard</button>
        <button on:click={goToDetails} class="block w-full text-black text-left px-4 py-2 rounded-full hover:scale-110  transition-transform duration-300">Details</button>
        <button on:click={goToUserListing} class="block w-full  text-black text-left px-4 py-2 rounded-full hover:scale-110  transition-transform duration-300">User Listing</button>
      </aside>  
      
      
        <slot />
      
      </div>
<style>
  .sidebar{
    background-color: #89c2d9;
  }
</style>