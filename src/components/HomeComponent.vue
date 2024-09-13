<template>
    <div>
      <!-- Navbar -->
      <nav class="navbar navbar-expand-lg navbar-light bg-light fixed-top">
        <div class="container">
          <!-- Logo -->
          <a class="navbar-brand" href="#">
            <img src="../assets/logo-3.png" alt="Logo" width="100" height="100"> <!-- Logo de la veterinaria -->
          </a>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
            aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav ms-auto">
              <li class="nav-item">
                <a class="nav-link" href="#about">Sobre Nosotros</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#why-choose-us">Por qué Elegirnos</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#services">Servicios</a>
              </li>
              <li class="nav-item">
                <router-link class="nav-link" to="/citas">Agendar Cita</router-link> 
              </li>
            </ul>
          </div>
        </div>
      </nav>
      <br>
      <!-- Sección: Sobre Nosotros -->
      <section id="about" class="py-5">
        <div class="container">
          <h2 class="text-center mb-4">Sobre Nosotros</h2>
          <div class="row">
            <div class="col-md-6">
              <p>
                En <strong>CareVet</strong>, nos dedicamos a cuidar a tus mascotas como si fueran parte de nuestra familia. 
                Fundada en 2005, nuestra clínica ha crecido con la misión de brindar atención médica de calidad para todas 
                las mascotas. Contamos con un equipo de veterinarios expertos y un personal comprometido, ofreciendo 
                un ambiente cálido y profesional para que tus animales se sientan seguros y amados.
              </p>
              <p>
                Nos especializamos en cuidados preventivos, diagnósticos avanzados y tratamientos médicos y quirúrgicos 
                para todas las especies. Creemos que la salud de tu mascota es nuestra prioridad, y nos esforzamos por 
                ofrecer la mejor atención posible.
              </p>
            </div>
            <div class="col-md-6">
              <img src="../assets/photo-9.jpg" class="img-fluid" alt="Imagen sobre nosotros">
            </div>
          </div>
        </div>
      </section>
  
      <!-- Sección: Por qué Elegirnos (con carousel) -->
      <section id="why-choose-us" class="py-5 bg-light">
        <div class="container">
          <h2 class="text-center mb-4">Por qué Elegirnos</h2>
          <div class="row">
            <!-- Columna con texto -->
            <div class="col-md-6">
              <p>
                En <strong>CareVet</strong>, nos destacamos por nuestro compromiso con el bienestar de tu mascota. 
                Estas son algunas razones para elegirnos:
              </p>
              <ul>
                <li><strong>Atención 24/7:</strong> Estamos disponibles para emergencias todo el día, todos los días.</li>
                <li><strong>Veterinarios Especializados:</strong> Contamos con expertos en cirugía, odontología, dermatología y más.</li>
                <li><strong>Equipamiento Moderno:</strong> Utilizamos tecnología avanzada para diagnósticos y tratamientos precisos.</li>
                <li><strong>Enfoque Personalizado:</strong> Adaptamos nuestro cuidado a las necesidades específicas de cada mascota.</li>
              </ul>
            </div>
            <!-- Columna con carousel -->
            <div class="col-md-6">
              <div id="carouselExample" class="carousel slide" data-bs-ride="carousel">
                <div class="carousel-inner">
                  <div class="carousel-item active">
                    <img src="../assets/photo-4.jpeg" class="d-block w-100" alt="Slide 1">
                  </div>
                  <div class="carousel-item">
                    <img src="../assets/photo-5.jpeg" class="d-block w-100" alt="Slide 2">
                  </div>
                  <div class="carousel-item">
                    <img src="../assets/photo-6.jpeg" class="d-block w-100" alt="Slide 3">
                  </div>
                </div>
                <button class="carousel-control-prev" type="button" data-bs-target="#carouselExample" data-bs-slide="prev">
                  <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                  <span class="visually-hidden">Previous</span>
                </button>
                <button class="carousel-control-next" type="button" data-bs-target="#carouselExample" data-bs-slide="next">
                  <span class="carousel-control-next-icon" aria-hidden="true"></span>
                  <span class="visually-hidden">Next</span>
                </button>
              </div>
            </div>
          </div>
        </div>
      </section>
  
      <!-- Sección: Servicios -->
      <section id="services" class="py-5">
        <div class="container">
          <h2 class="text-center mb-4">Nuestros Servicios</h2>
          <div class="row">
            <div class="col-md-4">
              <img src="../assets/photo-10.jpeg" class="img-fluid mb-3" alt="Chequeos Generales">
              <h4>Chequeos Generales</h4>
              <p>Realizamos chequeos de rutina para asegurar que tu mascota se mantenga sana y feliz. Las visitas regulares nos ayudan a detectar cualquier problema antes de que se agrave.</p>
            </div>
            <div class="col-md-4">
              <img src="../assets/photo-8.jpeg" class="img-fluid mb-3" alt="Cirugía">
              <h4>Cirugía</h4>
              <p>Nuestro equipo especializado realiza desde cirugías menores hasta procedimientos complejos, garantizando el bienestar de tu mascota durante todo el proceso.</p>
            </div>
            <div class="col-md-4">
              <img src="../assets/photo-9.jpg" class="img-fluid mb-3" alt="Vacunación y Desparasitación">
              <h4>Vacunación y Desparasitación</h4>
              <p>Protege a tu mascota de enfermedades comunes y graves mediante nuestro completo programa de vacunación y desparasitación.</p>
            </div>
          </div>
        </div>
      </section>
  
      <!-- Sección: Redes Sociales -->
      <section class="py-5 bg-light">
        <div class="container text-center">
          <h4>Síguenos en nuestras redes sociales</h4>
          <div class="d-flex justify-content-center mt-4">
            <!-- Instagram -->
            <a href="https://www.instagram.com/" class="me-3" target="_blank">
              <img src="https://img.icons8.com/ios-glyphs/30/000000/instagram-new.png" alt="Instagram" />
            </a>
            <!-- Gmail -->
            <a href="mailto:jcochojilh@miumg.edu.gt" class="me-3">
              <img src="https://img.icons8.com/ios-glyphs/30/000000/gmail.png" alt="Gmail" />
            </a>
            <!-- WhatsApp -->
            <a href="https://wa.me/+50247479132" target="_blank">
              <img src="https://img.icons8.com/ios-glyphs/30/000000/whatsapp.png" alt="WhatsApp" />
            </a>
          </div>
        </div>
      </section>
    </div>
  </template>
  
  <script>
  export default {
    name: 'HomePage',
  };
  </script>
  
  <style scoped>
  /* Añadir un poco de espaciado entre la barra de navegación y las secciones */
  section {
    margin-top: 80px;
  }
  
  .navbar {
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  }
  
  .carousel-inner img {
    height: 300px;
    object-fit: cover;
  }
  
  .img-fluid {
    border-radius: 10px;
  }
  
  /* Estilo para los íconos de redes sociales */
  a img {
    transition: transform 0.2s;
  }
  
  a img:hover {
    transform: scale(1.2);
  }
  </style>
  