<script>
  import Board from './components/Board.svelte';
  import ThemeSwitcher from './components/ThemeSwitcher.svelte';

  const currentYear = new Date().getFullYear();
</script>

<style>
  main {
    display: table;
    margin: 0 auto;
  }

  header {
    display: flex;
    flex-direction: row-reverse;
    justify-content: space-between;
    align-items: center;
  }

  h1 {
    font-size: 2rem;
  }

  @media (max-width: 441px) {
    h1 {
      font-size: 7vw; /* responsive typography */
    }
  }

  section {
    background-color: var(--overlay);
    padding: 12px 24px;
    border-radius: 8px;
    box-shadow: 0px 5px 8px -4px black;
  }

  footer {
    text-align: right;
    color: var(--low-muted-text);
    font-size: 0.8rem;
    margin-top: 8px;
  }

  .github {
    /* colorize black part of the logo using the "darkslategray" color
      generated via https://codepen.io/sosuke/pen/Pjoqqp */
    filter: invert(23%) sepia(31%) saturate(536%) hue-rotate(131deg)
      brightness(99%) contrast(86%);
    vertical-align: bottom;
  }
</style>

<main>
  <header>
    <ThemeSwitcher />
    <h1>multiplication &boxbox; square</h1>
  </header>
  <section>
    <Board />
  </section>
  <footer>
    Copyright &copy; {currentYear} wed
    <a
      href="https://github.com/wedk/multiplication-square"
      target="_blank"
      rel="noopener noreferrer"
      title="View on GitHub">
      <img
        src="images/github.png"
        width="18"
        height="18"
        alt="GitHub logo"
        class="github" />
    </a>
  </footer>
</main>
