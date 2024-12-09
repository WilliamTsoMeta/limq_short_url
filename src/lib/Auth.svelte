<script lang="ts">
  import Logo from './components/Logo.svelte';
  import AuthTabs from './components/AuthTabs.svelte';
  import AuthForm from './components/AuthForm.svelte';
  import { signUp, signIn } from './services/auth';

  let activeTab: 'login' | 'signup' = 'login';
  let loading = false;
  let email = '';
  let password = '';
  let error: string | null = null;
  let rememberMe = false;

  async function handleSubmit() {
    if (!email || !password) {
      error = 'Please enter your email and password';
      return;
    }

    try {
      loading = true;
      error = null;

      if (activeTab === 'login') {
        const result = await signIn(email, password);
        if (result) {
          console.log('Login successful:', result);
        }
      } else {
        const result = await signUp(email, password);
        if (result) {
          alert('Please check your email to complete registration!');
        }
      }
    } catch (err) {
      if (err instanceof Error) {
        error = err.message;
      } else {
        error = activeTab === 'login' 
          ? 'Login failed. Please check your credentials.'
          : 'Registration failed. Please try again.';
      }
    } finally {
      loading = false;
    }
  }
</script>

<div class="min-h-screen flex items-center justify-center p-4 bg-gray-50">
  <div class="w-full max-w-md space-y-8 bg-white p-8 rounded-2xl shadow-lg">
    <Logo />
    
    <div class="text-center space-y-2">
      <h1 class="text-2xl font-semibold text-gray-900">
        Log in to your account
      </h1>
      <p class="text-gray-600">
        Welcome back! Please enter your details.
      </p>
    </div>

    <AuthTabs bind:activeTab />
    
    <AuthForm
      bind:email
      bind:password
      {loading}
      {error}
      onSubmit={handleSubmit}
      showRememberMe={activeTab === 'login'}
      bind:rememberMe
    />

    {#if activeTab === 'signup'}
      <p class="text-center text-sm text-gray-500">
        Already have an account?
        <button
          class="text-blue-600 hover:text-blue-700 font-medium"
          on:click={() => activeTab = 'login'}
        >
          Log in
        </button>
      </p>
    {:else}
      <p class="text-center text-sm text-gray-500">
        Don't have an account?
        <button
          class="text-blue-600 hover:text-blue-700 font-medium"
          on:click={() => activeTab = 'signup'}
        >
          Sign up
        </button>
      </p>
    {/if}
  </div>
</div>