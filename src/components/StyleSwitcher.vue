<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const STYLES = [
  { id: 'professional', label: 'Professional', dot: '#2563EB' },
  { id: 'glassmorphism', label: 'Glassmorphism', dot: 'linear-gradient(135deg,#c2a3f7,#9fd0f7)' },
  { id: 'neumorphism', label: 'Neumorphism', dot: '#e8ebf2' },
  { id: 'neobrutalism', label: 'Neobrutalism', dot: '#ffe45e' },
  { id: 'flat', label: 'Flat design', dot: '#94A3B8' },
  { id: 'minimalism', label: 'Minimalism', dot: '#fafafa' },
]

const KEY = 'portfolio-style'
const VALID = STYLES.map((s) => s.id)

const isOpen = ref(false)
const current = ref('professional')
const rootEl = ref(null)

function apply(id) {
  if (!VALID.includes(id)) id = 'professional'
  document.documentElement.setAttribute('data-style', id)
  current.value = id
  try {
    localStorage.setItem(KEY, id)
  } catch (e) {}
}

function pick(id) {
  apply(id)
  isOpen.value = false
}

function onDocClick(e) {
  if (rootEl.value && !rootEl.value.contains(e.target)) isOpen.value = false
}

onMounted(() => {
  let saved = null
  try {
    saved = localStorage.getItem(KEY)
  } catch (e) {}
  apply(VALID.includes(saved) ? saved : 'professional')
  document.addEventListener('click', onDocClick)
})

onBeforeUnmount(() => document.removeEventListener('click', onDocClick))
</script>

<template>
  <div ref="rootEl" class="style-switcher">
    <button
      class="style-gear"
      type="button"
      title="Change style"
      aria-label="Change design style"
      :aria-expanded="isOpen"
      @click.stop="isOpen = !isOpen"
    >
      <svg viewBox="0 0 24 24" width="17" height="17" aria-hidden="true">
        <path
          fill="currentColor"
          d="M19.43 12.98c.04-.32.07-.64.07-.98s-.03-.66-.07-.98l2.11-1.65a.5.5 0 0 0 .12-.64l-2-3.46a.5.5 0 0 0-.61-.22l-2.49 1a7.3 7.3 0 0 0-1.69-.98l-.38-2.65A.49.49 0 0 0 14 2h-4a.49.49 0 0 0-.49.42l-.38 2.65c-.61.25-1.17.59-1.69.98l-2.49-1a.5.5 0 0 0-.61.22l-2 3.46a.5.5 0 0 0 .12.64l2.11 1.65c-.04.32-.07.64-.07.98s.03.66.07.98l-2.11 1.65a.5.5 0 0 0-.12.64l2 3.46c.14.24.42.34.61.22l2.49-1c.52.39 1.08.73 1.69.98l.38 2.65c.04.24.24.42.49.42h4c.25 0 .45-.18.49-.42l.38-2.65a7.3 7.3 0 0 0 1.69-.98l2.49 1c.23.09.49 0 .61-.22l2-3.46a.5.5 0 0 0-.12-.64l-2.11-1.65ZM12 15.5A3.5 3.5 0 1 1 12 8.5a3.5 3.5 0 0 1 0 7Z"
        />
      </svg>
    </button>

    <Transition name="pop">
      <div v-if="isOpen" class="style-popover">
        <p class="style-pop-title">Design style</p>
        <button
          v-for="s in STYLES"
          :key="s.id"
          class="style-row"
          :class="{ 'is-current': s.id === current }"
          type="button"
          @click="pick(s.id)"
        >
          <span class="dot" :style="{ background: s.dot }"></span>
          <span class="label">{{ s.label }}</span>
          <span v-if="s.id === current" class="tick">✓</span>
        </button>
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.style-switcher {
  position: relative;
  flex-shrink: 0;
}

.style-gear {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  color: var(--text-secondary);
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 10px;
  cursor: pointer;
  transition: color 0.15s ease, border-color 0.15s ease;
}
.style-gear:hover {
  color: var(--primary);
}

.style-popover {
  position: absolute;
  top: calc(100% + 10px);
  right: 0;
  z-index: 200; /* above .nav (z-index: 100) */
  min-width: 200px;
  padding: 8px;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 12px;
  box-shadow: var(--shadow);
}

.style-pop-title {
  font-size: 0.72rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--text-secondary);
  padding: 4px 8px 8px;
}

.style-row {
  display: flex;
  align-items: center;
  gap: 10px;
  width: 100%;
  padding: 8px;
  border: none;
  background: transparent;
  border-radius: 8px;
  color: var(--text);
  font-family: var(--font-code);
  font-size: 0.85rem;
  cursor: pointer;
  text-align: left;
}
.style-row:hover {
  background: var(--surface-soft);
}
.style-row.is-current {
  color: var(--primary);
}

.dot {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  border: 1px solid var(--border);
  flex-shrink: 0;
}

.tick {
  margin-left: auto;
  color: var(--success);
}

.pop-enter-active,
.pop-leave-active {
  transition: opacity 0.15s ease, transform 0.15s ease;
}
.pop-enter-from,
.pop-leave-to {
  opacity: 0;
  transform: translateY(-4px);
}
</style>
