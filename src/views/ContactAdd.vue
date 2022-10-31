<template>
    <div v-if="contact" class="page">
        <h4>Thêm Liên hệ mới</h4>
        <ContactForm :contact="contact" @add:contact="addContact"/>
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";

import ContactService from "@/services/contact.service";
export default {
    components: {
        ContactForm,
    },
    
    data() {
        return {
            contact: {
                name: '',
                email: '',
                address: '',
                phone: '',
                favorite: false,
            },
            //message: 'Nhận dữ liệu từ Form!',
        };
    },

    methods: {
        async addContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Liên hệ được THÊM thành công.";
                console.log("Liên hệ được THÊM thành công.");
                confirm("Thêm liên hệ thành công!");
            } catch (error) {
                console.log(error);
            }
            console.log(data);
        },
        
        
    },
};
</script>
