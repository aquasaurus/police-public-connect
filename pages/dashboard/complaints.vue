<template>
    <div class="max-w-6xl mx-auto flex flex-col space-y-4">
        <div class = "text-2xl uppercase font-bold">All Complaints</div>
        <CardComplaint
            v-for="complaint in complaintInfo.sort(
                (a, b) =>
                    b.complaint_created.getTime() -
                    a.complaint_created.getTime()
            )"
            :key="`complaint_${complaint.complaint_id}`"
            :complaint-info="complaint"
        />
    </div>
</template>
<script setup>
    definePageMeta({
        layout: "dashboard",
    });

    const complaintInfo = ref([]);
    const res = await fetch(`https://api.policepublic.in/complaints/all`, {
        headers: { Authorization: localStorage.getItem("ppc_token") },
    });
    if (res.status == 200) {
        const cInfo = await res.json();
        console.log(cInfo);
        complaintInfo.value = cInfo.map((x) => {
            x.complaint_created = new Date(x.complaint_created);
            return x;
        });
    } else if (res.status == 404) {
        complaintInfo.value = {
            complaint_id: 1,
            complaint_name: "Not Found",
            complaint_phone: "Not Found",
            complaint_content: "Not Found",
            complaint_status: 3,
            complaint_attendee: 1,
            complaint_created: new Date("1999-12-31"),
            complaint_comments: [],
        };
    }
</script>
