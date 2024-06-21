<template>
    <div class="ml-3">
        <project-form @submit="createProject" />

        <h3 class="text-red-600">{{ error }}</h3>

        <project-list
            :projects="projects"
            @edit-project="showEditModal"
            @delete-project="confirmDelete"
        />
        <edit-project-modal
            v-if="editModalVisible"
            :show-modal="editModalVisible"
            :project="editProject"
            @close-modal="closeEditModal"
            @update-project="updateProject"
        />
    </div>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";
import ProjectForm from "./components/ProjectForm.vue";
import ProjectList from "./components/ProjectList.vue";
import EditProjectModal from './components/EditProjectModal.vue';

export default {
    components: {
        ProjectForm,
        ProjectList,
        EditProjectModal,
    },
    data() {
        return {
            error: null,
            projects: [],
            editProject: null,
            editModalVisible: false,
        };
    },

    created() {
        this.fetchProjects();
    },

    methods: {
        async fetchProjects() {
            await axios
                .get("http://127.0.0.1:8000/api/projects/")
                .then((response) => {
                    this.projects = response.data;
                })
                .catch((error) => {
                    console.error(error);
                });
        },
        async createProject(projectData) {
            await axios
                .post("http://127.0.0.1:8000/api/projects/", projectData)
                .then((response) => {
                    console.log(response);
                    // Clear the form after successful submission

                    this.error = null;
                    this.fetchProjects();
                })
                .catch((error) => {
                    // console.error(error);
                    this.error = error.response.data.message;
                    // alert("An error occurred. Please try again.");
                });
        },
        showEditModal(project) {
            this.editProject = project;
            this.editModalVisible = true;
        },
        closeEditModal() {
            this.editModalVisible = false;
            this.editProject = null;
        },
        updateProject(projectData) {
            axios
                .put(
                    `http://127.0.0.1:8000/api/projects/${this.editProject.id}`,
                    projectData
                )
                .then((response) => {
                    console.log(response);
                    this.fetchProjects();
                    this.closeEditModal();
                })
                .catch((error) => {
                    console.error(error);
                    alert("An error occurred. Please try again.");
                });
        },
        confirmDelete(id) {
            Swal.fire({
                title: "Are you sure?",
                text: "You won't be able to revert this!",
                icon: "warning",
                showCancelButton: true,
                confirmButtonColor: "#3085d6",
                cancelButtonColor: "#d33",
                confirmButtonText: "Yes, delete it!",
            }).then((result) => {
                if (result.isConfirmed) {
                    this.deleteProject(id);
                }
            });
        },
        deleteProject(id) {
            axios
                .delete(`http://127.0.0.1:8000/api/projects/${id}`)
                .then((result) => {
                    this.fetchProjects();
                    console.log(result);
                    Swal.fire(
                        "Deleted!",
                        "Your project has been deleted.",
                        "success"
                    );
                })
                .catch((error) => {
                    console.error(error);
                    alert("An error occurred. Please try again.");
                });
        },
    },
};
</script>
