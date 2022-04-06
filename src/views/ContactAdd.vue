<template>
    <div v-if="contact" class="page">
        <h4>Thêm Liên Hệ</h4>
        <ContactForm
            :contact="contact"
            @submit:contact="create"
        />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";
import { object } from 'yup/lib/locale';

export default {
    components: {
    ContactForm,
    },
    props: {
        id: { type: String, required: true },
    },
    data() {
        return {
            contact: {
                type:object,
                required: true
            },
            message: "",
        };
    },
    methods: {
      async create(data) {
            try {
                await ContactService.create( data);
                this.message = "Liên hệ được lưu thành công.";
            } catch (error) {
                console.log(error);
            }
        },
    
    
    },
    
    
};
</script>