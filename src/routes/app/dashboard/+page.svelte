<script>
  import { goto } from '$app/navigation';

  function goToUsers() {
    goto('/users');
  }

  function goToDetails() {
    goto('/details');
  }
</script>


  <!-- Main Content -->
  <main class="flex-1 flex items-center justify-center bg-white text-center px-4 min-h-screen">
    <div class="flex flex-col items-center justify-center">
      <h1 class="text-4xl animate-bounce md:text-6xl font-bold mb-4">
        Welcome to User Manager
      </h1>
      <p class="text-lg md:text-xl mb-8">
        Manage, search, and edit users easily.
      </p>
    </div>
  </main>
  

