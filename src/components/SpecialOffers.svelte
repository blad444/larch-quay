
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

<style>
  .special-offers {
    padding: 160px 32px;
    background: #eeecea;
    color: #333231;
  }

  .offers-inner {
    max-width: 1376px;
    margin: 0 auto;
  }

  .section-title {
    margin: 0 0 64px;
    font-family: 'Newsreader', Georgia, serif;
    font-size: 64px;
    font-weight: 400;
    line-height: 1.1;
  }

  .offers-grid {
    display: grid;
    grid-template-columns: repeat(4, minmax(0, 1fr));
    gap: 24px;
  }

  .offer-card {
    min-width: 0;
  }

  .offer-image {
    position: relative;
    aspect-ratio: 4 / 5;
    overflow: hidden;
  }

  .offer-image img {
    width: 100%;
    height: 100%;
    display: block;
    object-fit: cover;
  }

  .offer-label {
    position: absolute;
    top: 16px;
    left: 16px;
    padding: 8px 12px;
    background: #eeecea;
    font-size: 12px;
  }

  .offer-info {
    padding-top: 20px;
  }

  .building,
  .offer-expiry {
    color: #6b6763;
    font-size: 14px;
  }

  .building {
    margin: 0 0 8px;
  }

  .offer-info h3 {
    margin: 0 0 16px;
    font-family: 'Newsreader', Georgia, serif;
    font-size: 24px;
    font-weight: 400;
  }

  .price-row {
    display: flex;
    align-items: baseline;
    flex-wrap: wrap;
    gap: 12px;
  }

  .offer-price {
    font-size: 24px;
    font-weight: 500;
  }

  .old-price {
    color: #6b6763;
    font-size: 14px;
    text-decoration: line-through;
  }

  .offer-expiry {
    margin: 10px 0 20px;
  }

  .book-button {
    width: 100%;
    min-height: 48px;
    border: 1px solid #333231;
    background: transparent;
    color: #333231;
    font: inherit;
    cursor: pointer;
    transition: background 0.2s, color 0.2s;
  }

  .book-button:hover {
    background: #333231;
    color: #fff;
  }


  @media (max-width: 1024px) {
    .special-offers {
      padding: 120px 32px;
    }

    .section-title {
      margin-bottom: 48px;
      font-size: 48px;
    }

    .offers-grid {
      grid-template-columns: repeat(2, minmax(0, 1fr));
      row-gap: 48px;
    }
  }

  @media (max-width: 600px) {
    .special-offers {
      padding: 96px 0;
    }

    .section-title {
      margin: 0 16px 32px;
      font-size: 34px;
    }

    .offers-grid {
      display: flex;
      gap: 12px;
      overflow-x: auto;
      padding: 0 16px 12px;
      scroll-snap-type: x mandatory;
      scrollbar-width: none;
    }

    .offers-grid::-webkit-scrollbar {
      display: none;
    }

    .offer-card {
      flex: 0 0 280px;
      scroll-snap-align: start;
    }

    .offer-info h3 {
      font-size: 20px;
    }
  }

</style>
