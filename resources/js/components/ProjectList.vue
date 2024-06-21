<template>
    <h2 class="text-2xl font-bold mb-4">Projects</h2>
    <table class="min-w-full divide-y divide-gray-200">
        <thead>
            <tr>
                <th class="px-6 py-3 bg-gray-50">Id</th>
                <th class="px-6 py-3 bg-gray-50">Name</th>
                <th class="px-6 py-3 bg-gray-50">Description</th>
                <th class="px-6 py-3 bg-gray-50">Actions</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="project in projects" :key="project.id">
                <td class="px-6 py-4 whitespace-nowrap">
                    {{ project.id }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                    {{ project.name }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                    {{ project.description }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                    <button
                        @click="showEditModal(project)"
                        class="ml-2 px-2 py-1 bg-blue-500 text-white rounded"
                    >
                        Edit
                    </button>
                    <button
                        @click="confirmDelete(project.id)"
                        class="ml-2 px-2 py-1 bg-red-500 text-white rounded"
                    >
                        Delete
                    </button>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script>
export default {
    props: {
        projects: {
            type: Array,
            required: true,
        },
    },
    emits: ["edit-project", "delete-project"],
    methods: {
        showEditModal(project) {
            this.$emit("edit-project", project); // Emit the edit-project event
        },
        confirmDelete(id) {
            this.$emit("delete-project", id); // Emit the delete-project event
        },
    },
};
</script>

<style scoped></style>
