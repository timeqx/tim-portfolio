<script>
  export let profile;
</script>

<section id="about" class="pt-24 pb-16 px-6">
  <div class="max-w-6xl mx-auto text-center mb-16">
    <h1 class="text-5xl md:text-6xl font-bold text-gray-900 mb-6">
      {profile.name}
    </h1>
    <p class="text-xl md:text-2xl text-gray-600 mb-8">
      {profile.title}
    </p>
    <p class="text-lg text-gray-700 max-w-2xl mx-auto leading-relaxed">
      {profile.bio}
    </p>
  </div>
</section>