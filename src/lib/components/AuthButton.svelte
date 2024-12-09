<script lang="ts">
  export let onClick: () => void
  export let loading: boolean
  export let type: 'login' | 'signup'
  
  const colors = {
    login: 'bg-indigo-600 hover:bg-indigo-700 focus:ring-indigo-500',
    signup: 'bg-green-600 hover:bg-green-700 focus:ring-green-500'
  }
  
  const text = {
    login: { idle: '登录', loading: '登录中...' },
    signup: { idle: '注册', loading: '注册中...' }
  }
</script>

<button
  type="button"
  on:click={onClick}
  disabled={loading}
  class="group relative w-[48%] flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white {colors[type]} focus:outline-none focus:ring-2 focus:ring-offset-2"
>
  {loading ? text[type].loading : text[type].idle}
</button>