
<script>
    import { goto } from '$app/navigation';
  
    function goToUsers() {
      goto('/users');
    }
  </script>
  
  <div class="flex flex-col items-center justify-center min-h-screen bg-gradient-to-br from-blue-100 to-blue-300 text-center px-4">
    <h1 class="text-4xl md:text-6xl font-bold mb-4">Welcome to User Manager</h1>
    <p class="text-lg md:text-xl mb-8">Manage, search, and edit users easily.</p>
    <button on:click={goToUsers} class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-3 rounded-full text-lg">
      Go to Dashboard
    </button>
  </div>
  