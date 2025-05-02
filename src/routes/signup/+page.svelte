<script>
    import { goto } from '$app/navigation';
    let email = '';
    let password = '';
    let confirmPassword = '';
    let errorMessage = '';
    let successMessage = '';
  
    async function signup() {
      if (password !== confirmPassword) {
        errorMessage = 'Passwords do not match.';
        setTimeout(() => {
          errorMessage = '';
        }, 3000);
        return;
      }
  
      // In a real application, you would send this data to a server
      // to create a new user account.
      console.log('Signing up with:', { email, password });
  
      // For this example, we'll just simulate success
      successMessage = 'Account created successfully! Redirecting to login...';
      setTimeout(() => {
        successMessage = '';
        goto('/login'); // Replace '/login' with your actual login route
      }, 2000);
    }
  </script>
  
  <div class="min-h-screen flex items-center justify-center bg-gradient-to-br from-green-100 to-teal-200">
    <div class="w-full max-w-md bg-white p-8 rounded-xl shadow-lg space-y-6">
      <div>
        <h2 class="text-3xl font-bold text-gray-800 text-center mb-4">Create Account</h2>
        <p class="text-gray-600 text-center">Sign up to join our community!</p>
      </div>
      <form on:submit|preventDefault={signup} class="space-y-4">
        <div>
          <label for="email" class="block text-gray-700 text-sm font-bold mb-2">Email Address</label>
          <input
            type="email"
            id="email"
            placeholder="you@example.com"
            bind:value={email}
            class="shadow appearance-none border rounded w-full py-3 px-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            required
          />
        </div>
        <div>
          <label for="password" class="block text-gray-700 text-sm font-bold mb-2">Password</label>
          <input
            type="password"
            id="password"
            placeholder="********"
            bind:value={password}
            class="shadow appearance-none border rounded w-full py-3 px-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            required
          />
        </div>
        <div>
          <label for="confirm-password" class="block text-gray-700 text-sm font-bold mb-2">Confirm Password</label>
          <input
            type="password"
            id="confirm-password"
            placeholder="********"
            bind:value={confirmPassword}
            class="shadow appearance-none border rounded w-full py-3 px-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            required
          />
        </div>
  
        {#if errorMessage}
          <div class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative" role="alert">
            <strong class="font-bold">Error!</strong>
            <span class="block sm:inline">{errorMessage}</span>
          </div>
        {/if}
  
        {#if successMessage}
          <div class="bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded relative" role="alert">
            <strong class="font-bold">Success!</strong>
            <span class="block sm:inline">{successMessage}</span>
          </div>
        {/if}
  
        <button
          type="submit"
          class="w-full bg-teal-600 hover:bg-teal-700 text-white font-bold py-3 px-4 rounded-lg focus:outline-none focus:shadow-outline transition duration-200"
        >
          Sign Up
        </button>
        <div class="text-center">
          <p class="inline-block align-baseline text-sm text-gray-600">
            Already have an account?
            <a href="/login" class="font-semibold text-teal-500 hover:text-teal-800">Log In</a>
          </p>
        </div>
      </form>
    </div>
  </div>