<script setup lang="ts">
import { ref, reactive } from 'vue'
import emailjs from '@emailjs/browser'
import TitleHeader from '../components/TitleHeader.vue'

const formRef = ref<HTMLFormElement | null>(null)
const loading = ref<boolean>(false)

const form = reactive<{
  name: string
  email: string
  message: string
}>({
  name: '',
  email: '',
  message: ''
})

const toast = reactive({
  show: false,
  type: 'success',
  message: ''
})

const showToast = (type: 'success' | 'error', message: string) => {
  toast.show = true
  toast.type = type
  toast.message = message

  setTimeout(() => {
    toast.show = false
  }, 4000)
}

const handleChange = (e: Event) => {
  const target = e.target as HTMLInputElement | HTMLTextAreaElement
  const { name, value } = target
  ;(form as any)[name] = value
}

const handleSubmit = async (e: Event) => {
  e.preventDefault()
  setLoading(true)

  try {
    if (formRef.value) {
      await emailjs.sendForm(
          import.meta.env.VITE_APP_EMAILJS_SERVICE_ID,
          import.meta.env.VITE_APP_EMAILJS_TEMPLATE_ID,
          formRef.value,
          import.meta.env.VITE_APP_EMAILJS_PUBLIC_KEY
      )

      form.name = ''
      form.email = ''
      form.message = ''

      showToast('success', '✅ Message sent successfully! Thank you for reaching out.')
    }
  } catch (error) {
    console.error('EmailJS Error:', error)
    showToast('error', '❌ Failed to send message. Please try again.')
  } finally {
    setLoading(false)
  }
}

const setLoading = (value: boolean) => {
  loading.value = value
}
</script>

<template>
  <section id="contact" class="flex-center section-padding">
    <div class="w-full h-full md:px-10 px-5">
      <TitleHeader
          title="Get in Touch – Let's Connect"
          sub="💬 Have questions or ideas? Let's talk! 🚀"
      />
      <div class="mt-16">
        <div class="lg:px-32 md:px-16 sm:px-8 px-4">
          <div class="flex-center card-border rounded-xl p-10">
            <form
                ref="formRef"
                @submit="handleSubmit"
                class="w-full flex flex-col gap-7"
            >
              <div>
                <label for="name">Your name</label>
                <input
                    type="text"
                    id="name"
                    name="name"
                    v-model="form.name"
                    @input="handleChange"
                    placeholder="What's your good name?"
                    required
                />
              </div>

              <div>
                <label for="email">Your Email</label>
                <input
                    type="email"
                    id="email"
                    name="email"
                    v-model="form.email"
                    @input="handleChange"
                    placeholder="What's your email address?"
                    required
                />
              </div>

              <div>
                <label for="message">Your Message</label>
                <textarea
                    id="message"
                    name="message"
                    v-model="form.message"
                    @input="handleChange"
                    placeholder="How can I help you?"
                    rows="5"
                    required
                />
              </div>

              <button type="submit">
                <div class="cta-button group">
                  <div class="bg-circle" />
                  <p class="text">
                    {{ loading ? "Sending..." : "Send Message" }}
                  </p>
                  <div class="arrow-wrapper">
                    <img src="/images/arrow-down.svg" alt="arrow" />
                  </div>
                </div>
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>

    <Transition name="toast">
      <div
          v-if="toast.show"
          :class="[
            'fixed top-32 md:right-4 mx-4 z-50 p-4 rounded-lg shadow-lg max-w-sm',
            toast.type === 'success' ? 'bg-green-500 text-white' : 'bg-red-500 text-white'
          ]"
      >
        {{ toast.message }}
      </div>
    </Transition>
  </section>
</template>

<style scoped>
.toast-enter-active,
.toast-leave-active {
  transition: all 0.3s ease;
}
.toast-enter-from {
  opacity: 0;
  transform: translateX(100%);
}
.toast-leave-to {
  opacity: 0;
  transform: translateX(100%);
}
</style>
