<script lang="ts">
  export let activeTab: 'login' | 'signup';
</script>

<div class="flex mb-8 bg-gray-50 rounded-lg p-1">
  <button
    class="flex-1 py-2 px-4 text-sm font-medium rounded-md transition-colors {activeTab === 'login' ? 'bg-white shadow-sm' : 'text-gray-500 hover:text-gray-700'}"
    on:click={() => activeTab = 'login'}
  >
    Log in
  </button>
  <button
    class="flex-1 py-2 px-4 text-sm font-medium rounded-md transition-colors {activeTab === 'signup' ? 'bg-white shadow-sm' : 'text-gray-500 hover:text-gray-700'}"
    on:click={() => activeTab = 'signup'}
  >
    Sign up
  </button>
</div>