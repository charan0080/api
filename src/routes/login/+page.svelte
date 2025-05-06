<script>
    // @ts-nocheck
    
      import { goto } from '$app/navigation';
      let email = '';
      let password = '';
      let userlist = ['abc@gmail.com'];
      let passwordlist = ['123abc'];
      let errorMessage = '';
    
      function signup() {
        goto("/signup");
      }
    
      function login() {
        const index = userlist.indexOf(email);
        if (index !== -1 && passwordlist[index] === password) {
          goto('/app/dashboard'); // Replace with your actual route
        } else {
          errorMessage = 'Invalid email or password';
          setTimeout(() => {
            errorMessage = ''; // Clear error message after a short delay
          }, 3000);
        }
      }
    </script>
    
    <div class="min-h-screen flex items-center justify-center bg-white">
      <div class="w-full max-w-md bg-white p-8 rounded-xl shadow-lg space-y-6">
        <div>
          <h2 class="text-3xl font-bold text-gray-800 text-center mb-4">Login</h2>
          <p class="text-gray-600 text-center">Welcome back! Please enter your details.</p>
        </div>
        <form on:submit|preventDefault={login} class="space-y-4">
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
    
          {#if errorMessage}
            <div class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative" role="alert">
              <strong class="font-bold">Error!</strong>
              <span class="block sm:inline">{errorMessage}</span>
            </div>
          {/if}
    
          <button
            type="submit"
            class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 px-4 rounded-lg focus:outline-none focus:shadow-outline transition duration-200"
          >
            Log In
          </button>
          
          <div> <button
            type="submit"
            on:click={signup}
            class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 px-4 rounded-lg focus:outline-none focus:shadow-outline transition duration-200"
          >sign up </div>
        </form>
      </div>
    </div>