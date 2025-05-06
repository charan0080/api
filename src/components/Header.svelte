<script lang="ts">
    import { createEventDispatcher } from 'svelte';
    import '@fortawesome/fontawesome-free/css/all.min.css';
  
    const dispatch = createEventDispatcher<{ menuToggle: void }>();
  
    function toggleSidebar() {
      dispatch('menuToggle');
    }
  </script>
  
  <header class="header shadow-md px-4 py-3 flex justify-between items-center relative z-40">
    <!-- Menu Button -->
    <button
      class="lg:hidden text-gray-800 text-2xl"
      on:click={toggleSidebar}
      aria-label="Toggle Sidebar"
    >
      <i class="fa-solid fa-bars"></i>
    </button>
  
    <!-- Logo -->
    <div class=" text-xl font-bold text-black text-center w-full">User Listing</div>

  
    
  
  </header>
  <style>
    .header{
        background-color: #89c2d9;
    }
  </style>
  