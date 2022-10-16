<template>
    <div class="p-2 w-full">
        <div class="bg-black/20 w-full shadow-lg">
            <div
                :class="`flex flex-row items-center rounded-t-xl border-b-4 ${
                    complaintInfo.complaint_status === 1
                        ? `border-red-500`
                        : complaintInfo.complaint_status === 2
                        ? `border-amber-300`
                        : `border-zinc-900`
                } px-4 py-6 justify-between cursor-pointer`"
                @click="() => {complaintOpen = !complaintOpen}"
            >
                <span>#{{ complaintInfo.complaint_id }}</span>
                <span>{{
                    complaintInfo.complaint_created
                        .toLocaleString("en-GB", {timeZone: "Asia/Kolkata"})
                        .split("GMT")[0]
                }}</span
                ><button
                    :class="`stroke-2 stroke-white transition duration-500 ease-in-out transform ${
                        complaintOpen ? `rotate-180` : `rotate-0`
                    }`"
                   
                >
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        width="24"
                        height="24"
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        class="feather feather-chevron-down"
                    >
                        <polyline points="6 9 12 15 18 9"></polyline>
                    </svg>
                </button>
            </div>
            <div
                :class="`transition-all duration-500 ease-in-out overflow-y-hidden px-4 ${
                    complaintOpen ? `max-h-[70rem] py-4` : `max-h-0`
                } w-full`"
            >
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-start">
                    <div class="p-2 flex flex-col space-y-4">
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Person Name</span
                            >
                            <span class="text-base">{{
                                complaintInfo.complaint_name
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Contact Number</span
                            >
                            <span class="text-base">{{
                                complaintInfo.complaint_phone
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Status</span
                            >
                            <span class="text-base">{{
                                complaintInfo.complaint_status === 1
                                    ? "Open"
                                    : complaintInfo.complaint_status === 2
                                    ? "Attended"
                                    : complaintInfo.complaint_status === 3
                                    ? "Closed"
                                    : complaintInfo.complaint_status === 4
                                    ? "Flagged"
                                    : "Unknown"
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Details</span
                            >
                            <span class="text-base">{{
                                complaintInfo.complaint_content
                            }}</span>
                        </div>
                    </div>
                    <div class="p-2 flex flex-col items-center">
                        <a
                            :href="`/dashboard/complaint/${complaintInfo.complaint_id}`"
                            class="p-2 text-center bg-blue-400 text-white rounded-xl transition duration-500 ease-in-out transform hover:-translate-y-1"
                        >
                            View Timeline</a
                        >
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
    const complaintOpen = ref(false);
    interface Complaint {
        complaint_id: string;
        complaint_name: string;
        complaint_phone: string;
        complaint_email?: string;
        complaint_content: string;
        complaint_status: ComplaintStatus;
        complaint_attendee?: Volunteer;
        complaint_created: Date;
        complaint_comments: ComplaintComments[];
    }
    const pleaseLog = console.log
    enum ComplaintStatus {
        OPEN = 1,
        ATTENDED = 2,
        CLOSED = 3,
    }

    interface ComplaintComments {
        comment_id: string;
        comment_user: Volunteer;
        comment_content: string;
        comment_created: Date;
    }

    interface Volunteer {
        user_name: string;
        user_id: string;
    }

    const { complaintInfo } = defineProps({ complaintInfo: Object });
</script>
