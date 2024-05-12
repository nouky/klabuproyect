<script>
  let pos = 1;
  let kwadrantpath = `/img/kwadrant-${pos}.svg`;
</script>

<div id="kwadrant-container" class="row position-relative mb-3">
  <img id="kwadrant" src={kwadrantpath} alt="Quadrant" />
  <img
    id="wijzer"
    class="position-absolute"
    src="/img/wijzer.svg"
    alt="Pointer"
  />
</div>
