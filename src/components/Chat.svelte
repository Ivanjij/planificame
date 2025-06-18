<script>
  import Loader from "./Loader.svelte";
  let prompt = "";
  let result = "";
  let load = false;
  let isTextResponse = false;

  // Almacenar el historial de la conversación
  let conversation = [];

  const API_KEY = "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";
  const OPENAI_URL = "https://api.openai.com/v1/chat/completions";

  const apiSubmit = async (type) => {
    load = true;
    const userMessage = prompt;
    const messageRole = type === "text" ? "user" : "assistant";

    // Agregar el mensaje del usuario a la conversación
    conversation.push({ role: messageRole, content: userMessage });

    const body = {
      "model": "gpt-4o-mini",
      "messages": [
        {
          "role": "system",
          "content": "Actúa como un assistant de desarrollo profesional. Tu objetivo es proporcionar orientación general para mejorar habilidades profesionales, especialmente habilidades blandas (como comunicación, liderazgo, trabajo en equipo, gestión del tiempo, adaptabilidad, entre otras), y sugerir cursos y recursos útiles para diferentes áreas laborales comunes (como administración, tecnología, salud, educación, ingeniería, etc.). No solicites ni almacenes información personal, identificadores sensibles, o detalles específicos del usuario como nombre, ubicación, edad, género, datos laborales concretos, etc. Trabaja únicamente con descripciones generales o categorías profesionales cuando el usuario decida proporcionarlas. Si el usuario no especifica un área profesional, ofrece sugerencias generales que puedan aplicarse a diversos perfiles laborales. Asegúrate de que todas tus recomendaciones sean prácticas, éticas y aplicables sin comprometer la privacidad del usuario."
        },
        ...conversation,  // Mantener todo el historial de la conversación
      ],
      "temperature": 0.7
    };

    try {
      const response = await fetch(OPENAI_URL, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${API_KEY}`,
        },
        body: JSON.stringify(body),
      });

      const data = await response.json();
      
      // Mostrar respuesta de la API
      if (data.error) {
        result = `Error: ${data.error.message}`;
        conversation.push({ role: "assistant", content: result });
      } else {
        result = data.choices?.[0]?.message?.content.trim() || "No se recibio respuesta.";
        conversation.push({ role: "assistant", content: result });
      }
    } catch (error) {
      result = "Error al conectar con la API.";
      conversation.push({ role: "assistant", content: result });
    } finally {
      load = false;
      prompt = "";
    }
  };
</script>

<style>
  /* Import Google Fonts */
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');

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

  h2 {
    font-family: 'Poppins', sans-serif;
    font-size: 2.8em;
    font-weight: 700;
    color: #00bcd4;
    text-align: center;
    margin-bottom: 30px;
    text-shadow: 0 4px 8px rgba(0, 188, 212, 0.3);
    animation: fadeInTitle 1.2s ease-in-out forwards;
    letter-spacing: 1.5px;
  }

  @keyframes fadeInTitle {
    0% { opacity: 0; transform: translateY(-20px); }
    100% { opacity: 1; transform: translateY(0); }
  }

  /* Page Container that aligns to the right */
  .page-container {
    display: flex;
    justify-content: flex-end;
    align-items: flex-start;
    height: 100vh;
    width: 100%;
    padding: 20px;
  }

  /* Contenedor del chat */
  .container {
    background: #333333;
    border-radius: 15px;
    padding: 35px;
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.4);
    display: flex;
    flex-direction: column;
    gap: 25px;
    width: 100%;
    max-width: 700px;
    animation: slideIn 0.8s ease-out forwards;
    border: 1px solid rgba(0, 188, 212, 0.3);
    overflow-y: auto; /* Enable scrolling for conversation */
    max-height: 80vh; /* Set a max height for scrolling */
  }

  @keyframes slideIn {
    0% { opacity: 0; transform: translateY(20px); }
    100% { opacity: 1; transform: translateY(0); }
  }

  textarea {
    width: calc(100% - 24px);
    min-height: 150px;
    border: 1px solid #555555;
    border-radius: 10px;
    padding: 12px;
    font-size: 1.1em;
    resize: vertical;
    transition: border-color 0.3s ease, box-shadow 0.3s ease;
    background-color: #444444;
    color: #e0e0e0;
    caret-color: #00bcd4;
  }

  textarea::placeholder {
    color: #aaaaaa;
  }

  textarea:focus {
    border-color: #00bcd4;
    box-shadow: 0 0 10px rgba(0, 188, 212, 0.5);
    outline: none;
  }

  .button-group {
    display: flex;
    gap: 15px;
  }

  button {
    flex: 1;
    padding: 14px 20px;
    background: #00bcd4;
    color: white;
    border: none;
    border-radius: 10px;
    font-size: 1.05em;
    font-weight: 600;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease, box-shadow 0.3s ease;
    letter-spacing: 0.5px;
  }

  button:hover {
    background-color: #0097a7;
    transform: translateY(-2px);
    box-shadow: 0 8px 15px rgba(0, 188, 212, 0.4);
  }

  button:active {
    transform: translateY(1px);
    box-shadow: 0 4px 8px rgba(0, 188, 212, 0.3);
  }

  .response-container {
    display: flex;
    flex-direction: column-reverse; /* Responses stack on top of each other */
    margin-top: 15px;
    max-height: 400px;
    overflow-y: auto;
  }

  p, pre {
    background: #444444;
    padding: 20px;
    border-radius: 12px;
    white-space: pre-wrap;
    font-size: 1.05em;
    color: #e0e0e0;
    margin: 0;
    max-width: 100%;
    word-wrap: break-word;
    line-height: 1.6;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
    border: 1px solid rgba(255, 255, 255, 0.1);
  }

  pre {
    background: #2b2b2b;
    border: 1px solid #00bcd4;
    padding: 15px;
    border-radius: 8px;
    overflow-x: auto;
  }

  /* Loader styling (assuming you have a Loader.svelte component) */
  .loader {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
  }

  /* Responsive Design */
  @media (max-width: 768px) {
    h2 {
      font-size: 2.2em;
      margin-top: 20px;
    }

    .container {
      margin: 20px;
      padding: 25px;
    }

    .button-group {
      flex-direction: column;
      gap: 10px;
    }

    button {
      width: 100%;
    }

    textarea {
      min-height: 120px;
    }
  }

  @media (max-width: 480px) {
    h2 {
      font-size: 1.8em;
    }

    .container {
      padding: 20px;
      margin: 15px;
    }

    p, pre {
      font-size: 0.95em;
      padding: 15px;
    }

    button {
      font-size: 0.95em;
      padding: 12px;
    }
  }
</style>
<br><br><br>
<h2>FICAFS IA</h2>
<div class="page-container">
  <div class="container">
    <textarea bind:value={prompt} rows="6" placeholder="Pregunta lo que necesites, respondere lo que solicites..."></textarea>

    <div class="button-group">
      <button on:click={() => apiSubmit("text")}>Generar texto</button>
    </div>

    {#if load}
      <div class="loader">
        <Loader />
      </div>
    {/if}

    {#if result}
      <div class="response-container">
        {#if isTextResponse}
          <p>{result}</p>
        {:else}
          <pre>{result}</pre>
        {/if}
      </div>
    {/if}
  </div>
</div>
