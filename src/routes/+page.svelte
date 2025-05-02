<script>
  import { goto } from '$app/navigation';

  function goToLogin() {
    goto('/login'); // Assuming you have a /login route
  }

  function goToSignup() {
    goto('/signup'); // Assuming you have a /signup route
  }
</script>

<div class="min-h-screen bg-gradient-to-br from-blue-200 to-indigo-300 flex flex-col justify-center items-center">
  <div class="text-center mb-8">
    <h1 class="text-4xl font-bold text-gray-800 mb-2">Welcome!</h1>
    <p class="text-lg text-gray-600">Join our amazing community or sign in to continue.</p>
  </div>

  <div class="flex space-x-4">
    <button
      on:click={goToLogin}
      class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 px-6 rounded-full focus:outline-none focus:shadow-outline transition duration-200"
    >
      Log In
    </button>
    <button
      on:click={goToSignup}
      class="bg-teal-500 hover:bg-teal-600 text-white font-bold py-3 px-6 rounded-full focus:outline-none focus:shadow-outline transition duration-200"
    >
      Sign Up
    </button>
  </div>
</div>