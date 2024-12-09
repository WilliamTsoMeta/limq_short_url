<script lang="ts">
  export let email: string;
  export let password: string;
  export let loading: boolean;
  export let error: string | null;
  export let onSubmit: () => void;
  export let showRememberMe = true;
  export let rememberMe = false;
</script>

<form class="space-y-4" on:submit|preventDefault={onSubmit}>
  {#if error}
    <div class="text-sm text-red-600 bg-red-50 p-3 rounded-lg">
      {error}
    </div>
  {/if}

  <div class="space-y-2">
    <label for="email" class="block text-sm text-gray-700">Email</label>
    <input
      id="email"
      type="email"
      bind:value={email}
      required
      disabled={loading}
      class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
      placeholder="Enter your email"
    />
  </div>

  <div class="space-y-2">
    <label for="password" class="block text-sm text-gray-700">Password</label>
    <input
      id="password"
      type="password"
      bind:value={password}
      required
      disabled={loading}
      class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
      placeholder="••••••••"
    />
  </div>

  {#if showRememberMe}
    <div class="flex items-center justify-between">
      <label class="flex items-center">
        <input
          type="checkbox"
          bind:checked={rememberMe}
          class="w-4 h-4 text-blue-600 border-gray-300 rounded focus:ring-blue-500"
        />
        <span class="ml-2 text-sm text-gray-600">Remember for 30 days</span>
      </label>
      <a href="/forgot-password" class="text-sm text-blue-600 hover:text-blue-700">
        Forgot password
      </a>
    </div>
  {/if}

  <button
    type="submit"
    disabled={loading}
    class="w-full py-2 px-4 bg-blue-600 hover:bg-blue-700 text-white font-medium rounded-lg transition-colors disabled:opacity-50"
  >
    {loading ? 'Loading...' : 'Log in'}
  </button>

  <div class="relative my-6">
    <div class="absolute inset-0 flex items-center">
      <div class="w-full border-t border-gray-200"></div>
    </div>
    <div class="relative flex justify-center text-sm">
      <span class="px-2 bg-white text-gray-500">or</span>
    </div>
  </div>

  <button
    type="button"
    class="w-full flex items-center justify-center gap-3 py-2 px-4 bg-white border border-gray-300 rounded-lg hover:bg-gray-50 transition-colors"
  >
    <img src="/google.svg" alt="Google" class="w-5 h-5" />
    <span class="text-sm font-medium">Sign in with Google</span>
  </button>
</form>