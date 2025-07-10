 <script>
  export let profile;
</script>
 
 <section id="contact" class="py-16 px-6">
    <div class="max-w-6xl mx-auto text-center">
      <h2 class="text-3xl font-bold text-gray-900 mb-8">Get In Touch</h2>
      <p class="text-lg text-gray-600 mb-8 max-w-2xl mx-auto">
        I'm always open to discussing new opportunities, interesting projects, or just having a chat about technology.
      </p>
      
      <div class="flex flex-wrap justify-center gap-6 mb-8">
        <a 
          href="mailto:{profile.email}"
          class="flex items-center space-x-2 text-gray-600 hover:text-gray-900 transition-colors"
        >
          <span>✉️</span>
          <span>{profile.email}</span>
        </a>
        <a 
          href="tel:{profile.phone}"
          class="flex items-center space-x-2 text-gray-600 hover:text-gray-900 transition-colors"
        >
          <span>📱</span>
          <span>{profile.phone}</span>
        </a>
        <a 
          href="https://github.com/{profile.github}"
          target="_blank"
          rel="noopener noreferrer"
          class="flex items-center space-x-2 text-gray-600 hover:text-gray-900 transition-colors"
        >
          <span>🐙</span>
          <span>GitHub</span>
        </a>
        <a 
          href="https://linkedin.com/in/{profile.linkedin}"
          target="_blank"
          rel="noopener noreferrer"
          class="flex items-center space-x-2 text-gray-600 hover:text-gray-900 transition-colors"
        >
          <span>💼</span>
          <span>LinkedIn</span>
        </a>
      </div>

      <button 
        on:click={() => window.location.href = `mailto:${profile.email}`}
        class="bg-gray-900 text-white px-8 py-3 rounded-lg hover:bg-gray-800 transition-colors"
      >
        Send Message
      </button>
    </div>
  </section>