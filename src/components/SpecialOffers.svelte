
<script>
  const offers = [
    { id: 'QS-1209', building: 'Building QS', rooms: 2, area: 75 },
    { id: 'CH-907', building: 'Building CH', rooms: 3, area: 90 },
    { id: 'YD-708', building: 'Building YD', rooms: 2, area: 80 },
    { id: 'TR-609', building: 'Building TR', rooms: 1, area: 55 }
  ];
</script>

<section class="special-offers">
  <div class="offers-inner">
    <h2 class="section-title">Special offers</h2>

    <div class="offers-grid">
      {#each offers as offer (offer.id)}
        <article class="offer-card">
          <div class="offer-image">
            <span class="offer-label">Special offer</span>
          </div>

          <div class="offer-info">
            <p class="building">{offer.building}</p>
            <h3>{offer.rooms} bedrooms · {offer.area} m²</h3>
          </div>
        </article>
      {/each}
    </div>
  </div>
</section>
