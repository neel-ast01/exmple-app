<template>
    <h2 class="text-2xl font-bold mb-4">Create Project</h2>
    <form @submit.prevent="handleSubmit" class="flex flex-col md:flex-row">
        <div class="flex-row">
            <label for="name" class="block mb-1">Name:</label>
            <input
                id="name"
                type="text"
                v-model="name"
                class="border border-gray-300 rounded px-2 py-1"
            />
        </div>
        <div class="flex-row ml-3">
            <label for="description" class="block mb-1">Description:</label>
            <textarea
                id="description"
                v-model="description"
                class="border border-gray-300 rounded px-2 py-1"
            ></textarea>
        </div>
        <button
            type="submit"
            class="ml-3 mb-5 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded self-end"
        >
            Create
        </button>
    </form>
</template>

<script>
export default {
    emits: ["submit"],
    props: {
        project: {
            type: Object,
            required: false,
            default: null,
        },
    },
    data() {
        return {
            name: "",
            description: "",
        };
    },
    created() {
        if (this.project) {
            this.name = this.project.name;
            this.description = this.project.description;
        }
    },
    methods: {
        handleSubmit() {
            const projectData = {
                name: this.name,
                description: this.description,
            };
            this.$emit("submit", projectData);
            this.resetForm();
        },
        resetForm() {
            this.name = "";
            this.description = "";
        },
    },
};
</script>

<style scoped></style>
