<script lang="ts">
    import supabase from '$lib/supabase';
    import type { AuthChangeEvent, Session, User } from '@supabase/supabase-js';

    import { onMount } from 'svelte';
    // import { user } from '$lib/Store';
    import photoIcon from '$lib/images/photoIcon.png';


    async function Goto(e: Event) {
        window.location.href = '/LoginPage';
    };
  
    let photo_url = '';
    let email = '';
    let password = '';
    let name = '';
    let surname = '';
  
    // Function to handle form submission
    const handleRegister = async () => {
      try {
        const { data: userInfo, error } = await supabase.auth.signUp({
          email,
          password,
        });

        if (error) {
          // Handle registration error
          console.error('Error during registration:', error);
          return;
        }
  
        // If registration is successful, it saves the additional user details in the database.
        if (userInfo && userInfo.user) {
          const { error: profileError } = await supabase
            .from('users')
            .insert([{ email, password, name, surname, photo_url }]);
  
          if (profileError) {
            // Handle profile data insertion error
            console.error('Error saving user profile:', profileError);
          } else {
            console.log('User registered successfully:', userInfo.user);
            // Redirect to the BlogPage upon successful registration
            // $user = userInfo.session?.user.email;
            window.location.href = '/BlogPageAuth';
          }
        }
      } catch (error) {
        console.error('Unhandled error during registration:', error);
      }
    };
    onMount(() => {
        const realFileBtn = document.getElementById("real-file") as HTMLInputElement;
        const customBtn = document.getElementById("custom-button") as HTMLButtonElement;
        const customTxt = document.getElementById("custom-text") as HTMLSpanElement;

        customBtn.addEventListener("click", function() {
            realFileBtn.click();
        });

        realFileBtn.addEventListener("change", function() {
            if (realFileBtn.value) {
                customTxt.innerHTML = realFileBtn.value;
                photo_url = realFileBtn.value;
            } else {
                customTxt.innerHTML = "No photo chose, yet."
            }
        });

    });
  </script>
  
  
  
  
  
<main>
  <h1>SIGN UP</h1>
  <form on:submit|preventDefault={handleRegister} class="form1">
          <div class="items1">
              <input type="file" id="real-file" hidden/>  
              <!-- bind:this={photo_url}  -->
              <button type="button" id="custom-button">
                <img src={photoIcon} alt="Icon of camera" id="photoIcon">
                <p id="photoTxt">Add photo</p>
              </button>
              <!-- <span id="custom-text">No photo chose, yet.</span> -->
              <div class="Nickname">
                  <input type="text" id="name" placeholder="Name" bind:value={name} />
                  <input type="text" id="surname" placeholder="Surname" bind:value={surname} />
              </div>
          </div>
          <div class="items">
              <input type="email" id="email" placeholder="Email" bind:value={email} />
          </div>
          <div class="items">
              <input type="password" id="password" placeholder="Password" bind:value={password} />
          </div>
          <div class="items">
              <button type="submit" id="signup">Sign up</button>
          </div>      
          <div class="itemsLast">
              <p id="account">Already have an account?</p>
              <form on:submit|preventDefault={Goto}>
                  <button id="goto">Log in</button>
              </form>
          </div>
  </form>
</main>

<style>
  @import './SignupPage.css';
</style>  
