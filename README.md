<h1 id="typing"></h1>

<script>
  const text = "Hello, welcome!";
  let index = 0;
  
  function type() {
    if (index < text.length) {
      document.getElementById("typing").textContent += text.charAt(index);
      index++;
      setTimeout(type, 100); // delay between letters
    }
  }
  
  type();
</script>
