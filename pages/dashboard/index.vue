<template>
    <div class="max-w-6xl mx-auto flex flex-col space-y-4">
        <CardComplaint v-for = "complaint in complaints.sort((a, b) => b.complaint_created.getTime() - a.complaint_created.getTime())" :key = "`complaint_${complaint.complaint_id}`" :complaint-info="complaint" />
    </div>
</template>
<script setup>
    definePageMeta({
        layout: "dashboard",
    });

    const complaints = [
        {
            complaint_id: 1,
            complaint_name: "Raju",
            complaint_phone: "6767676767",
            complaint_content: "Missing Money",
            complaint_status: 2,
            complaint_attendee: "V450",
            complaint_created: new Date("2022-04-19"),
            //      complaint_comments: "Help asap",
        },
        {
            complaint_id: 2,
            complaint_name: "Ramasamy",
            complaint_phone: "8834567062",
            complaint_content: "Damaged and Worn Off Roads",
            complaint_status: 3,
            complaint_attendee: "V784",
            complaint_created: new Date("2022-11-14"),
            complaint_comments:
                "Transportations is highly difficult and prone to accidents.",
        },
    ];
</script>
