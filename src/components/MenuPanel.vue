<template>
  <div class="menu-panel">
    <h3>Accessibility Settings</h3>
    <div>
    <label>
  <input
    type="checkbox"
    :checked="settings.pauseAnimations"
    @change="$emit('update', 'pauseAnimations', $event.target.checked)"
  />
  Pause Animations
</label>

      <label>
  <input
    type="checkbox"
    :checked="settings.contrast"
    @change="$emit('update', 'contrast', $event.target.checked)"
  />
  High Contrast
</label>

<label>
  <input
    type="checkbox"
    :checked="settings.bigText"
    @change="$emit('update', 'bigText', $event.target.checked)"
  />
  Bigger Text
</label>

<label>
  <input
    type="checkbox"
    :checked="settings.dyslexia"
    @change="$emit('update', 'dyslexia', $event.target.checked)"
  />
  Dyslexia-Friendly Font
</label>

<!-- ✅ Correct new entry -->
<label>
  <input
    type="checkbox"
    :checked="settings.highlightLinks"
    @change="$emit('update', 'highlightLinks', $event.target.checked)"
  />
  Highlight Links
</label>



    </div>
  </div>
</template>

<script>
export default {
  props: ['settings'],
};
</script>

<style>
.menu-panel {
  position: fixed;
  bottom: 70px;
  right: 20px;
  background: white;
  border: 1px solid #ccc;
  padding: 15px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  z-index: 9998;
  width: 250px;
}
.menu-panel label {
  display: block;
  margin: 10px 0;
}
</style>
