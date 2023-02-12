<template>
    <div v-if="auth.user === null" class="row justify-content-center">
        <div class="col-md-4">
            <div class="card border-0 rounded-3 shadow-sm">
                <div class="card-body">
                    <h5>LOGIN</h5>
                    <hr />
                    <form @submit.prevent="storeLogin">
                        <div class="mb-3">
                            <label class="form-label">Email Address</label>
                            <input
                                type="email"
                                class="form-control"
                                v-model="form.email"
                                placeholder="Email Address"
                            />
                        </div>
                        <div v-if="errors.email" class="alert alert-danger">
                            {{
                                toast.success("Login Berhasil", {
                                    autoClose: 3000,
                                    theme: "colored",
                                })
                            }}
                        </div>

                        <div class="mb-3">
                            <label class="form-label">Password</label>
                            <input
                                type="password"
                                class="form-control"
                                v-model="form.password"
                                placeholder="Password"
                            />
                        </div>
                        <div v-if="errors.password" class="alert alert-danger">
                            {{ errors.password }}
                        </div>

                        <button type="submit" class="btn btn-primary w-100">
                            LOGIN
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </div>
    <div v-if="auth.user" class="row justify-content-center">
        <div class="col-md-4">
            <div class="card border-0 rounded-3 shadow-sm">
                <div class="card-body">
                    <h5>
                        Anda Sudah Login silahkan klik
                        <Link href="/posts" class="btn btn-md btn-primary"
                            >Post</Link
                        >
                    </h5>
                    <hr />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
//import layout App
import LayoutApp from "../../Layouts/App.vue";

//import reactivity API dari vue
import { reactive } from "vue";

//import inertia adapter
import { Inertia } from "@inertiajs/inertia";
import { Link } from "@inertiajs/inertia-vue3";

// import { toast } from "vue3-toastify";
// import "vue3-toastify/dist/index.css";

export default {
    //set layout
    layout: LayoutApp,

    //get props
    props: {
        errors: Object,
        auth: Object,
    },
    components: {
        Link,
    },

    //define composition API
    setup() {
        //define state
        const form = reactive({
            email: "",
            password: "",
        });

        //method storeLogin
        const storeLogin = () => {
            //send data ke server
            Inertia.post("/login", {
                email: form.email,
                password: form.password,
            });
        };

        return {
            form,
            storeLogin,
        };
    },
};
</script>

<style></style>
