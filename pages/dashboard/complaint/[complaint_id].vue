<template>
    <div class="p-4">
        <div
            class="border-b-2 border-blue-400 text-2xl px-2 font-bold uppercase"
        >
            Complaint #{{ complaint_id }}
        </div>
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
                    <span class="font-semibold text-lg uppercase">Status</span>
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
                    <span class="font-semibold text-lg uppercase">Details</span>
                    <span class="text-base">{{
                        complaintInfo.complaint_content
                    }}</span>
                </div>
            </div>
            <div class="p-2 flex flex-col items-center max-w-2xl">
                <div class="bg-gray-700 text-white w-full">
                    <div class="border-b-2 border-blue-400">
                        <span class="p-2 font-bold uppercase text-lg"
                            >Comments Timeline</span
                        >
                    </div>
                    <div
                        class="flex flex-col space-y-4 max-h-[20rem] overflow-y-auto p-2"
                    >
                        <div
                            v-for="comment in complaintInfo.complaint_comments
                                .sort(
                                    (a, b) =>
                                        a.comment_created.getTime() -
                                        b.comment_created.getTime()
                                )
                                .reverse()"
                            :key="comment.comment_id"
                            class=""
                        >
                            <div
                                :title="String(comment.comment_user.user_id)"
                                class="p-1 flex flex-row items-center space-x-4"
                            >
                                <span
                                    class="font-semibold text-base uppercase"
                                    >{{ comment.comment_user.user_name }}</span
                                ><span class="text-gray-400 text-sm">{{
                                    comment.comment_created
                                        .toISOString()
                                        .split("T")
                                        .join(" at ")
                                }}</span>
                            </div>
                            <div class="p-2 break-words text-sm">
                                {{ comment.comment_content }}
                            </div>
                        </div>
                        <div class = "p-2">
                            <input type = "text" class = "p-2 text-sm bg-gray-600 border border-blue-400" v-model="enteringComment" placeholder="Add comment" />
                        </div>
                       <div class = "p-2">
                            <button class = "bg-blue-400 p-2 text-sm" @click="addComment">Add Comment</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
const enteringComment = ref("")
    const route = useRoute();

    const complaint_id = route.params.complaint_id as string;

    const complaintInfo = {
        complaint_id: 1,
        complaint_name: "Raju",
        complaint_phone: "6767676767",
        complaint_content: "Missing Money",
        complaint_status: 2,
        complaint_attendee: "V450",
        complaint_created: new Date("2022-04-19"),
        complaint_comments: [
            {
                comment_content: "Help asap",
                comment_created: new Date("2022-04-19"),
                comment_user: {
                    user_id: 8,
                    user_name: "Raja",
                },
                comment_id: 1,
            },
        ],
    };

    function addComment() {

    }
</script>
