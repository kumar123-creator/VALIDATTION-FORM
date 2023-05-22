
<h1>DETAILS</h1>
<script>
  import { onMount } from 'svelte';

  let firstName = '';
  let surname = '';
  let email = '';
  let password = '';
  let mobile = '';

  let firstNameError = '';
  let surnameError = '';
  let emailError = '';
  let passwordError = '';
  let mobileError = '';

  function validateForm() {
    // Reset errors
    firstNameError = '';
    surnameError = '';
    emailError = '';
    passwordError = '';
    mobileError = '';

    let isValid = true;

    // Validate First Name
    if (!firstName) {
      firstNameError = 'First Name is required.';
      isValid = false;
    } else if (firstName.length > 28) {
      firstNameError = 'First Name must be less than 29 characters.';
      isValid = false;
    }

    // Validate Surname
    if (!surname) {
      surnameError = 'Surname is required.';
      isValid = false;
    } else if (surname.length > 28) {
      surnameError = 'Surname must be less than 29 characters.';
      isValid = false;
    }

    // Validate Email
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!email) {
      emailError = 'Email is required.';
      isValid = false;
    } else if (!emailRegex.test(email)) {
      emailError = 'Invalid email format.';
      isValid = false;
    }

    // Validate Password
    const passwordRegex = /^(?=.*[0-9a-zA-Z])(?=.*[!@#$%^&*])[0-9a-zA-Z!@#$%^&*]{6,15}$/;
    if (!password) {
      passwordError = 'Password is required.';
      isValid = false;
    } else if (!passwordRegex.test(password)) {
      passwordError = 'Password must contain at least one alphanumeric character and one special character. Password length should be between 6 and 15 characters.';
      isValid = false;
    }

    // Validate Mobile
    const mobileRegex = /^(\+)?\d+$/;
    if (!mobile) {
      mobileError = 'Mobile is required.';
      isValid = false;
    } else if (!mobileRegex.test(mobile)) {
      mobileError = 'Invalid mobile number.';
      isValid = false;
    }

    return isValid;
  }

  function handleSubmit(event) {
    event.preventDefault();

    if (validateForm()) {
      // Submit the form
      console.log('Form submitted successfully!');
    }
  }

  // Optional: Initialize form data or perform other actions on mount
  onMount(() => {
    // Initialize form data if needed
  });
</script>

<style>
  /* Add Bootstrap or Tailwind CSS classes for styling */
</style>

<form on:submit={handleSubmit}>
  <div>
    <label for="firstName">First Name:</label>
    <input type="text" id="firstName" bind:value={firstName} />
    {#if firstNameError}<p>{firstNameError}</p>{/if}
  </div>

  <div>
    <label for="surname">Surname:</label>
    <input type="text" id="surname" bind:value={surname} />
    {#if surnameError}<p>{surnameError}</p>{/if}
  </div>

  <div>
    <label for="email">Email:</label>
    <input type="email" id="email" bind:value={email} />
    {#if emailError}<p>{emailError}</p>{/if}
  </div>
  
    <div>
    <label for="password">password:</label>
    <input type="text" id="password" bind:value={password} />
      {#if passwordError}<p>{passwordError}</p>{/if}
  </div>

  <div>
    <label for="mobile">Mobile:</label>
    <input type="number" id="mobile" bind:value={mobile} />
    {#if mobileError}<p>{mobileError}</p>{/if}
   </div>
 
 <button type="submit" class="btn btn-primary">Submit</button>
  </form>
</div>

