<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Display</title>
  <style>
    body { margin: 0; overflow: hidden; background: #000; }
    #slide-img {
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 100%;
      object-fit: contain;
      display: none;
    }
    #sheet {
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 100%;
      border: none;
      display: none;
    }
  </style>
</head>
<body>

<img id="slide-img" />
<iframe id="sheet"
  src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSzna1dS_hUHyWukdkuJSsKEjzKcnJXHOy1Mrtria5zvRIqsGwjfXRUB-4gcz9tLv3VkGBOy3jNjjVZ/pubhtml?gid=1370414161&single=true">
</iframe>

<script>
  // ── CONFIG ──────────────────────────────────────────────
  const PRESENTATION_ID = "1_s2ba0wRyUjUt-MfHUoQ9d5WjV7eT_vr9qKcnAahAjg"; // from /d/THIS/edit
  const TOTAL_SLIDES    = 22;   // your total slide count
  const LAST_N_SLIDES   = 3;    // how many last slides to show
  const SLIDE_DURATION  = 3000; // ms per slide
  const SHEET_DURATION  = 5000; // ms for sheet
  // ────────────────────────────────────────────────────────

  const img   = document.getElementById("slide-img");
  const sheet = document.getElementById("sheet");

  const START_SLIDE = TOTAL_SLIDES - LAST_N_SLIDES + 1;
  let currentSlide  = START_SLIDE;

  function getSlideUrl(n) {
    // Google export trick: slide 1 has no number in the pageid
    const pageId = n === 1 ? "p" : `p${n}`;
    return `https://docs.google.com/presentation/d/${PRESENTATION_ID}/export/png?pageid=${pageId}&cachebust=${Date.now()}`;
  }

  function showNextSlide() {
    sheet.style.display = "none";
    img.style.display   = "block";
    img.src = getSlideUrl(currentSlide);

    const next = currentSlide;
    currentSlide++;

    if (currentSlide > TOTAL_SLIDES) {
      currentSlide = START_SLIDE;
      setTimeout(showSheet, SLIDE_DURATION);
    } else {
      setTimeout(showNextSlide, SLIDE_DURATION);
    }
  }

  function showSheet() {
    img.style.display   = "none";
    sheet.style.display = "block";
    sheet.src = sheet.src.split("&t=")[0] + "&t=" + Date.now();
    setTimeout(() => {
      currentSlide = START_SLIDE;
      showNextSlide();
    }, SHEET_DURATION);
  }

  // Kick off
  showNextSlide();
</script>
</body>
</html>
