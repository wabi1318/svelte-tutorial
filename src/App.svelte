<script>
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'
</script>

<header class="header">
  <a class="header-title" href="/">Svelte EC</a>
  <nav>
    <ul class="header-links">
      <li>ようこそゲストさん</li>
      <li>
        <a href="/cart">カート (0)</a>
      </li>
    </ul>
  </nav>
</header>

<article class="product">
  <div class="product-main">
    <div class="image-container">
      <img src="https://github.com/svelte-book/sample-app/raw/main/static/react-book-1.png" alt="『Svelte Guide』表紙" />
    </div>
  </div>

  <div>
    <h2>Svelte Guide</h2>
    <dl>
      <dt>価格</dt>
      <dd>3500円</dd>
    </dl>
    <div>
      <button>カートに入れる</button>
    </div>
  </div>

  <footer>
    <h3>関連商品</h3>
    <ul>
      <li>
        <a href="/products/react-book">React book</a>
        - 3500円
      </li>
      <li>
        <a href="/products/vue-book">Vue book</a>
        - 3500円
      </li>
      <li>
        <a href="/products/angular-book">Angular book</a>
        - 3500円
      </li>
    </ul>
  </footer>
</article>

<style>
  :global(body) {
    margin: 0;
    background-color: #eee;
    padding: 0;
  }

  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0 auto;
    padding: 0 15px;
    background-color: #fff;
    width: 100%;
    max-width: 800px;
    height: 50px;
  }


</style>
