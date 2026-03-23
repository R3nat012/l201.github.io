---
layout: null
---
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

<img id="slide-img" src="" />
<iframe id="sheet"
  src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSzna1dS_hUHyWukdkuJSsKEjzKcnJXHOy1Mrtria5zvRIqsGwjfXRUB-4gcz9tLv3VkGBOy3jNjjVZ/pubhtml?gid=1370414161&single=true">
</iframe>

<script>
  const PRESENTATION_ID = "1_s2ba0wRyUjUt-MfHUoQ9d5WjV7eT_vr9qKcnAahAjg";
  const TOTAL_SLIDES = 22; // change to your actual number of slides
  const SLIDE_DURATION = 3000;  // ms per slide
  const SHEET_DURATION = 5000;  // ms for sheet

  const img = document.getElementById("slide-img");
  const sheet = document.getElementById("sheet");

  function getSlideUrl(slideNumber) {
    return `https://docs.google.com/presentation/d/${PRESENTATION_ID}/export/png?pageid=p${slideNumber === 1 ? "" : slideNumber}`;
  }

  const FIRST_OF_LAST5 = TOTAL_SLIDES - 4;
  let currentSlide = FIRST_OF_LAST5;

  function showNextSlide() {
    img.style.display = "block";
    sheet.style.display = "none";
    img.src = getSlideUrl(currentSlide);

    currentSlide++;
    if (currentSlide > TOTAL_SLIDES) {
      currentSlide = 1;
      setTimeout(showSheet, SLIDE_DURATION); // after last slide, show sheet
    } else {
      setTimeout(showNextSlide, SLIDE_DURATION);
    }
  }

  function showSheet() {
    img.style.display = "none";
    sheet.style.display = "block";
    // force refresh
    sheet.src = sheet.src.split("&t=")[0] + "&t=" + Date.now();
    setTimeout(() => { currentSlide = 1; showNextSlide(); }, SHEET_DURATION);
  }

  // preload first slide then start
  img.src = getSlideUrl(1);
  img.onload = showNextSlide;
</script>
</body>
</html>
