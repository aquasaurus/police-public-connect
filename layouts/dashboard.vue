<template>
  <div
    class="
      flex flex-col
      min-h-screen scroll-smooth
      font-montserrat
      text-lg
      tracking-wide
      text-gray-900
      bg-white
    "
  >
    <LayoutHeader :nav-list="Navigation" />
    <main class="flex-1 w-full mx-auto bg-white py-8"><slot /></main>
    <LayoutFab :nav="FabNav" />
    <footer></footer>
  </div>
</template>
    <style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
</style>

<script setup>
definePageMeta({
  middleware: ["auth"]
})

onMounted(() => {
  if(!localStorage.getItem("ppc_token")) {
    window.location.href="/login"
  }
})
const FabNav = [
  {
    name: "Home",
    action: "/#",
    key: "home",
    toolTip: "Go Home",
    routeIcon: "M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z",
  },
  {
    name: "Complaint",
    action: "/complain",
    key: "complaint",
    toolTip: "File Complaint",
    routeIcon:
      "M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7 M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z",
  },
  {
    name: "Login",
    action: "/login",
    key: "login",
    toolTip: "Volunteer Login",
    routeIcon: "M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z",
  },
];

const Navigation = [
  {
    name: `Dashboard`,
    route: `/dashboard`,
    key: `dashboard`,
  },
  {
    name: `All Complaints`,
    route: `/dashboard/complaints`,
    key: `complaints`,
  },
  {
    name: `My Complaints`,
    route: `/dashboard/mycomplaints`,
    key: `mycomplaints`,
  },

  {
    name: `Profile`,
    route: `/dashboard/me`,
    key: `profile`,
  },
  {
    name: `Logout`,
    route: `/dashboard/logout`,
    key: `logout`,
  },
];

</script>