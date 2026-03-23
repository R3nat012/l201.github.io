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

<img id="slide-img" src="l201.github.io/Componentes_l201.jpg" />
<iframe id="sheet"
  src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSzna1dS_hUHyWukdkuJSsKEjzKcnJXHOy1Mrtria5zvRIqsGwjfXRUB-4gcz9tLv3VkGBOy3jNjjVZ/pubhtml?gid=1370414161&single=true">
</iframe>

<script>
  const SLIDES        = ["l201.github.io/Componentes_l201.jpg","l201.github.io/Impresiones_l201.jpg","l201.github.io/robots_l201.jpg"];
  const SLIDE_DURATION = 3000; // ms per slide
  const SHEET_DURATION = 5000; // ms for sheet

  const img   = document.getElementById("slide-img");
  const sheet = document.getElementById("sheet");
  let current = 0;

  function showNextSlide() {
    sheet.style.display = "none";
    img.style.display   = "block";
    img.src = SLIDES[current];
    current++;

    if (current >= SLIDES.length) {
      current = 0;
      setTimeout(showSheet, SLIDE_DURATION);
    } else {
      setTimeout(showNextSlide, SLIDE_DURATION);
    }
  }

  function showSheet() {
    img.style.display   = "none";
    sheet.style.display = "block";
    sheet.src = sheet.src.split("&t=")[0] + "&t=" + Date.now();
    setTimeout(showNextSlide, SHEET_DURATION);
  }

  showNextSlide();
</script>
</body>
</html>
