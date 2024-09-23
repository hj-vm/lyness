<script>
    import { onMount } from 'svelte';
  
    let sections = [];
    let sectionTitles = [];
    let currentIndex = 0;
    let isMenuOpen = false;
  
    // Scroll to the section with the given index
    function scrollToSection(index) {
      if (index < 0) {
        index = sections.length - 1; // Wrap around to the last section
      } else if (index >= sections.length) {
        index = 0; // Wrap around to the first section
      }
      sections[index].scrollIntoView({ behavior: 'smooth' });
      currentIndex = index;
    }
  
    // Scroll to the previous section
    function scrollToPrevious() {
      scrollToSection(currentIndex - 1);
    }
  
    // Scroll to the next section
    function scrollToNext() {
      scrollToSection(currentIndex + 1);
    }
  
    // Get references to the sections and their titles on mount
    onMount(() => {
      sections = document.querySelectorAll('.scroll-section');
      sectionTitles = Array.from(sections).map(section => section.getAttribute('data-title') || 'Untitled Section');
    });
  
    // Toggle the side menu
    function toggleMenu() {
      isMenuOpen = !isMenuOpen;
    }
  </script>
  
  <div class={`fixed top-10 ${isMenuOpen ? 'left-[260px]' : 'left-10'} drop-shadow-xl transition-all duration-300 ease-in-out`}>
    <svg
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 24 24"
      class={`size-16 active:scale-125 transition-all ${isMenuOpen ? 'fill-[#d70000] rotate-45' : 'fill-white'}`}
      on:click={toggleMenu}
    >
      <path fill-rule="evenodd" d="M12 2.25c-5.385 0-9.75 4.365-9.75 9.75s4.365 9.75 9.75 9.75 9.75-4.365 9.75-9.75S17.385 2.25 12 2.25ZM12.75 9a.75.75 0 0 0-1.5 0v2.25H9a.75.75 0 0 0 0 1.5h2.25V15a.75.75 0 0 0 1.5 0v-2.25H15a.75.75 0 0 0 0-1.5h-2.25V9Z" clip-rule="evenodd" />
    </svg>
  </div>
  
  <div class="fixed bottom-10 right-10 flex flex-row gap-2 drop-shadow-xl">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="white" class="size-16 active:scale-125 transition-all" on:click={scrollToPrevious}>
      <path fill-rule="evenodd" d="M12 2.25c-5.385 0-9.75 4.365-9.75 9.75s4.365 9.75 9.75 9.75 9.75-4.365 9.75-9.75S17.385 2.25 12 2.25Zm-4.28 9.22a.75.75 0 0 0 0 1.06l3 3a.75.75 0 1 0 1.06-1.06l-1.72-1.72h5.69a.75.75 0 0 0 0-1.5h-5.69l1.72-1.72a.75.75 0 0 0-1.06-1.06l-3 3Z" clip-rule="evenodd" />
    </svg>
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="white" class="size-16 active:scale-125 transition-all" on:click={scrollToNext}>
      <path fill-rule="evenodd" d="M12 2.25c-5.385 0-9.75 4.365-9.75 9.75s4.365 9.75 9.75 9.75 9.75-4.365 9.75-9.75S17.385 2.25 12 2.25Zm4.28 10.28a.75.75 0 0 0 0-1.06l-3-3a.75.75 0 1 0-1.06 1.06l1.72 1.72H8.25a.75.75 0 0 0 0 1.5h5.69l-1.72 1.72a.75.75 0 1 0 1.06 1.06l3-3Z" clip-rule="evenodd" />
    </svg>
  </div>
  
  <div
    class="fixed top-0 left-0 w-[250px] h-full bg-[#333] text-white transform transition-transform duration-300 ease-in-out"
    class:translate-x-0={isMenuOpen}
    class:-translate-x-full={!isMenuOpen}
  >

    <div class="px-16 py-4 mt-auto">
        <img src="/images/OICw.webp" alt="Orkney Islands Council Logo" class="w-full h-auto" />
    </div>
    {#each sectionTitles as title, index}
      <div class="p-4 border-b border-[#444]" on:click={() => scrollToSection(index)}>
        {title}
      </div>
    {/each}
  </div>