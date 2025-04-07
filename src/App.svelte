<script>
  import Slider from './Slider.svelte';

  let product = {
    id: 'svelte-book',
    name: 'Svelte book',
    price: 3500,
    images: [
      'https://github.com/svelte-book/sample-app/raw/main/static/react-book-1.png',
      'https://github.com/svelte-book/sample-app/raw/main/static/react-book-2.png',
      'https://github.com/svelte-book/sample-app/raw/main/static/react-book-3.png',
    ],
  };

  let relatedProducts = [
    { id: 'react-book', name: 'React book', price: 3500 },
    { id: 'vue-book', name: 'Vue book', price: 3500 },
    { id: 'angular-book', name: 'Angular book', price: 3500 },
  ];

  let cart = $state([]);

  const addToCart = (productId) => {
    cart = [...cart, productId];
    // cart.push(productId)
  };
</script>

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

  .header-links {
    display: flex;
    gap: 10px;
    margin: 0;
    list-style: none;
    padding: 0;
  }

  .product {
    margin: 0 auto;
    background-color: #fff;
    padding: 15px;
    width: 100%;
    max-width: 800px;
  }

  .product-main {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
  }

  .image-container {
    width: 200px;
    max-width: 400px;
    overflow: hidden;
  }
</style>

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
      <Slider images={product.images} />
    </div>
    <div>
      <h2>{product.name}</h2>
      <dl>
        <dt>価格</dt>
        <dd>{product.price}</dd>
      </dl>
      <div>
        {#if !cart.includes('svelte-book')}
          <button onclick={() => addToCart('svelte-book')}>カートに入れる</button>
        {:else}
          <button disabled>カート追加済み</button>
        {/if}
      </div>
    </div>
  </div>

  <footer>
    <h3>関連商品</h3>
    {#each relatedProducts as product}
      <li>
        <a href="/products/{product.id}">{product.name}</a>
        - {product.price}円
      </li>
    {/each}
  </footer>
</article>
