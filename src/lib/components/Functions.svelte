<script context="module">
  export function noteType(type) {
    let noteType = [
      {
        type: "B",
        class: "bass",
        label: "Bass",
        range: [{ type: "max", position: 31, note: "G2" }],
      },
      {
        type: "A",
        class: "accompaniment",
        label: "Accompaniment",
        range: null,
      },
      {
        type: "M",
        class: "melody",
        label: "Melody",
        range: [{ type: "min", position: 72, note: "C6" }],
      },
    ];

    noteType = noteType.filter((n) => n.type === type);

    return noteType[0];
  }
</script>
