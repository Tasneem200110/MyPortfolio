<template>
  <section id="contact" class="contact">
    <div class="contact-inner">
      <!-- Left: Form -->
      <form class="contact-form" @submit.prevent="onSubmit">
        <input v-model="form.name" type="text" placeholder="Your name" aria-label="Your name" required />
        <input v-model="form.email" type="email" placeholder="Email" aria-label="Email" required />
        <input v-model="form.website" type="url" placeholder="Your website (If exists)" aria-label="Website" />
        <textarea v-model="form.message" rows="6" placeholder="How can I help?*" aria-label="Message" required />

        <div class="actions">
          <button type="submit" class="btn primary" :disabled="sending">
            {{ sending ? 'Sending…' : 'Get In Touch' }}
          </button>
          <div class="socials fade-up delay-4" aria-label="Social links">
          <a class="social outline" :href="links.github" target="_blank" aria-label="GitHub">
            <i class="fa-brands fa-github"></i>
          </a>
          <a class="social outline" :href="links.linkedin" target="_blank" aria-label="Linkedin">
            <i class="fa-brands fa-linkedin"></i>
          </a>
          <a class="social outline" :href="links.whatsapp" target="_blank" aria-label="Whatsapp">
            <i class="fa-brands fa-whatsapp"></i>
          </a>
        </div>
        </div>
      </form>
      <p v-if="errorMsg" class="error">{{ errorMsg }}</p>

      <!-- Right: Copy -->
      <div class="contact-copy">
        <h2 class="title special">
          Let's <span class="outlined">talk</span> for
          <br />
          <span class="special">Something special</span>
        </h2>
        <p class="desc">
          I seek to push the limits of creativity to create high‑engaging, user‑friendly,
          and memorable interactive experiences.
        </p>
        <div class="info">
          <a :href="`mailto:${email}`" class="link">{{ email }}</a>
          <a :href="phoneHref" class="link">{{ phone }}</a>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { reactive, computed, ref } from 'vue'

const props = defineProps({
  email: { type: String, default: 'tasneemmostafa200110@gmail.com' },
  phone: { type: String, default: '(+20) 1119360459' },
  links: {
    type: Object,
    default: () => ({
      github: 'https://github.com/',
      linkedin: 'https://www.linkedin.com/',
      whatsapp: 'https://wa.me/'
    })
  }
})

const email = computed(() => props.email?.trim())
const phone = computed(() => props.phone)
const links = computed(() => props.links)
// Sanitize phone to a tel:+E164-ish format
const phoneHref = computed(() => {
  const raw = String(props.phone || '')
  const plus = raw.trim().startsWith('+')
  const digits = raw.replace(/[^0-9]/g, '')
  return `tel:${plus ? '+' : ''}${digits}`
})

const form = reactive({ name: '', email: '', website: '', message: '' })
const sending = ref(false)
const errorMsg = ref('')

async function onSubmit() {
  if (sending.value) return
  errorMsg.value = ''
  // Very light validation
  if (!form.name || !form.email || !form.message) {
    errorMsg.value = 'Please fill the required fields.'
    return
  }
  try {
    sending.value = true
    // Try JSON endpoint first
    const jsonRes = await fetch(`https://formsubmit.co/ajax/${encodeURIComponent(email.value)}` , {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'Accept': 'application/json' },
      body: JSON.stringify({
        name: form.name,
        email: form.email,
        website: form.website,
        message: form.message,
        _subject: 'Portfolio Contact',
        _captcha: 'false',
        _template: 'table'
      })
    })
    let ok = jsonRes.ok
    let data
    try { data = await jsonRes.json() } catch (_) { data = null }
    const success = data && (data.success === true || data.success === 'true')

    if (!ok || !success) {
      // Fallback: URL-encoded submission (some environments block JSON)
      const params = new URLSearchParams()
      params.set('name', form.name)
      params.set('email', form.email)
      params.set('website', form.website)
      params.set('message', form.message)
      params.set('_subject', 'Portfolio Contact')
      params.set('_captcha', 'false')
      params.set('_template', 'table')
      const formRes = await fetch(`https://formsubmit.co/${encodeURIComponent(email.value)}`, {
        method: 'POST',
        headers: { 'Accept': 'application/json', 'Content-Type': 'application/x-www-form-urlencoded' },
        body: params.toString()
      })
      if (!formRes.ok) {
        const txt = await formRes.text()
        throw new Error(txt || (data && data.message) || 'Failed to send')
      }
    }

    alert('Thanks! Your message was sent successfully.')
    form.name = ''
    form.email = ''
    form.website = ''
    form.message = ''
  } catch (err) {
    console.error(err)
    errorMsg.value = (err && err.message) ? `Error: ${err.message}` : 'Sorry, failed to send. Please try again later.'
  } finally {
    sending.value = false
  }
}
</script>

<style scoped>
.contact {
  background: #ffffff;
  padding: 72px 0;
}
.contact-inner {
  margin: 0 120px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  align-items: start;
}
.outlined {
  font-weight: 900;
  color: transparent;
  -webkit-text-stroke: 2px #111;
}
/* Left */
.contact-form {
  display: grid;
  gap: 14px;
}
.contact-form input,
.contact-form textarea {
  width: 100%;
  border: 1px solid #e5e5e5;
  background: #fff;
  border-radius: 8px;
  padding: 14px 16px;
  font-size: 16px;
  color: #0b0b0b;
}
.contact-form textarea { resize: vertical; }

.actions {
  display: flex;
  gap: 12px;
  align-items: center;
  margin-top: 4px;
}
.socials {
  display: flex;
  gap: 14px;
}
.social {
  width: 44px;
  height: 44px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 10px;
  font-size: 16px;
  transition: transform 0.12s ease, background 0.2s ease, color 0.2s ease, box-shadow 0.2s ease;
}
.social.filled {
  background: #0b0b0b;
  color: #fff;
  box-shadow: 0 8px 24px rgba(0,0,0,0.12);
}
.social.outline {
  color: #0b0b0b;
  border: 1.5px solid #0b0b0b;
}
.social:hover { transform: translateY(-2px); }
.social:active { transform: translateY(0); }

/* Hover styles for social links */
.social.outline:hover {
  background: #0b0b0b;
  color: #ffffff;
  border-color: transparent;
  box-shadow: 0 10px 28px rgba(0,0,0,0.14);
}
.social.filled:hover {
  background: #111111;
  box-shadow: 0 12px 32px rgba(0,0,0,0.16);
}

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 44px;
  padding: 0 18px;
  border-radius: 8px;
  border: 1px solid #0b0b0b;
  color: #0b0b0b;
  background: #fff;
  text-decoration: none;
  cursor: pointer;
  transition: transform .15s ease, background .2s ease, color .2s ease;
}
.btn.primary {
  background: #0b0b0b;
  color: #fff;
  border-color: #0b0b0b;
}
.btn.icon {
  width: 44px;
  padding: 0;
  background: #fff;
}
.btn:hover { transform: translateY(-2px); }
.btn:active { transform: translateY(0); }
.btn[disabled] {
  opacity: 0.6;
  cursor: not-allowed;
  transform: none;
}

/* Right */
.contact-copy .title {
  margin: 0 0 12px 0;
  font-size: clamp(28px, 6vw, 44px);
  color: #0b0b0b;
  line-height: 1.15;
}
.contact-copy .talk { font-weight: 800; text-decoration: underline; }
.contact-copy .special { font-weight: 800; }
.desc {
  color: #4b4b4b;
  margin-bottom: 18px;
  line-height: 1.7;
}
.info { display: grid; gap: 8px; }
.link { color: #0b0b0b; text-decoration: none; }
.link:hover { text-decoration: underline; }

.error {
  color: #c0392b;
  font-size: 14px;
  margin-top: 8px;
}

@media (max-width: 980px) {
  .contact-inner { margin: 0 24px; grid-template-columns: 1fr; }
}
</style>
