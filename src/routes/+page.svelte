<script lang="ts">
  import { onMount } from 'svelte';

  type User = {
    id: number;
    name: string;
    email: string;
    phone: string;
  };

  let users: User[] = [];
  let error: string | null = null;
  let showModal = false;

  let form = {
    name: '',
    email: '',
    phone: ''
  };

  let sortBy: 'name' | 'email' | null = null;
  let sortAsc = true;
  let showEditModal = false;
  let editForm: User = { id: 0, name: '', email: '', phone: '' };

  async function fetchData() {
    try {
      const res = await fetch('https://jsonplaceholder.typicode.com/users');
      if (!res.ok) throw new Error('Failed to fetch');
      users = await res.json() as User[];
    } catch (err) {
      error = 'Failed to load users';
      console.error(err);
    }
  }

  function openEditModal(user: User) {
  editForm = { ...user };
  showEditModal = true;
}

function updateUser() {
  users = users.map(u => u.id === editForm.id ? { ...editForm } : u);
  showEditModal = false;
}

  function sort(field: 'name' | 'email') {
    if (sortBy === field) {
      sortAsc = !sortAsc;
    } else {
      sortBy = field;
      sortAsc = true;
    }

    users = [...users].sort((a, b) => {
      const valA = a[field].toLowerCase();
      const valB = b[field].toLowerCase();
      return sortAsc ? valA.localeCompare(valB) : valB.localeCompare(valA);
    });
  }

  function openModal() {
    form = { name: '', email: '', phone: '' };
    showModal = true;
  }

  function closeModal() {
    showModal = false;
  }

  function addUser() {
    const newUser: User = {
      id: Date.now(),
      ...form
    };
    users = [newUser, ...users];
    closeModal();
  }

  function editUser(id: number) {
  const user = users.find(u => u.id === id);
  if (user) openEditModal(user);
}


  function deleteUser(id: number) {
    users = users.filter(user => user.id !== id);
  }

  onMount(fetchData);
</script>

<!-- MAIN LAYOUT -->
<div class="p-6 max-w-6xl mx-auto">
  <div class="flex justify-between items-center mb-6">
    <h1 class="text-3xl font-bold">Users Listing</h1>
    <button on:click={openModal} class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700">
      Add User
    </button>
  </div>

  {#if error}
    <p class="text-red-500">{error}</p>
  {:else if users.length === 0}
    <p>Loading...</p>
  {:else}
    <div class="overflow-x-auto rounded border">
      <table class="min-w-full bg-white border-collapse">
        <thead>
          <tr class="bg-gray-100 text-left">
            <th class="p-3">
              <div class="flex items-center space-x-2">
                <span>Name</span>
                <button 
                  on:click={() => sort('name')} 
                  class="text-sm bg-gray-200 px-2 py-1 rounded hover:bg-gray-300"
                >
                  Sort {sortBy === 'name' ? (sortAsc ? '▲' : '▼') : ''}
                </button>
              </div>
            </th>
            <th class="p-3">
              <div class="flex items-center space-x-2">
                <span>Email</span>
                <button 
                  on:click={() => sort('email')} 
                  class="text-sm bg-gray-200 px-2 py-1 rounded hover:bg-gray-300"
                >
                  Sort {sortBy === 'email' ? (sortAsc ? '▲' : '▼') : ''}
                </button>
              </div>
            </th>
            <th class="p-3">Phone</th>
            <th class="p-3">Actions</th>
          </tr>
        </thead>
        <tbody>
          {#each users as user}
            <tr class="border-t hover:bg-gray-50">
              <td class="p-3">{user.name}</td>
              <td class="p-3 break-words max-w-xs">{user.email}</td>
              <td class="p-3">{user.phone}</td>
              <td class="p-3 flex space-x-2">
                <button on:click={() => editUser(user.id)} class="text-blue-600 hover:underline">Edit</button>
                <button on:click={() => deleteUser(user.id)} class="text-red-600 hover:underline">Delete</button>
              </td>
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  {/if}

  <!-- MODAL -->
  {#if showModal}
    <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
      <div class="bg-white p-6 rounded-lg w-full max-w-md shadow-lg">
        <h2 class="text-xl font-semibold mb-4">Add New User</h2>
        <div class="space-y-4">
          <input type="text" placeholder="Name" bind:value={form.name} class="w-full p-2 border rounded" />
          <input type="email" placeholder="Email" bind:value={form.email} class="w-full p-2 border rounded" />
          <input type="tel" placeholder="Phone" bind:value={form.phone} class="w-full p-2 border rounded" />
        </div>
        <div class="mt-6 flex justify-end space-x-3">
          <button on:click={closeModal} class="px-4 py-2 bg-gray-300 rounded hover:bg-gray-400">Cancel</button>
          <button on:click={addUser} class="px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700">Add</button>
        </div>
      </div>
    </div>
  {/if}
</div>

{#if showEditModal}
  <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-white p-6 rounded-lg w-full max-w-md shadow-lg">
      <h2 class="text-xl font-semibold mb-4">Edit User</h2>
      <div class="space-y-4">
        <input type="text" placeholder="Name" bind:value={editForm.name} class="w-full p-2 border rounded" />
        <input type="email" placeholder="Email" bind:value={editForm.email} class="w-full p-2 border rounded" />
        <input type="tel" placeholder="Phone" bind:value={editForm.phone} class="w-full p-2 border rounded" />
      </div>
      <div class="mt-6 flex justify-end space-x-3">
        <button on:click={() => showEditModal = false} class="px-4 py-2 bg-gray-300 rounded hover:bg-gray-400">Cancel</button>
        <button on:click={updateUser} class="px-4 py-2 bg-green-600 text-white rounded hover:bg-green-700">Update</button>
      </div>
    </div>
  </div>
{/if}

