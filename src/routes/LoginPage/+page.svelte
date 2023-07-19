<script lang="ts">
    import supabase from '$lib/supabase';
    import { goto } from '$app/navigation'
    import { onMount } from 'svelte';
    import type { AuthChangeEvent, Session, User } from '@supabase/supabase-js';

    async function Goto(e: Event) {
        window.location.href = '/SignupPage';
    };
  
    let email = '';
    let password = '';

    // Function to handle form submission
    const handleLogin = async () => {
      try {
        const { data, error } = await supabase.auth.signInWithPassword({
          email: email,
          password: password
        });

  
        if (error) {
          // Handle registration error
          console.error('Error during login:', error);
          return;
        } else {
          window.location.href = '/BlogPageAuth';
        }

      } catch (error) {
        console.error('Unhandled error during login:', error);
      }
    };
  </script>

<body>
  <main>
    <h1>LOG IN</h1>
    <form on:submit|preventDefault={handleLogin} class="form1">
            <div class="items">
                <input type="email" id="email" placeholder="Email" bind:value={email} />
            </div>
            <div class="items">
                <input type="password" id="password" placeholder="Password" bind:value={password} />
            </div>
            <div class="items">
                <button type="submit" id="login">Log in</button>
            </div>      
            <div class="itemsLast">
                <p id="account">Don’t have an account yet?</p>
                <form on:submit|preventDefault={Goto}>
                    <button id="goto">Sign up</button>
                </form>
            </div>
    </form>
  </main>
</body>

<style>
  @import'./LoginPage.css';
</style>