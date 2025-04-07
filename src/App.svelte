<script>
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

  let cart = [];

  const addToCart = (productId) => {
    cart = [...cart, productId];
    // cart.push(productId)
  };

  let sliderCenterIndex = 0;
  let sliderLeftIndex = product.images.length - 1;
  let sliderRightIndex = 1;

  function sliderMoveLeft() {
    sliderCenterIndex = (sliderCenterIndex - 1 + product.images.length) % product.images.length;
    sliderLeftIndex = (sliderCenterIndex - 1 + product.images.length) % product.images.length;
    sliderRightIndex = (sliderCenterIndex + 1) % product.images.length;
  }

  function sliderMoveRight() {
    sliderCenterIndex = (sliderCenterIndex + 1) % product.images.length;
    sliderLeftIndex = (sliderCenterIndex - 1 + product.images.length) % product.images.length;
    sliderRightIndex = (sliderCenterIndex + 1) % product.images.length;
  }
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

  .image-container img {
    width: 100%;
  }

  .slider {
    position: relative;
    width: 80%;
    margin: 0 10%;
  }

  .slider-item {
    width: 100%;
  }

  .slider-item.left {
    position: absolute;
    top: 0;
    right: 100%;
  }

  .slider-item.right {
    position: absolute;
    top: 0;
    left: 100%;
  }

  .slider-left-button {
    position: absolute;
    top: 50%;
    left: -30px;
    transform: translateY(-50%);
    cursor: pointer;
    z-index: 10;
  }

  .slider-right-button {
    position: absolute;
    top: 50%;
    right: -30px;
    transform: translateY(-50%);
    cursor: pointer;
    z-index: 10;
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
      <div class="slider">
        <img
          src={product.images[sliderLeftIndex]}
          alt="左側のスライダー"
          class="slider-item left"
        />
        <img
          src={product.images[sliderCenterIndex]}
          alt="中央のスライダー"
          class="slider-item center"
        />
        <img
          src={product.images[sliderRightIndex]}
          alt="右側のスライダー"
          class="slider-item right"
        />
        <button on:click={sliderMoveLeft} class="slider-left-button">←</button>
        <button on:click={sliderMoveRight} class="slider-right-button">→</button>
      </div>
    </div>

    <div>
      <h2>{product.name}</h2>
      <dl>
        <dt>価格</dt>
        <dd>{product.price}</dd>
      </dl>
      <div>
        {#if !cart.includes('svelte-book')}
          <button on:click={() => addToCart('svelte-book')}>カートに入れる</button>
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
        <!-- {#if !cart.includes(product.id)}
          <button on:click={() => addToCart(product.id)}>カートに入れる</button>
        {:else}
          <button disabled>カート追加済み</button>
        {/if} -->
      </li>
    {/each}
  </footer>
</article>
