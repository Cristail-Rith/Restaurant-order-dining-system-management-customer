<script setup lang="ts">
    const userData = ref<{
        username :string,
        password : string
    }>({
        username : '',
        password : ""
    })

async function handleLogin(e:Event) {
    e.preventDefault()
    const res = await fetch ("http://localhost:8000/api/v1/accounts/login/",{
     method : "POST",
     headers : {
        "Content-type": "application/json"
     },
     body : JSON.stringify(userData.value)   
    })
    const result = await res.json()
    localStorage.setItem("access", result.access)
}


</script>


<template>
    <form class="max-w-sm mx-auto mt-20">
  <div class="mb-5">
    <label for="username" class="block mb-2.5 text-sm font-medium text-heading">username</label>
    <input v-model="userData.username" type="text" id="username" class="bg-neutral-secondary-medium border border-default-medium text-heading text-sm rounded-base focus:ring-brand focus:border-brand block w-full px-3 py-2.5 shadow-xs placeholder:text-body" placeholder="Enter your username" required />
  </div>
  <div class="mb-5">
    <label for="password" class="block mb-2.5 text-sm font-medium text-heading">Your password</label>
    <input v-model="userData.password" type="password" id="password" class="bg-neutral-secondary-medium border border-default-medium text-heading text-sm rounded-base focus:ring-brand focus:border-brand block w-full px-3 py-2.5 shadow-xs placeholder:text-body" placeholder="••••••••" required />
  </div>
  <button @click="handleLogin" type="submit" class="text-white bg-brand box-border border border-transparent hover:bg-brand-strong focus:ring-4 focus:ring-brand-medium shadow-xs font-medium leading-5 rounded-base text-sm px-4 py-2.5 focus:outline-none">Login</button>
</form>




</template>