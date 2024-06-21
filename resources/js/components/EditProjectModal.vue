<template>
    <!-- Edit Form -->
    <div
        class="fixed z-10 inset-0 overflow-y-auto"
        v-show="showModal"
        @click.self="$emit('close-modal')"
    >
        <div
            class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0"
        >
            <!-- Background overlay -->
            <div class="fixed inset-0 transition-opacity" aria-hidden="true">
                <div class="absolute inset-0 bg-gray-500 opacity-75"></div>
            </div>
            <!-- Dialog -->
            <span
                class="hidden sm:inline-block sm:align-middle sm:h-screen"
                aria-hidden="true"
                >&#8203;</span
            >
            <div
                class="inline-block align-bottom bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full"
                role="dialog"
                aria-modal="true"
                aria-labelledby="modal-headline"
            >
                <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
                    <div class="sm:flex sm:items-start">
                        <div
                            class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left"
                        >
                            <h3
                                class="text-lg leading-6 font-medium text-gray-900"
                                id="modal-headline"
                            >
                                Edit Project
                            </h3>
                            <!-- Edit Form -->
                            <form @submit.prevent="handleSubmit">
                                <div class="mt-2">
                                    <label for="editName" class="block mb-1"
                                        >Name:</label
                                    >
                                    <input
                                        id="editName"
                                        type="text"
                                        v-model="project.name"
                                        class="border border-gray-300 rounded px-2 py-1 w-full"
                                    />
                                </div>
                                <div class="mt-2">
                                    <label
                                        for="editDescription"
                                        class="block mb-1"
                                        >Description:</label
                                    >
                                    <input
                                        id="editDescription"
                                        type="text"
                                        v-model="project.description"
                                        class="border border-gray-300 rounded px-2 py-1 w-full"
                                    />
                                </div>
                                <div class="mt-2">
                                    <button
                                        type="submit"
                                        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
                                    >
                                        Update
                                    </button>
                                    <button
                                        @click="cancelEdit"
                                        class="ml-2 bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded"
                                    >
                                        Cancel
                                    </button>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        showModal: {
            type: Boolean,
            required: true,
        },
        project: {
            type: Object,
            required: true,
        },
    },
    methods: {
        handleSubmit() {
            this.$emit("update-project", this.project);
            this.$emit("close-modal");
        },
        cancelEdit() {
            this.$emit("close-modal");
        },
    },
    emits: ["close-modal", "update-project"],
};
</script>

<style scoped></style>
