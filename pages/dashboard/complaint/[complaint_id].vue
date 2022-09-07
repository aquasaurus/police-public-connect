<template>
    <div class="p-4 max-w-9xl mx-auto py-8">
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
                    <span v-if = "complaintInfo.complaint_status !== 2" class="text-base">{{
                        complaintInfo.complaint_status === 1
                            ? "Open"
                            : complaintInfo.complaint_status === 3
                            ? "Closed"
                            : complaintInfo.complaint_status === 4
                            ? "Flagged"
                            : "Unknown"
                    }}</span>
                    <span v-else>
                            Attended by <a class = "text-blue-500" :href = "`/dashboard/volunteers/info/${complaintInfo.complaint_attendee}`">#{{complaintInfo.complaint_attendee}}</a>
                    </span>
                </div>
                <div class="flex flex-col space-y-1 break-words">
                    <span class="font-semibold text-lg uppercase">Details</span>
                    <span class="text-base">{{
                        complaintInfo.complaint_content
                    }}</span>
                </div>
                <button v-if = "complaintInfo.complaint_status === 1"
                    class="p-2 text-center bg-blue-400 text-white rounded-xl transition duration-500 ease-in-out transform hover:-translate-y-1"
                    @click="attend"
                >
                    Attend Complaint
                </button>
            </div>
            <div class="p-2 flex flex-col items-center max-w-2xl">
                <div class="bg-black/20 text-white w-full">
                    <div class="border-b-2 border-blue-400">
                        <span class="p-2 font-bold uppercase text-lg"
                            >Comments Timeline</span
                        >
                    </div>
                    <div
                        class="flex flex-col space-y-4 max-h-[20rem] overflow-y-auto p-2"
                    >
                        <div
                            v-for="comment in complaintInfo.complaint_comments.sort(
                                (a, b) =>
                                    a.comment_created.getTime() -
                                    b.comment_created.getTime()
                            )"
                            :key="comment.comment_id"
                            class=""
                        >
                            <div
                                :title="String(comment.comment_user?.user_id)"
                                class="p-1 flex flex-row items-center space-x-4"
                            >
                                <span
                                    class="font-semibold text-base uppercase"
                                    >{{ comment.comment_user?.user_name }}</span
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
                        <div class="p-2">
                            <input
                                type="text"
                                class="p-2 text-sm bg-gray-600 border border-blue-400"
                                v-model="enteringComment"
                                placeholder="Add comment"
                            />
                        </div>
                        <div class="p-2">
                            <button
                                class="bg-blue-400 p-2 text-sm"
                                @click="addComment"
                            >
                                Add Comment
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
    definePageMeta({
        layout: "dashboard",
    });

    const enteringComment = ref("");
    const complaintInfo = ref({
        complaint_id: 1,
        complaint_name: "Fetching",
        complaint_phone: "Fetching",
        complaint_content: "Fetching",
        complaint_status: 3,
        complaint_attendee: 1,
        complaint_created: new Date("1999-12-31"),
        complaint_comments: [],
    });
    const route = useRoute();

    const complaint_id = route.params.complaint_id as string;

    const res = await fetch(
        `https://api.policepublic.in/complaints/get/${complaint_id}`,
        { headers: { Authorization: localStorage.getItem("ppc_token") } }
    );
    if (res.status == 200) {
        const cInfo = await res.json();
        complaintInfo.value = cInfo;
        complaintInfo.value.complaint_created = new Date(
            complaintInfo.value.complaint_created
        );
        complaintInfo.value.complaint_comments =
            complaintInfo.value.complaint_comments.map((x) => ({
                comment_user: x.comment_user,
                comment_created: new Date(x.comment_created),
                comment_content: x.comment_content,
            }));
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

    async function addComment() {
        const commentVal = enteringComment.value;
        if (!commentVal) return;
        const res = await fetch(
            `https://api.policepublic.in/complaints/comments/${complaint_id}`,
            {
                method: "POST",
                body: JSON.stringify({ comment: commentVal }),
                headers: { Authorization: localStorage.getItem("ppc_token") },
            }
        );
        if (res.status == 200) {
            history.go(0);
        }
    }
    async function attend() {
        const res = await fetch(
            `https://api.policepublic.in/complaints/${complaint_id}/attend`,
            {
                method: "POST",
                headers: { Authorization: localStorage.getItem("ppc_token") },
            }
        );
        if (res.status == 200) {
            history.go(0);
        }
    }
    
</script>
