<style>
  :global(body) {
    font-family: 'Poppins', sans-serif;
    background: linear-gradient(135deg, #2a2a2a, #1a1a1a); /* Darker, professional gradient */
    color: #e0e0e0;
    margin: 0;
    padding: 0;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  /* Animaciones para la tarjeta de bienvenida */
        @keyframes fadeInTitle {
            0% { opacity: 0; transform: translateY(-30px); }
            100% { opacity: 1; transform: translateY(0); }
        }

        @keyframes slideInText {
            0% { opacity: 0; transform: translateY(20px); }
            100% { opacity: 1; transform: translateY(0); }
        }

        @keyframes fadeInCard {
            0% { opacity: 0; transform: scale(0.9); }
            100% { opacity: 1; transform: scale(1); }
        }

        .welcome-container {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-grow: 1; /* Permite que el contenedor de bienvenida ocupe el espacio disponible */
            width: 100%;
            padding: 20px;
        }

        .welcome-card {
            background: #333333;
            border-radius: 15px;
            padding: 40px;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.5);
            width: 100%;
            max-width: 600px;
            text-align: center;
            border: 1px solid rgba(0, 188, 212, 0.4);
            animation: fadeInCard 1s ease-out forwards;
            animation-delay: 0.5s; /* Retrasa la animación de la tarjeta */
            opacity: 0; /* Asegura que la tarjeta esté oculta al inicio */
        }

        .welcome-button {
            display: inline-block;
            padding: 15px 35px;
            background: #00bcd4;
            color: white;
            text-decoration: none;
            border: none;
            border-radius: 10px;
            font-size: 1.1em;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease, box-shadow 0.3s ease;
            letter-spacing: 0.8px;
            box-shadow: 0 5px 15px rgba(0, 188, 212, 0.3);
            animation: slideInText 2s ease-out forwards;
            animation-delay: 0.6s;
        }

        .welcome-button:hover {
            background-color: #0097a7;
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(0, 188, 212, 0.5);
        }

        .welcome-button:active {
            transform: translateY(1px);
            box-shadow: 0 4px 8px rgba(0, 188, 212, 0.3);
        }

        /* Adaptación para pantallas pequeñas */
        @media (max-width: 768px) {
            .welcome-card {
                padding: 30px;
                margin: 0 15px;
            }

            h1 {
                font-size: 2.8em !important; /* Ajuste para móviles */
            }

            .welcome-card h2 {
                font-size: 1.8em !important;
            }

            .welcome-card p {
                font-size: 1em !important;
            }

            .welcome-button {
                padding: 12px 25px;
                font-size: 1em;
            }
        }

        @media (max-width: 480px) {
            h1 {
                font-size: 2.2em !important;
            }
            .welcome-card h2 {
                font-size: 1.5em !important;
            }
        }
        .container{
          display: block;
          text-align: center;
        }
</style>

<div class="container">
  <h1 style="
            font-family: 'Poppins', sans-serif;
            font-size: 3.5em;
            font-weight: 700;
            color: #00bcd4;
            text-shadow: 0 5px 10px rgba(0, 188, 212, 0.4);
            animation: fadeInTitle 1.5s ease-in-out forwards;
            letter-spacing: 2px;
            margin-top: 0;
        ">
            ¡Bienvenido a PLANIFICAME!
        </h1>

        <main class="welcome-container">
        <div class="welcome-card">
            <h2 style="
                font-size: 2.2em;
                color: #e0e0e0;
                margin-bottom: 20px;
                text-align: center;
                animation: slideInText 1.5s ease-out forwards;
            ">
                Descubre el poder de la inteligencia artificial.
            </h2>
            <p style="
                font-size: 1.1em;
                line-height: 1.7;
                color: #aaaaaa;
                text-align: center;
                margin-bottom: 45px;
                animation: slideInText 1.8s ease-out forwards;
                animation-delay: 0.3s;
            ">
                Estamos aquí para ayudarte a descubrir tus areas de mejora en el ambito profesional, consulta que cursos 
                puedes tomar para capacitarte.
                <br>
                <a href="/chat" class="welcome-button">
                Comenzar
                </a>
            </p>
        </div>
    </main>
</div>
