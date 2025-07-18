<template>
  <div id="app">
    <FloatingButton @toggle="showPanel = !showPanel" />
    <MenuPanel v-if="showPanel" :settings="settings" @update="updateSettings" />

    <main :class="{ 'dyslexia-font': settings.dyslexia }">
      <h1> Welcome to Skillblend</h1>
      <p>
        This is a Vue-based accessibility widget demo. Use the floating button to open accessibility options and customize your browsing experience.
      </p>

      <button @click="showImage = !showImage" class="toggle-btn">
        {{ showImage ? 'Hide' : 'Show' }} Image
      </button>
      <div class="bounce-box">ANIAMTION </div>


      <img
        v-if="!settings.hideImages && showImage"
        src="https://vuejs.org/images/logo.png"
        alt="Vue.js Official Logo"
        class="featured-image"
      />

      <p>
        Visit our <a href="#contact">Contact Page</a> or check out <a href="https://vuejs.org/guide/introduction.html">Vue Tips & Resources</a>.
      </p>

      <!-- TEST ZONE -->
      <section>
        <h2> Visual Demo Section</h2>

        <p title="This is a tooltip" aria-label="Helpful paragraph">
          Hover over this paragraph to see tooltip in action.
        </p>

        <div class="spinner"></div>

        <img
          v-if="!settings.hideImages"
          src="https://miro.medium.com/v2/resize:fit:1200/1*wnIEgP1gNMrK5gZU7QS0-A.jpeg"
          alt="Vue Component Architecture"
          class="featured-image"
        />

        <h3>Subheading Level 3</h3>
        <h4>Subheading Level 4</h4>
      </section>

      <footer id="contact">
        <h2> Contact Us</h2>
        <p>Email us at <a href="mailto:sharmap4396@gmail.com">sharmap4396@gmail.com</a></p>
        <p>Visit <a href="https://vuejs.org/guide/introduction.html" target="_blank">vuejs.org</a> for more information.</p>
      </footer>
    </main>
  </div>
</template>

<script>
import FloatingButton from './components/FloatingButton.vue';
import MenuPanel from './components/MenuPanel.vue';

export default {
  components: { FloatingButton, MenuPanel },
  data() {
    return {
      showPanel: false,
      showImage: true,
      settings: JSON.parse(localStorage.getItem('a11y-settings')) || {
        contrast: false,
        bigText: false,
        dyslexia: false,
        highlightLinks: false,
        textSpacing: false,
        pauseAnimations: false,
        hideImages: false,
        enlargeCursor: false,
        showTooltips: false,
        showHeadings: false,
      },
    };
  },
  watch: {
    settings: {
      handler(val) {
        localStorage.setItem('a11y-settings', JSON.stringify(val));
        document.body.classList.toggle('high-contrast', val.contrast);
        document.body.classList.toggle('big-text', val.bigText);
        document.body.classList.toggle('highlight-links', val.highlightLinks);
        document.body.classList.toggle('text-spacing', val.textSpacing);
        document.body.classList.toggle('pause-animations', val.pauseAnimations);
        document.body.classList.toggle('enlarge-cursor', val.enlargeCursor);
        document.body.classList.toggle('show-tooltips', val.showTooltips);
        document.body.classList.toggle('show-headings', val.showHeadings);

        if (val.dyslexia) {
          if (!document.getElementById('dyslexia-font')) {
            const link = document.createElement('link');
            link.href = 'https://cdn.jsdelivr.net/gh/antijingoist/opendyslexic/web/opendyslexic.css';
            link.rel = 'stylesheet';
            link.id = 'dyslexia-font';
            document.head.appendChild(link);
          }
        } else {
          const link = document.getElementById('dyslexia-font');
          if (link) link.remove();
        }
      },
      deep: true,
      immediate: true,
    },
  },
  methods: {
    updateSettings(key, value) {
      this.settings[key] = value;
    },
  },
};
</script>

<style>
body {
  background-color: #eef1f5;
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', sans-serif;
  color: #333;
}

#app {
  min-height: 100vh;
  padding: 2rem;
  background-color: #fff;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.05);
  border-radius: 10px;
  margin: 2rem auto;
  max-width: 900px;
}

main h1, h2, h3, h4 {
  margin-top: 1.5rem;
  color: #2c3e50;
}

p {
  font-size: 1rem;
  line-height: 1.8;
}

button.toggle-btn {
  background-color: #42b883;
  color: white;
  border: none;
  padding: 10px 16px;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
  margin: 1rem 0;
}

button.toggle-btn:hover {
  background-color: #36996d;
}

a {
  color: #42b883;
  text-decoration: underline;
}

img.featured-image {
  display: block;
  margin: 20px auto;
  max-width: 100%;
  height: auto;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

footer {
  margin-top: 4rem;
  padding-top: 2rem;
  border-top: 1px solid #ccc;
  font-size: 0.95rem;
  color: #666;
}

footer a {
  color: #0066cc;
}

.spinner {
  width: 50px;
  height: 50px;
  border: 5px solid #ddd;
  border-top-color: #42b883;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin: 20px auto;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.high-contrast {
  filter: contrast(150%) brightness(1.2);
}

.big-text {
  font-size: 1.2rem;
}

.highlight-links a {
  border-bottom: 2px solid red !important;
}

.text-spacing {
  letter-spacing: 0.05rem;
  line-height: 2;
}

.pause-animations *,
.pause-animations *::before,
.pause-animations *::after {
  animation: none !important;
  transition: none !important;
}

.dyslexia-font {
  font-family: 'OpenDyslexic', Arial, sans-serif !important;
}

.enlarge-cursor {
  cursor: url('https://cur.cursors-4u.net/mechanics/mec-7/mec699.cur'), auto !important;
}

.show-tooltips [title]:hover::after,
.show-tooltips [aria-label]:hover::after {
  content: attr(title);
  position: absolute;
  background: #333;
  color: white;
  padding: 4px 8px;
  font-size: 0.8rem;
  border-radius: 4px;
  white-space: nowrap;
  z-index: 9999;
}

.show-headings h1::before,
.show-headings h2::before,
.show-headings h3::before,
.show-headings h4::before,
.show-headings h5::before,
.show-headings h6::before {
  content: "🔹 ";
  color: #444;
}
.bounce-box {
  width: 200px;
  padding: 10px;
  margin: 20px auto;
  text-align: center;
  background-color: #42b883;
  color: white;
  border-radius: 8px;
  font-weight: bold;
  animation: bounce 1s infinite alternate ease-in-out;
  transition: transform 0.3s ease;
}

@keyframes bounce {
  from {
    transform: translateY(0px);
  }
  to {
    transform: translateY(-15px);
  }
}

</style>
