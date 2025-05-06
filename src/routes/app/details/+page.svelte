<script lang="ts">
  import { onMount } from 'svelte';

  type User = {
    id: number;
    name: string;
    email: string;
    phone: string;
    website: string;
    username: string;
  };

  let users: User[] = [];
  let error: string | null = null;

  function getRandomLightColor(): string {
    const colors = [
      'bg-blue-100',
      'bg-green-100',
      'bg-yellow-100',
      'bg-purple-100',
      'bg-pink-100',
      'bg-indigo-100',
      'bg-teal-100',
      'bg-orange-100'
    ];
    return colors[Math.floor(Math.random() * colors.length)];
  }

  onMount(async () => {
    try {
      const res = await fetch('https://jsonplaceholder.typicode.com/users');
      if (!res.ok) throw new Error('Failed to fetch users');
      users = await res.json();
    } catch (err) {
      error = 'Failed to load user data';
      console.error(err);
    }
  });
</script>

<div class="p-6 bg-white min-h-screen">
  <h1 class="text-3xl font-bold text-center mb-8">User Details</h1>

  {#if error}
    <p class="text-red-600 text-center">{error}</p>
  {:else if users.length === 0}
    <p class="text-center">Loading...</p>
  {:else}
    <div class="grid gap-6 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
      {#each users as user}
        <div class={`${getRandomLightColor()} shadow-md rounded-lg p-4 border border-blue-200 hover:shadow-lg transition`}>
          <h2 class="text-xl font-semibold text-blue-700 mb-2">ID: {user.id}</h2>
          <p><strong>Name:</strong> {user.name}</p>
          <p><strong>Email:</strong> {user.email}</p>
          <p><strong>Phone:</strong> {user.phone}</p>
          <p><strong>Username:</strong> {user.username}</p>
          <p><strong>Website:</strong> <a href={'https://' + user.website} target="_blank" class="text-blue-500 underline">{user.website}</a></p>
        </div>
      {/each}
    </div>
  {/if}
</div>
