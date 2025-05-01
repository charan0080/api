<script lang="ts">
  type User = {
    id: number;
    name: string;
    email: string;
    phone: string;
  };

  let users: User[] = [];
  let error: string | null = null;
  let sortBy: 'name' | 'email' | null = null;
  let sortAsc: boolean = true;

  async function fetchData() {
    try {
      const res = await fetch('https://jsonplaceholder.typicode.com/users');
      if (!res.ok) throw new Error('Failed to fetch');
      const json = await res.json() as User[];
      users = json;
    } catch (err) {
      error = 'Failed to load users';
      console.error(err);
    }
  }

  function sort(field: 'name' | 'email') {
    sortBy = field;
    sortAsc = sortBy === field ? !sortAsc : true;
    users = [...users].sort((a, b) =>
      sortAsc
        ? a[field].localeCompare(b[field])
        : b[field].localeCompare(a[field])
    );
  }

  function addUser() {
    // Placeholder logic – in production use a modal or form
    const newUser: User = {
      id: Date.now(),
      name: 'New User',
      email: 'newuser@example.com',
      phone: '123-456-7890'
    };
    users = [newUser, ...users];
  }

  function editUser(id: number) {
    alert(`Edit user with ID: ${id}`);
  }

  function deleteUser(id: number) {
    users = users.filter(user => user.id !== id);
  }

  fetchData();
</script>

<style>
  /* Optional: you can use Tailwind for all styling */
</style>

<div class="p-6 max-w-5xl mx-auto">
  <div class="flex justify-between items-center mb-4">
    <h1 class="text-2xl font-bold">Users Listing</h1>
    <button on:click={addUser} class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700">
      Add User
    </button>
  </div>

  {#if error}
    <p class="text-red-500">{error}</p>
  {:else if users.length === 0}
    <p>Loading...</p>
  {:else}
    <div class="grid grid-cols-5 gap-4 font-semibold border-b pb-2">
      <button on:click={() => sort('name')} class="text-left col-span-1">Name</button>
      <button on:click={() => sort('email')} class="text-left col-span-1">Email</button>
      <div class="col-span-1">Phone</div>
      <div class="col-span-1">Edit</div>
      <div class="col-span-1">Delete</div>
    </div>

    {#each users as user}
      <div class="grid grid-cols-5 gap-4 border-b py-2">
        <div class="col-span-1">{user.name}</div>
        <div class="col-span-1">{user.email}</div>
        <div class="col-span-1">{user.phone}</div>
        <button on:click={() => editUser(user.id)} class="text-blue-600 hover:underline col-span-1">Edit</button>
        <button on:click={() => deleteUser(user.id)} class="text-red-600 hover:underline col-span-1">Delete</button>
      </div>
    {/each}
  {/if}
</div>
