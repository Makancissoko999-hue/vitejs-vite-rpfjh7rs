<script>
  let market = 'es';
  let activeCategory = 'Tous';
  let searchQuery = '';
  let cart = [];
  let showCart = false;
  let showSellerModal = false;
  let orderNotice = '';

  const products = [
    { id: 1, name: 'Sac tissé artisanal', category: 'Accessoires', market: 'ml', price: 12500, image: 'https://images.unsplash.com/photo-1548036328-c9fa89d128fa?auto=format&fit=crop&w=900&q=80', label: 'Artisanat' },
    { id: 2, name: 'Pochette en cuir', category: 'Accessoires', market: 'ml', price: 8500, image: 'https://images.unsplash.com/photo-1606760227091-3dd870d97f1d?auto=format&fit=crop&w=900&q=80', label: 'Sélection locale' },
    { id: 3, name: 'Chemise en coton', category: 'Vêtements', market: 'ml', price: 10000, image: 'https://images.unsplash.com/photo-1598033129183-c4f50c736f10?auto=format&fit=crop&w=900&q=80', label: 'Mode' },
    { id: 4, name: 'Bracelet artisanal', category: 'Bijoux', market: 'ml', price: 5000, image: 'https://images.unsplash.com/photo-1611652022419-a9419f74343d?auto=format&fit=crop&w=900&q=80', label: 'Fait main' },
    { id: 5, name: 'Sneakers urbaines', category: 'Chaussures', market: 'es', price: 49, image: 'https://images.unsplash.com/photo-1542291026-7eec264c27ff?auto=format&fit=crop&w=900&q=80', label: 'Tendance' },
    { id: 6, name: 'Sac de ville', category: 'Accessoires', market: 'es', price: 35, image: 'https://images.unsplash.com/photo-1584917865442-de89df76afd3?auto=format&fit=crop&w=900&q=80', label: 'Style quotidien' },
    { id: 7, name: 'T-shirt essentiel', category: 'Vêtements', market: 'es', price: 18, image: 'https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?auto=format&fit=crop&w=900&q=80', label: 'Indispensable' },
    { id: 8, name: 'Montre classique', category: 'Accessoires', market: 'es', price: 59, image: 'https://images.unsplash.com/photo-1523275335684-37898b6baf30?auto=format&fit=crop&w=900&q=80', label: 'Élégant' }
  ];

  $: visibleProducts = products.filter((product) =>
    product.market === market &&
    (activeCategory === 'Tous' || product.category === activeCategory) &&
    product.name.toLowerCase().includes(searchQuery.trim().toLowerCase())
  );
  $: categories = ['Tous', ...new Set(products.filter((p) => p.market === market).map((p) => p.category))];
  $: cartCount = cart.reduce((total, item) => total + item.quantity, 0);
  $: cartTotal = cart.reduce((total, item) => total + item.price * item.quantity, 0);

  function formatPrice(value) {
    return new Intl.NumberFormat(market === 'es' ? 'es-ES' : 'fr-FR', {
      style: 'currency',
      currency: market === 'es' ? 'EUR' : 'XOF',
      maximumFractionDigits: 0
    }).format(value);
  }

  function changeMarket(nextMarket) {
    if (market === nextMarket) return;
    market = nextMarket;
    activeCategory = 'Tous';
    searchQuery = '';
    cart = [];
    showCart = false;
    orderNotice = '';
  }

  function addToCart(product) {
    const existing = cart.find((item) => item.id === product.id);
    cart = existing
      ? cart.map((item) => item.id === product.id ? { ...item, quantity: item.quantity + 1 } : item)
      : [...cart, { ...product, quantity: 1 }];
    orderNotice = '';
  }

  function removeFromCart(productId) {
    cart = cart.filter((item) => item.id !== productId);
  }

  function placeDemoOrder() {
    if (!cart.length) return;
    showCart = false;
    orderNotice = 'Simulation terminée : aucune commande réelle ni aucun paiement n’a été envoyé. Le panier de démonstration a été réinitialisé.';
    cart = [];
  }
</script>

<svelte:head>
  <title>MAKCISS CAPITAL — Le commerce, plus simple</title>
  <meta name="description" content="Prototype de marketplace locale pour le Mali et l’Espagne. Découvrez des produits, explorez les boutiques et préparez vos commandes." />
  <meta name="theme-color" content="#0b1714" />
</svelte:head>

<div class="demo-banner">
  <span class="demo-dot"></span>
  PROTOTYPE DE DÉMONSTRATION · PAS DE PAIEMENT RÉEL
</div>

<header class="site-header">
  <a class="brand" href="#accueil" aria-label="MAKCISS CAPITAL accueil">
    <span class="brand-mark">M</span>
    <span class="brand-name">MAKCISS <small>CAPITAL</small></span>
  </a>

  <nav class="desktop-nav" aria-label="Navigation principale">
    <a href="#catalogue">Découvrir</a>
    <a href="#comment-ca-marche">Comment ça marche</a>
    <button class="nav-link" onclick={() => showSellerModal = true}>Vendre avec nous</button>
  </nav>

  <div class="header-actions">
    <div class="market-switch" aria-label="Choisir le marché">
      <button class:chosen={market === 'es'} aria-pressed={market === 'es'} onclick={() => changeMarket('es')}>🇪🇸 Espagne</button>
      <button class:chosen={market === 'ml'} aria-pressed={market === 'ml'} onclick={() => changeMarket('ml')}>🇲🇱 Mali</button>
    </div>
    <button class="cart-button" onclick={() => showCart = true} aria-label="Ouvrir le panier">
      <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M3 4h2l2.2 10.2a2 2 0 0 0 2 1.6h8.9a2 2 0 0 0 1.9-1.4L22 8H6"/><circle cx="10" cy="20" r="1.2"/><circle cx="18" cy="20" r="1.2"/></svg>
      <span>Panier</span><b>{cartCount}</b>
    </button>
  </div>
</header>

<main>
  <section class="hero" id="accueil">
    <div class="hero-copy">
      <div class="eyebrow"><span></span> LE COMMERCE, PLUS PROCHE DE VOUS</div>
      <h1>Les bonnes trouvailles.<br /><em>Les bonnes rencontres.</em></h1>
      <p>Découvrez des produits sélectionnés auprès de vendeurs locaux. Une expérience pensée pour rapprocher les boutiques et leurs clients.</p>
      <div class="hero-actions">
        <a class="button button-primary" href="#catalogue">Explorer les produits <span>↗</span></a>
        <button class="button button-quiet" onclick={() => showSellerModal = true}>Je suis commerçant</button>
      </div>
      <div class="hero-proof">
        <span class="proof-icon">✓</span>
        <span><strong>Des vendeurs à découvrir</strong><small>La confiance se construit commande après commande.</small></span>
      </div>
    </div>
    <div class="hero-art">
      <div class="hero-image"></div>
      <div class="floating-note note-top"><span class="note-icon">✳</span><span><strong>La découverte locale</strong><small>Des produits, des histoires.</small></span></div>
      <div class="floating-note note-bottom"><span class="note-stars">★★★★★</span><strong>Un commerce plus humain</strong><small>Un projet en construction</small></div>
      <div class="hero-stamp">M<br /><small>MC</small></div>
    </div>
  </section>

  <section class="market-strip" aria-label="Marché sélectionné">
    <div><span class="strip-symbol">◎</span><span><small>VOUS EXPLOREZ</small><strong>{market === 'es' ? 'Le marché espagnol' : 'Le marché malien'}</strong></span></div>
    <div class="strip-divider"></div>
    <p>{market === 'es' ? 'Prix indicatifs en euros · Catalogue de démonstration' : 'Prix indicatifs en FCFA · Catalogue de démonstration'}</p>
    <span class="strip-location">{market === 'es' ? 'ES / EUR' : 'ML / XOF'}</span>
  </section>

  {#if orderNotice}
    <div class="notice" role="status"><span>ℹ</span><p>{orderNotice}</p><button aria-label="Fermer le message" onclick={() => orderNotice = ''}>×</button></div>
  {/if}

  <section class="catalogue section-wrap" id="catalogue">
    <div class="section-heading">
      <div><div class="eyebrow">À DÉCOUVRIR</div><h2>Le marché <em>du moment.</em></h2></div>
      <p>Une première sélection d’exemples pour tester la navigation. Les vendeurs et les stocks réels seront ajoutés après validation.</p>
    </div>

    <div class="catalogue-tools">
      <div class="category-list" aria-label="Filtrer par catégorie">
        {#each categories as category}
          <button class:active={activeCategory === category} onclick={() => activeCategory = category}>{category}</button>
        {/each}
      </div>
      <label class="search-box">
        <svg viewBox="0 0 24 24" aria-hidden="true"><circle cx="10.8" cy="10.8" r="6.8"/><path d="m16 16 5 5"/></svg>
        <input bind:value={searchQuery} placeholder="Rechercher un produit" aria-label="Rechercher un produit" />
      </label>
    </div>

    {#if visibleProducts.length}
      <div class="product-grid">
        {#each visibleProducts as product}
          <article class="product-card">
            <div class="product-image-wrap">
              <img src={product.image} alt={product.name} loading="lazy" />
              <span class="product-label">{product.label}</span>
              <button class="quick-add" aria-label={'Ajouter ' + product.name + ' au panier'} onclick={() => addToCart(product)}>+</button>
            </div>
            <div class="product-meta"><span>{product.category}</span><span class="market-code">{market === 'es' ? 'ES' : 'ML'}</span></div>
            <h3>{product.name}</h3>
            <div class="product-bottom"><strong>{formatPrice(product.price)}</strong><button onclick={() => addToCart(product)}>Ajouter au panier <span>↗</span></button></div>
          </article>
        {/each}
      </div>
    {:else}
      <div class="empty-state"><span>⌕</span><h3>Aucun produit trouvé</h3><p>Essayez un autre mot ou une autre catégorie.</p><button class="button button-primary" onclick={() => { searchQuery = ''; activeCategory = 'Tous'; }}>Réinitialiser les filtres</button></div>
    {/if}
    <p class="catalogue-footnote">Images et produits illustratifs. Aucune disponibilité commerciale n’est garantie dans ce prototype.</p>
  </section>

  <section class="how-section" id="comment-ca-marche">
    <div class="section-wrap">
      <div class="section-heading">
        <div><div class="eyebrow">SIMPLE, ÉTAPE PAR ÉTAPE</div><h2>Le commerce, <em>en confiance.</em></h2></div>
        <p>Le parcours cible de MAKCISS CAPITAL, avant l’activation des services réels.</p>
      </div>
      <div class="steps-grid">
        <article class="step-card"><span class="step-number">01</span><span class="step-icon">⌕</span><h3>Découvrez</h3><p>Parcourez les produits et trouvez une boutique qui vous correspond.</p></article>
        <article class="step-card"><span class="step-number">02</span><span class="step-icon">＋</span><h3>Commandez</h3><p>Ajoutez vos articles au panier et vérifiez les détails de votre commande.</p></article>
        <article class="step-card"><span class="step-number">03</span><span class="step-icon">↗</span><h3>Suivez</h3><p>Dans la future version, les étapes de commande et de livraison seront visibles.</p></article>
      </div>
    </div>
  </section>

  <section class="seller-cta section-wrap">
    <div class="seller-cta-copy"><div class="eyebrow">VOUS ÊTES COMMERÇANT ?</div><h2>Votre boutique mérite<br /><em>d’être découverte.</em></h2><p>Nous préparons un espace vendeur pour publier les produits et gérer les commandes.</p><button class="button button-light" onclick={() => showSellerModal = true}>Découvrir l’espace vendeur <span>↗</span></button></div>
    <div class="seller-cta-mark">M<span>✳</span></div>
  </section>
</main>

<footer class="site-footer">
  <a class="brand brand-footer" href="#accueil"><span class="brand-mark">M</span><span class="brand-name">MAKCISS <small>CAPITAL</small></span></a>
  <p>Construire un commerce plus accessible, une étape à la fois.</p>
  <span>© 2026 MAKCISS CAPITAL · Prototype</span>
</footer>

{#if showCart}
  <div class="overlay" role="presentation" onclick={(event) => { if (event.target === event.currentTarget) showCart = false; }}>
    <section class="side-panel" role="dialog" aria-modal="true" aria-labelledby="cart-title">
      <div class="panel-header"><div><small>VOTRE SÉLECTION</small><h2 id="cart-title">Mon panier <em>({cartCount})</em></h2></div><button class="close-button" aria-label="Fermer le panier" onclick={() => showCart = false}>×</button></div>
      {#if cart.length}
        <div class="cart-items">
          {#each cart as item}
            <article class="cart-item"><img src={item.image} alt="" /><div class="cart-item-info"><strong>{item.name}</strong><small>Quantité : {item.quantity}</small><b>{formatPrice(item.price * item.quantity)}</b></div><button aria-label={'Retirer ' + item.name} onclick={() => removeFromCart(item.id)}>×</button></article>
          {/each}
        </div>
        <div class="cart-summary"><div><span>Sous-total indicatif</span><strong>{formatPrice(cartTotal)}</strong></div><p>La livraison et les taxes ne sont pas calculées dans cette démonstration.</p><button class="button button-primary full-button" onclick={placeDemoOrder}>Tester le parcours de commande</button><small class="demo-warning">Aucun paiement ne sera demandé ni effectué.</small></div>
      {:else}
        <div class="cart-empty"><span>＋</span><h3>Votre panier est vide</h3><p>Ajoutez un produit pour tester le parcours.</p><button class="button button-primary" onclick={() => showCart = false}>Continuer la découverte</button></div>
      {/if}
    </section>
  </div>
{/if}

{#if showSellerModal}
  <div class="overlay" role="presentation" onclick={(event) => { if (event.target === event.currentTarget) showSellerModal = false; }}>
    <section class="dialog-panel" role="dialog" aria-modal="true" aria-labelledby="seller-title">
      <button class="close-button dialog-close" aria-label="Fermer" onclick={() => showSellerModal = false}>×</button>
      <span class="dialog-icon">✳</span><div class="eyebrow">ESPACE VENDEUR</div><h2 id="seller-title">Bientôt, votre boutique.</h2><p>L’inscription vendeur n’est pas encore connectée. La prochaine étape sera de vérifier l’identité des vendeurs, leurs coordonnées et leurs produits avant de publier leur boutique.</p><button class="button button-primary full-button" onclick={() => showSellerModal = false}>J’ai compris</button><small class="demo-warning">Aucune donnée n’est envoyée ni enregistrée.</small>
    </section>
  </div>
{/if}
