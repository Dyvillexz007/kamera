<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ambil Foto</title>
<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #0f0f0f;
  color: #00ff99;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
video, canvas {
  width: 90%;
  max-width: 360px;
  border-radius: 12px;
  box-shadow: 0 0 15px #00ff99;
}
button {
  margin-top: 12px;
  padding: 10px 18px;
  font-size: 16px;
  border: none;
  border-radius: 8px;
  background: #00ff99;
  color: #000;
  font-weight: bold;
}
button:active {
  transform: scale(0.95);
}
</style>
</head>
<body>

<h3>📸 Ambil Foto</h3>

<video id="camera" autoplay playsinline></video>
<canvas id="result" style="display:none;"></canvas>

<button onclick="ambilFoto()">Ambil Foto</button>
<a id="download" style="display:none;">Simpan Foto</a>

<script>
const video = document.getElementById('camera');
const canvas = document.getElementById('result');
const downloadLink = document.getElementById('download');

navigator.mediaDevices.getUserMedia({
  video: { facingMode: "user" },
  audio: false
}).then(stream => {
  video.srcObject = stream;
}).catch(err => {
  alert("Kamera tidak bisa diakses");
});

function ambilFoto() {
  canvas.style.display = "block";
  canvas.width = video.videoWidth;
  canvas.height = video.videoHeight;

  const ctx = canvas.getContext("2d");
  ctx.drawImage(video, 0, 0);

  const dataURL = canvas.toDataURL("image/png");
  downloadLink.href = dataURL;
  downloadLink.download = "foto_kamera.png";
  downloadLink.textContent = "Simpan ke Galeri";
  downloadLink.style.display = "block";
}
</script>

</body>
</html>
