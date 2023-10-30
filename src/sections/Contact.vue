<script setup>
import SectionHeading from "@/components/SectionHeading.vue";
import NButton from "@/components/NButton.vue";
import InputField from "@/components/InputField.vue";
import { reactive, ref } from "vue";
import InputLabel from "@/components/InputLabel.vue";
import TextArea from "@/components/TextArea.vue";
import Toast from "@/components/Toast.vue";

const api = "https://Dinesh.canbebd.com/api/v1/messages";

let contactForm = reactive({
    name: "",
    email: "",
    subject: "",
    message: "",
});

let contactFormErrors = reactive({
    name: "",
    email: "",
    subject: "",
    message: "",
});

let loading = ref(false);

let showToast = ref(false);
let handleClose = () => {
    showToast.value = false;
};

let submitContactForm = () => {
    loading.value = true;

    fetch(api, {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
            Accept: "application/json",
        },
        body: JSON.stringify(contactForm),
    })
        .then((response) => {
            if (response.status === 201) {
                contactForm.name = "";
                contactForm.email = "";
                contactForm.subject = "";
                contactForm.message = "";

                return response.json();
            } else if (response.status === 422) {
                return response.json();
            } else {
                loading.value = false;
                throw new Error("Something went wrong");
            }
        })
        .then((data) => {
            if (data.errors) {
                contactFormErrors.name = data.errors.name ? data.errors.name[0] : "";
                contactFormErrors.email = data.errors.email ? data.errors.email[0] : "";
                contactFormErrors.subject = data.errors.subject ? data.errors.subject[0] : "";
                contactFormErrors.message = data.errors.message ? data.errors.message[0] : "";

                loading.value = false;
            } else {
                contactFormErrors.name = "";
                contactFormErrors.email = "";
                contactFormErrors.subject = "";
                contactFormErrors.message = "";

                showToast.value = true;
                setTimeout(() => {
                    showToast.value = false;
                }, 10000);

                loading.value = false;
            }
        });
};
</script>

<template>
    <transition name="fade" mode="in-out">
        <Toast v-if="showToast" :message="'Thank You, for your message! Will get back to you shortly.'" @close="handleClose"/>
    </transition>
    
    <!-- Contact -->
    <section id="contact" class="relative py-28 lg:py-36 overflow-hidden">
        <div class="absolute top-44 -left-64 h-[250px] w-[900px] -rotate-25 rounded-3xl bg-gradient-to-r from-cyan-600 to-indigo-800 opacity-20 dark:opacity-20 blur-3xl filter block"></div>
        <div class="container px-3 mx-auto max-w-6xl 2xl:max-w-7xl">
            <SectionHeading>Get In Touch</SectionHeading>

            <div class="grid grid-cols-1 md:grid-cols-12 gap-10 dark:text-slate-300 tracking-wide">
                <div class="grid grid-cols-1 md:grid-cols-12 gap-10 dark:text-slate-300 tracking-wide">
    <div class="md:col-span-5">
        <h3 class="font-medium text-3xl mb-2 dark:text-white">Quick Contact</h3>
        <ul class="mt-12 space-y-8 flex flex-col md:flex-row md:space-x-8">
            
            <li class="flex items-center space-x-4">
                <div>
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-7 h-7 dark:text-primary-300 text-primary-500">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M21.75 9v.906a2.25 2.25 0 01-1.183 1.981l-6.478 3.488M2.25 9v.906a2.25 2.25 0 001.183 1.981l6.478 3.488m8.839 2.51l-4.66-2.51m0 0l-1.023-.55a2.25 2.25 0 00-2.134 0l-1.022.55m0 0l-4.661 2.51m16.5 1.615a2.25 2.25 0 01-2.25 2.25h-15a2.25 2.25 0 01-2.25-2.25V8.844a2.25 2.25 0 011.183-1.98l7.5-4.04a2.25 2.25 0 012.134 0l7.5 4.04a2.25 2.25 0 011.183 1.98V19.5z" />
                    </svg>
                </div>
                <div>
                    
                    <h4 class="text-xl dark:text-white mb-1">Email</h4>
                    <p><a href="mailto:dineshlokesh0406@gmail.com" class="transition-all duration-300 hover:text-secondary-500 dark:hover:text-secondary-300">dineshlokesh0406@gmail.com</a></p>
                </div>
            </li>

            
            <li class="flex items-center space-x-4">
                <div>
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-7 h-7 dark:text-primary-300 text-primary-500">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M7.5 8.25h9m-9 3H12m-9.75 1.51c0 1.6 1.123 2.994 2.707 3.227 1.129.166 2.27.293 3.423.379.35.026.67.21.865.501L12 21l2.755-4.133a1.14 1.14 0 01.865-.501 48.172 48.172 0 003.423-.379c1.584-.233 2.707-1.626 2.707-3.228V6.741c0-1.602-1.123-2.995-2.707-3.228A48.394 48.394 0 0012 3c-2.392 0-4.744.175-7.043.513C3.373 3.746 2.25 5.14 2.25 6.741v6.018z" />
                                </svg>
                </div>
                <div>
                    <h4 class="text-xl dark:text-white mb-1">Social&nbsp;Media</h4>
                    <ul class="flex items-center space-x-2">
                        <li>
                            <a href="https://www.linkedin.com/in/dineshlokesh/" target="_blank">
                                <svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" viewBox="0 0 24 24" class="fill-current transition-all duration-300 hover:fill-secondary-500 dark:hover:fill-secondary-400">
                                    <path d="M0 1.146C0 .513.526 0 1.175 0h13.65C15.474 0 16 .513 16 1.146v13.708c0 .633-.526 1.146-1.175 1.146H1.175C.526 16 0 15.487 0 14.854V1.146zm4.943 12.248V6.169H2.542v7.225h2.401zm-1.2-8.212c.837 0 1.358-.554 1.358-1.248-.015-.709-.52-1.248-1.342-1.248-.822 0-1.359.54-1.359 1.248 0 .694.521 1.248 1.327 1.248h.016zm4.908 8.212V9.359c0-.216.016-.432.08-.586.173-.431.568-.878 1.232-.878.869 0 1.216.662 1.216 1.634v3.865h2.401V9.25c0-2.22-1.184-3.252-2.764-3.252-1.274 0-1.845.7-2.165 1.193v.025h-.016a5.54 5.54 0 0 1 .016-.025V6.169h-2.4c.03.678 0 7.225 0 7.225h2.4z"/>
                                </svg>
                            </a>
                        </li>
                        <li>
                            <a href="https://github.com/Dineshlokesh0406" target="_blank">
                                <svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" viewBox="0 0 24 24" class="fill-current transition-all duration-300 hover:fill-secondary-500 dark:hover:fill-secondary-400">
                                    <path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.012 8.012 0 0 0 16 8c0-4.42-3.58-8-8-8z"/>
                                </svg>
                            </a>
                        </li>
                        <li>
                            <a href="https://instagram.com/mr.dini.gowda?igshid=YTQwZjQ0NmI0OA==" target="_blank">
                                <svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" viewBox="0 0 24 24" class="fill-current transition-all duration-300 hover:fill-secondary-500 dark:hover:fill-secondary-400">
                                    <path d="M8 0C5.829 0 5.556.01 4.703.048 3.85.088 3.269.222 2.76.42a3.917 3.917 0 0 0-1.417.923A3.927 3.927 0 0 0 .42 2.76C.222 3.268.087 3.85.048 4.7.01 5.555 0 5.827 0 8.001c0 2.172.01 2.444.048 3.297.04.852.174 1.433.372 1.942.205.526.478.972.923 1.417.444.445.89.719 1.416.923.51.198 1.09.333 1.942.372C5.555 15.99 5.827 16 8 16s2.444-.01 3.298-.048c.851-.04 1.434-.174 1.943-.372a3.916 3.916 0 0 0 1.416-.923c.445-.445.718-.891.923-1.417.197-.509.332-1.09.372-1.942C15.99 10.445 16 10.173 16 8s-.01-2.445-.048-3.299c-.04-.851-.175-1.433-.372-1.941a3.926 3.926 0 0 0-.923-1.417A3.911 3.911 0 0 0 13.24.42c-.51-.198-1.092-.333-1.943-.372C10.443.01 10.172 0 7.998 0h.003zm-.717 1.442h.718c2.136 0 2.389.007 3.232.046.78.035 1.204.166 1.486.275.373.145.64.319.92.599.28.28.453.546.598.92.11.281.24.705.275 1.485.039.843.047 1.096.047 3.231s-.008 2.389-.047 3.232c-.035.78-.166 1.203-.275 1.485a2.47 2.47 0 0 1-.599.919c-.28.28-.546.453-.92.598-.28.11-.704.24-1.485.276-.843.038-1.096.047-3.232.047s-2.39-.009-3.233-.047c-.78-.036-1.203-.166-1.485-.276a2.478 2.478 0 0 1-.92-.598 2.48 2.48 0 0 1-.6-.92c-.109-.281-.24-.705-.275-1.485-.038-.843-.046-1.096-.046-3.233 0-2.136.008-2.388.046-3.231.036-.78.166-1.204.276-1.486.145-.373.319-.64.599-.92.28-.28.546-.453.92-.598.282-.11.705-.24 1.485-.276.738-.034 1.024-.044 2.515-.045v.002zm4.988 1.328a.96.96 0 1 0 0 1.92.96.96 0 0 0 0-1.92zm-4.27 1.122a4.109 4.109 0 1 0 0 8.217 4.109 4.109 0 0 0 0-8.217zm0 1.441a2.667 2.667 0 1 1 0 5.334 2.667 2.667 0 0 1 0-5.334z"/>
                                </svg>
                            </a>
                        </li>
                        
                    </ul>
                </div>
            </li>

            <!-- Location Section -->
            <li class="flex items-center space-x-4">
                <div>
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-7 h-7 text-primary-500 dark:text-primary-300">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M9 6.75V15m6-6v8.25m.503 3.498l4.875-2.437c.381-.19.622-.58.622-1.006V4.82c0-.836-.88-1.38-1.628-1.006l-3.869 1.934c-.317.159-.69.159-1.006 0L9.503 3.252a1.125 1.125 0 00-1.006 0L3.622 5.689C3.24 5.88 3 6.27 3 6.695V19.18c0 .836.88 1.38 1.628 1.006l3.869-1.934c.317-.159.69-.159 1.006 0l4.994 2.497c.317.158.69.158 1.006 0z" />
                                </svg>
                </div>
                <div>
                    <h4 class="text-xl dark:text-white mb-1">Location</h4>
                    <p><a href="https://maps.app.goo.gl/6xLyMFZDts1L9U8S6" target="_blank" class="transition-all duration-300 hover:text-secondary-500 dark:hover:text-secondary-300">Byragondlu,Tumkur</a></p>
                </div>
            </li>
        </ul>
    </div>
                </div>

                
            </div>
        </div>
    </section>
    <!-- Contact -->
</template>

<style scoped>
.fade-enter-from,
.fade-leave-to {
    transform: translateY(-120px);
    opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
    transition-duration: 300ms;
    transition-property: transform, opacity;
    transition-timing-function: cubic-bezier(0.6, 0.15, 0.35, 0.8);
}
</style>
<!--<div class="md:col-span-5">
                    <h3 class="font-medium text-3xl mb-2 dark:text-white">Quick Contact</h3>
                    <ul class="mt-12 space-y-8">
                        <li class="flex items-center space-x-4">
                            <div>
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-7 h-7 dark:text-primary-300 text-primary-500">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M21.75 9v.906a2.25 2.25 0 01-1.183 1.981l-6.478 3.488M2.25 9v.906a2.25 2.25 0 001.183 1.981l6.478 3.488m8.839 2.51l-4.66-2.51m0 0l-1.023-.55a2.25 2.25 0 00-2.134 0l-1.022.55m0 0l-4.661 2.51m16.5 1.615a2.25 2.25 0 01-2.25 2.25h-15a2.25 2.25 0 01-2.25-2.25V8.844a2.25 2.25 0 011.183-1.98l7.5-4.04a2.25 2.25 0 012.134 0l7.5 4.04a2.25 2.25 0 011.183 1.98V19.5z" />
                                </svg>
                            </div>
                            <div>
                                <h4 class="text-xl dark:text-white mb-1">Email</h4>
                                <p><a href="mailto:dineshlokesh0406@gmail.com" class="transition-all duration-300 hover:text-secondary-500 dark:hover:text-secondary-300">dineshlokesh0406@gmail.com</a></p>
                            </div>
                        </li>
                        <li class="flex items-center space-x-4">
                            <div>
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-7 h-7 dark:text-primary-300 text-primary-500">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M7.5 8.25h9m-9 3H12m-9.75 1.51c0 1.6 1.123 2.994 2.707 3.227 1.129.166 2.27.293 3.423.379.35.026.67.21.865.501L12 21l2.755-4.133a1.14 1.14 0 01.865-.501 48.172 48.172 0 003.423-.379c1.584-.233 2.707-1.626 2.707-3.228V6.741c0-1.602-1.123-2.995-2.707-3.228A48.394 48.394 0 0012 3c-2.392 0-4.744.175-7.043.513C3.373 3.746 2.25 5.14 2.25 6.741v6.018z" />
                                </svg>
                            </div>
                            <div>
                                <h4 class="text-xl dark:text-white mb-1">Social Media</h4>
                                <ul class="flex items-center space-x-2">
                                    <li>
                                        <a href="https://www.facebook.com/Dinesh.faysal.3152/" target="_blank">
                                            <svg xmlns="http://www.w3.org/2000/svg" width="26" height="26" viewBox="0 0 24 24" class="fill-current transition-all duration-300 hover:fill-secondary-500 dark:hover:fill-secondary-400">
                                            <path d="M12 0C5.4 0 0 5.4 0 12c0 5.3 3.8 9.8 8.7 11.3 0.6 0.1 0.8-0.3 0.8-0.6 0-0.3 0-1.2 0-2.3-3.2 0.7-3.8-1.5-3.8-1.5C4.2 17 4 15.8 4 15.8c-1.1-0.8 0.1-0.8 0.1-0.8 1.2 0.1 1.8 1.2 1.8 1.2 1 1.7 2.7 1.2 3.3 0.9 0.1-0.8 0.4-1.2 0.7-1.5-2.6-0.3-5.3-1.3-5.3-5.9 0-1.3 0.5-2.4 1.2-3.3-0.1-0.3-0.5-1.5 0.1-3.1 0 0 1-0.3 3.2 1.3 1-0.3 2-0.5 3-0.5s2 0.2 3 0.5c2.3-1.6 3.3-1.3 3.3-1.3 0.6 1.6 0.2 3 0.1 3.3 0.7 0.9 1.2 2 1.2 3.3 0 4.6-2.9 5.6-5.5 5.9 0.4 0.4 0.8 1.1 0.8 2.3 0 1.7 0 3.1 0 3.5 0 0.3 0.2 0.7 0.8 0.6C20.2 21.8 24 17.3 24 12 24 5.4 18.6 0 12 0z"></path>
                                            </svg>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="https://www.linkedin.com/in/dineshlokesh/" target="_blank">
                                            <svg xmlns="http://www.w3.org/2000/svg" width="26" height="26" viewBox="0 0 24 24" class="fill-current transition-all duration-300 hover:fill-secondary-500 dark:hover:fill-secondary-400">
                                                <path d="M20 3H4a1 1 0 0 0-1 1v16a1 1 0 0 0 1 1h16a1 1 0 0 0 1-1V4a1 1 0 0 0-1-1zM8.339 18.337H5.667v-8.59h2.672v8.59zM7.003 8.574a1.548 1.548 0 1 1 0-3.096 1.548 1.548 0 0 1 0 3.096zm11.335 9.763h-2.669V14.16c0-.996-.018-2.277-1.388-2.277-1.39 0-1.601 1.086-1.601 2.207v4.248h-2.667v-8.59h2.56v1.174h.037c.355-.675 1.227-1.387 2.524-1.387 2.704 0 3.203 1.778 3.203 4.092v4.71z"></path>
                                            </svg>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="#" target="_blank">
                                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" class="fill-current transition-all duration-300 hover:fill-secondary-500 dark:hover:fill-secondary-400">
                                            <path d="M12 0C5.4 0 0 5.4 0 12c0 5.3 3.8 9.8 8.7 11.3 0.6 0.1 0.8-0.3 0.8-0.6 0-0.3 0-1.2 0-2.3-3.2 0.7-3.8-1.5-3.8-1.5C4.2 17 4 15.8 4 15.8c-1.1-0.8 0.1-0.8 0.1-0.8 1.2 0.1 1.8 1.2 1.8 1.2 1 1.7 2.7 1.2 3.3 0.9 0.1-0.8 0.4-1.2 0.7-1.5-2.6-0.3-5.3-1.3-5.3-5.9 0-1.3 0.5-2.4 1.2-3.3-0.1-0.3-0.5-1.5 0.1-3.1 0 0 1-0.3 3.2 1.3 1-0.3 2-0.5 3-0.5s2 0.2 3 0.5c2.3-1.6 3.3-1.3 3.3-1.3 0.6 1.6 0.2 3 0.1 3.3 0.7 0.9 1.2 2 1.2 3.3 0 4.6-2.9 5.6-5.5 5.9 0.4 0.4 0.8 1.1 0.8 2.3 0 1.7 0 3.1 0 3.5 0 0.3 0.2 0.7 0.8 0.6C20.2 21.8 24 17.3 24 12 24 5.4 18.6 0 12 0z"></path>
                                            </svg>
                                        </a>
                                    </li>
                                </ul>
                            </div>
                        </li>
                        <li class="flex items-center space-x-4">
                            <div>
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-7 h-7 text-primary-500 dark:text-primary-300">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M9 6.75V15m6-6v8.25m.503 3.498l4.875-2.437c.381-.19.622-.58.622-1.006V4.82c0-.836-.88-1.38-1.628-1.006l-3.869 1.934c-.317.159-.69.159-1.006 0L9.503 3.252a1.125 1.125 0 00-1.006 0L3.622 5.689C3.24 5.88 3 6.27 3 6.695V19.18c0 .836.88 1.38 1.628 1.006l3.869-1.934c.317-.159.69-.159 1.006 0l4.994 2.497c.317.158.69.158 1.006 0z" />
                                </svg>
                            </div>
                            <div>
                                <h4 class="text-xl dark:text-white mb-1">Location</h4>
                                <p><a href="https://maps.app.goo.gl/6xLyMFZDts1L9U8S6" target="_blank" class="transition-all duration-300 hover:text-secondary-500 dark:hover:text-secondary-300">Byragondlu,Tumkur</a></p>
                            </div>
                        </li>
                    </ul>
                </div>-->