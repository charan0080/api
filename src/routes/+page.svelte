<script lang="ts">
    type ApiResponse = {
      message: string;
    };
  
    let data: ApiResponse | null = null;
    let error: string | null = null;
  
    async function fetchData() {
      try {
        const res = await fetch('https://jsonplaceholder.typicode.com/users');//network request
        if (!res.ok) throw new Error('Failed to fetch');
        const json = await res.json() as ApiResponse;
        data = json;    
      } catch (error) {
          error = 'An unknown error occurred';
        }
      } 
    fetchData();
  </script>
  {#if data}
    <p>Data: {JSON.stringify(data)}</p>
  {:else if error}
    <p>Error: {error}</p>
  {:else}
    <p>Loading...</p>
  {/if}
  