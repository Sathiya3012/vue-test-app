<script setup lang="ts">
  import { Authenticator } from "@aws-amplify/ui-vue";

  import { Amplify } from 'aws-amplify';
  import awsconfig from './aws-exports';
  import { signInWithRedirect } from 'aws-amplify/auth';

  const provider = {
  custom: 'Microsoft'
}

function handleSignInClick() {
    signInWithRedirect({ provider })
}

  Amplify.configure(awsconfig);
</script>

<template>
  <authenticator>
    <template v-slot:sign-up-header>
      <h3
        class="amplify-heading"
        style="padding: var(--amplify-space-xl) 0 0 var(--amplify-space-xl)"
      >
        Create a new account
      </h3>
    </template>
    <template v-slot:header>
      <div style="padding: var(--amplify-space-large); text-align: center">
        <img
          class="amplify-image"
          alt="Amplify logo"
          src="https://docs.amplify.aws/assets/logo-dark.svg"
        />
      </div>
    </template>
    <template v-slot:sign-in-header>
      <h3
        class="amplify-heading"
        style="padding: var(--amplify-space-xl) 0 0 var(--amplify-space-xl)"
      >
        Sign in to your account
      </h3>
    </template>
    <template v-slot:sign-in-footer>
      <div style="text-align: center; padding-top: 1rem">
        <button @click="handleSignInClick" class="sso-button">
          Microsoft
        </button>
      </div>
    </template>
    <template v-slot="{ user, signOut }">
      {{ user }}
      <h1>Hello {{ user.username }}!</h1>
      <button @click="signOut" variation="primary">Sign Out</button>
    </template>
    <template v-slot:footer>
      <div style="padding: var(--amplify-space-large); text-align: center">
        <p class="amplify-text" style="color: var(--amplify-colors-neutral-80)">
          © All Rights Reserved
        </p>
      </div>
    </template>
  </authenticator>
</template>


<style scoped>
.sso-button {
  background-color: #2563eb;
  color: white;
  padding: 10px 16px;
  border: none;
  border-radius: 6px;
  font-weight: bold;
  cursor: pointer;
}
.sso-button:hover {
  background-color: #1e40af;
}
.signout-button {
  margin-top: 20px;
  padding: 10px 16px;
  background-color: #ef4444;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}
</style>