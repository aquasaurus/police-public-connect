<template>
    <div
        class="flex flex-col min-h-screen scroll-smooth font-[Poppins] text-lg tracking-wide text-white dashbg"
    >
        <LayoutDashHeader :nav-list="Navigation" />
        <main
            class="flex-1 w-full mx-auto py-8"
        >
            <slot />
        </main>
        <LayoutFab :nav="FabNav" />
        <footer></footer>
    </div>
</template>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

    .dashbg {
        background-color: #121123;
        background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100%25' height='100%25' viewBox='0 0 1600 800'%3E%3Cg %3E%3Cpolygon fill='%23151426' points='1600 160 0 460 0 350 1600 50'/%3E%3Cpolygon fill='%23171629' points='1600 260 0 560 0 450 1600 150'/%3E%3Cpolygon fill='%231a192d' points='1600 360 0 660 0 550 1600 250'/%3E%3Cpolygon fill='%231c1b30' points='1600 460 0 760 0 650 1600 350'/%3E%3Cpolygon fill='%231F1E33' points='1600 800 0 800 0 750 1600 450'/%3E%3C/g%3E%3C/svg%3E");
        background-attachment: fixed;
        background-size: cover;
        /* background by SVGBackgrounds.com */
    }
</style>

<script setup>
    definePageMeta({
        middleware: ["auth"],
    });

    onMounted(() => {
        if (!localStorage.getItem("ppc_token")) {
            window.location.href = "/login";
        }
    });
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
