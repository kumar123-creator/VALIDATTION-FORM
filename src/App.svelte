
<h1>DETAILS</h1>
<script>
  import { onMount } from "svelte";

  let formData = {
    firstname: "",
    surname:"",
    email: "",
    password: "",
    mobile:""
  };

  let errors = {};

  const validateForm = () => {
    errors = {};

    if (!formData.firstname) {
      errors.firstname = "FirstName is required";
    }
    if (!formData.surname) {
      errors.surname = "SurName is required";
    }

    if (!formData.email) {
      errors.email = "Email is required";
    } else if (!isValidEmail(formData.email)) {
      errors.email = "Invalid email format";
    }

    if (!formData.password) {
      errors.password = "Password is required";
    } else if (formData.password.length < 6) {
      errors.password = "Password must be at least 6 characters long";
    }
     if (!formData.mobile) {
      errors.mobile = "Mobile is required";
    }
  };

  const isValidEmail = (email) => {
    // Regular expression to validate email format
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
  };

  const handleSubmit = () => {
    validateForm();

    if (Object.keys(errors).length === 0) {
      // Form submission logic goes here
      console.log("Form submitted successfully");
    }
  };

  onMount(() => {
    // Validate the form on initial load
    validateForm();
  });
</script>

<style>
  .error {
    color: red;
  }
</style>

<div class="container mt-5">
  <form on:submit|preventDefault={handleSubmit}>
    <div class="form-group">
      <label for="firstname">FirstName</label>
      <input
        type="text"
        class="form-control"
        id="firstname"
        bind:value={formData.firstname}
      />
      {#if errors.firstname}
        <p class="error">{errors.firstname}</p>
      {/if}
      </form>
    </div>
    
 <div class="container mt-5">
  <form on:submit|preventDefault={handleSubmit}>
    <div class="form-group">
      <label for="surname">SurName</label>
      <input
        type="text"
        class="form-control"
        id="surname"
        bind:value={formData.surname}
      />
      {#if errors.surname}
        <p class="error">{errors.surname}</p>
      {/if}
      </form>
    </div>

    <div class="form-group">
      <label for="email">Email</label>
      <input
        type="email"
        class="form-control"
        id="email"
        bind:value={formData.email}
      />
      {#if errors.email}
        <p class="error">{errors.email}</p>
      {/if}
    </div>

    <div class="form-group">
      <label for="password">Password</label>
      <input
        type="password"
        class="form-control"
        id="password"
        bind:value={formData.password}
      />
      {#if errors.password}
        <p class="error">{errors.password}</p>
      {/if}
    </div>
    
     <div class="form-group">
      <label for="mobile">Mobile:</label>
      <input type="text" id="mobile" class="form-control" bind:value={mobile} />
      {#if errors.mobile}
        <p class="error">{errors.mobile}</p>
      {/if}
    </div>


    <button type="submit" class="btn btn-primary">Submit</button>
  </form>
</div>

