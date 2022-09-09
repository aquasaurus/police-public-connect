<template>
  <div
    class="
      flex flex-col
      min-h-screen scroll-smooth
      font-[Poppins]
      text-lg
      tracking-wide
      break-words
      text-gray-900
      bg-white
    "
  >
    <LayoutHeader :nav-list="Navigation" />
    <main class="flex-1 w-full mx-auto bg-white"><slot /></main>
    <LayoutFab :nav="FabNav" />
    <LayoutFooter />
  </div>
</template>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
</style>

<script setup>
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
    name: `Home`,
    route: `/`,
    key: `home`,
  },
  {
    name: `About Us`,
    route: `/#about`,
    key: `about`,
  },

  {
    name: `Volunteers`,
    route: `/#volunteer`,
    key: `volunteer`,
  },

  {
    name: `Leaders`,
    route: `/#leaders`,
    key: `leaders`,
  },
  {
    name: `Events`,
    route: `/#events`,
    key: `events`,
  },
  {
    name: 'Contact us',
    route: '/#complain',
    key: 'contact us',
  },
  {
    name: `Complain`,
    route: `/complain`,
    key: `complain`,
  },
  {
    name: 'Register',
    route: '/apply',
    key: 'register',
  },
  {
    name: 'Login',
    route: '/login',
    key: 'login',
  },
];
</script>