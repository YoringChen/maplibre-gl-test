<script setup>
import { onMounted } from 'vue'
import maplibregl from 'maplibre-gl'

function isWebglSupported() {
    if (window.WebGLRenderingContext) {
        const canvas = document.createElement('canvas');
        try {
            // Note that { failIfMajorPerformanceCaveat: true } can be passed as a second argument
            // to canvas.getContext(), causing the check to fail if hardware rendering is not available. See
            // https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/getContext
            // for more details.
            const context = canvas.getContext('webgl2') || canvas.getContext('webgl');
            if (context && typeof context.getParameter == 'function') {
                return true;
            }
        } catch (e) {
            // WebGL is supported, but disabled
        }
        return false;
    }
    // WebGL not supported
    return false;
}

onMounted(() => {
  if (!isWebglSupported()) {
      alert('Your browser does not support MapLibre GL');
  } else {
      const map = new maplibregl.Map({
          container: 'map',
          style:
          'https://api.maptiler.com/maps/streets/style.json?key=MXkPxGcDNpW1xFokGCAM',
          center: [-74.5, 40],
          zoom: 9
      });
  }
})
</script>

<template>
  <div id="map"></div>
</template>

<style scoped>
body { margin: 0; padding: 0; }
html, body { height: 100%; }
#map { height: 500px; }
</style>