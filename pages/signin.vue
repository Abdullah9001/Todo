<template>
  <div>
    <button @click="signInWithGoogle">Signin With Google</button>
  </div>
</template>

<script setup>
import { signInWithPopup, GoogleAuthProvider, getAuth } from "firebase/auth";
const signInWithGoogle = async () => {
  const auth = getAuth();
  const provider = new GoogleAuthProvider();
  try {
    const result = await signInWithPopup(auth, provider);

    console.log("User signed in:", user);
    navigateTo("/");
  } catch (error) {
    console.error("Error signing in with Google:", error);
  }
};
</script>
