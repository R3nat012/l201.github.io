<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Display</title>
  <style>
    body { margin: 0; overflow: hidden; }
    iframe {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border: none;
    }
  </style>
</head>
<body>

<iframe id="slides" src="https://docs.google.com/presentation/d/e/2PACX-1vQx4X5UAD-X17lcE9aFRPdklw3W_VzyK1merA8aJmgXuqpPlyauDsMjObEC3bQ7geQtzR3WdfU6B6xg/embed?start=true&loop=true&delayms=2000"></iframe>

<iframe id="sheet" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSzna1dS_hUHyWukdkuJSsKEjzKcnJXHOy1Mrtria5zvRIqsGwjfXRUB-4gcz9tLv3VkGBOy3jNjjVZ/pubhtml?gid=1370414161&single=true" style="display:none;"></iframe>

<script>
  const slides = document.getElementById("slides");
  const sheet = document.getElementById("sheet");

  function showSlides() {
    slides.style.display = "block";
    sheet.style.display = "none";

    setTimeout(showSheet, 7000); // 7 segundos slides
  }

  function showSheet() {
    slides.style.display = "none";
    sheet.style.display = "block";

    // refresca el sheet para actualizar datos
    sheet.src = sheet.src;

    setTimeout(showSlides, 5000); // 5 segundos sheet
  }

  // iniciar
  showSlides();
</script>

</body>
</html>
