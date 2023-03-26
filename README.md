<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title style="font-size: 144px; font-weight: bold;">You're under control</title>
  <link href="https://fonts.googleapis.com/css?family=Montserrat&display=swap" rel="stylesheet">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <style>
    body {
      font-family: 'Montserrat', sans-serif;
      text-align: center;
    }
    h1 {
      color: white;
      font-weight: bold;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 48px;
      font-weight: bolder;
    }
  </style>
</head>
<body>
  <h1>You're under control</h1>
  <script>
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    const geometry = new THREE.SphereGeometry(25, 64, 64);
    const particles = new THREE.Points(geometry);
    scene.add(particles);

    camera.position.z = 10;

    function animate() {
      requestAnimationFrame(animate);
      particles.rotation.y += 0.001;
      const phi = particles.geometry.attributes.position.array[1];
      const color = new THREE.Color();
      color.setHSL((phi + 1) / 2, 1.0, 0.5);
      particles.material.color = color;
      renderer.render(scene, camera);
    }
    animate();

    particles.position.x = 0;
    particles.position.y = 0;
    particles.position.z = 0;

    function onMouseMove(event) {
      particles.position.x = (event.clientX / window.innerWidth) * 2 - 1;
      particles.position.y = -(event.clientY / window.innerHeight) * 2 + 1;
    }

    function onMouseUp(event) {
      particles.position.x = 0;
      particles.position.y = 0;
      particles.position.z = 0;
    }

    document.addEventListener('mousemove', onMouseMove, false);
    document.addEventListener('mouseup', onMouseUp, false);
  </script>
</body>
</html>
