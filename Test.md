<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Espada 3D</title>
  <style>
    body { margin: 0; overflow: hidden; }
    canvas { display: block; }
  </style>
</head>
<body>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

<script>
  // Cena
  const scene = new THREE.Scene();

  // Câmera
  const camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
  camera.position.z = 5;

  // Renderizador
  const renderer = new THREE.WebGLRenderer();
  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);

  // Luz
  const light = new THREE.PointLight(0xffffff, 1);
  light.position.set(5, 5, 5);
  scene.add(light);

  // Material
  const material = new THREE.MeshStandardMaterial({ color: 0xaaaaaa });

  // Lâmina da espada
  const bladeGeometry = new THREE.BoxGeometry(0.3, 3, 0.1);
  const blade = new THREE.Mesh(bladeGeometry, material);
  blade.position.y = 1.5;

  // Cabo
  const handleGeometry = new THREE.CylinderGeometry(0.1, 0.1, 1, 32);
  const handle = new THREE.Mesh(handleGeometry, new THREE.MeshStandardMaterial({ color: 0x654321 }));
  handle.position.y = -0.5;

  // Guarda (proteção da mão)
  const guardGeometry = new THREE.BoxGeometry(1, 0.2, 0.2);
  const guard = new THREE.Mesh(guardGeometry, new THREE.MeshStandardMaterial({ color: 0x333333 }));
  guard.position.y = 0;

  // Grupo espada
  const sword = new THREE.Group();
  sword.add(blade);
  sword.add(handle);
  sword.add(guard);

  scene.add(sword);

  // Animação
  function animate() {
    requestAnimationFrame(animate);

    sword.rotation.y += 0.01;
    sword.rotation.x += 0.005;

    renderer.render(scene, camera);
  }

  animate();

  // Ajuste responsivo
  window.addEventListener('resize', () => {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
  });
</script>

</body>
</html>
