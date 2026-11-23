
<script>
  import qsImage from '../../design/special-offers/assets/offer-QS-1209.png';
  import chImage from '../../design/special-offers/assets/offer-CH-907.png';
  import ydImage from '../../design/special-offers/assets/offer-YD-708.png';
  import trImage from '../../design/special-offers/assets/offer-TR-609.png';

  export let flats = [];
  export let prices = {};
  export let onBook = () => {};

  const offers = [
    { id: 'QS-1209', image: qsImage },
    { id: 'CH-907', image: chImage },
    { id: 'YD-708', image: ydImage },
    { id: 'TR-609', image: trImage }
  ];

  $: cards = offers
    .map((offer) => {
      const flat = flats.find((item) => item.id === offer.id);

      if (!flat) return null;

      const originalPrice = prices[offer.id] ?? flat.price;

      return {
        ...offer,
        flat,
        originalPrice,
        offerPrice: Math.round(originalPrice * 0.93 / 100) * 100
      };
    })
    .filter(Boolean);

  const formatPrice = (price) =>
    new Intl.NumberFormat('en-GB', {
      style: 'currency',
      currency: 'GBP',
      maximumFractionDigits: 0
    }).format(price);
</script>

<section class="special-offers">
  <div class="offers-inner">
    <h2 class="section-title">Special offers</h2>

    <div class="offers-grid">
      {#each cards as card (card.id)}
        <article class="offer-card">
          <div class="offer-image">
            <img src={card.image} alt={`${card.flat.building} apartment`} />
            <span class="offer-label">Special offer</span>
          </div>

          <div class="offer-info">
            <p class="building">{card.flat.building}</p>
            <h3>{card.flat.rooms} bedrooms · {card.flat.area} m²</h3>

            <div class="price-row">
              <span class="offer-price">{formatPrice(card.offerPrice)}</span>
              <span class="old-price">{formatPrice(card.originalPrice)}</span>
            </div>

            <p class="offer-expiry">Offer valid until 31 December 2026</p>

            <button class="book-button" on:click={onBook}>
              Book a viewing
            </button>
          </div>
        </article>
      {/each}
    </div>
  </div>
</section>
