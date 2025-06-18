<style>
    :global(body) {
        font-family: 'Poppins', sans-serif;
        background: linear-gradient(135deg, #2a2a2a, #1a1a1a);
        color: #e0e0e0;
        margin: 0;
        padding: 0;
        min-height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }

    .container{
        display: block;
        width: 50%;
        text-align: left;
    }

    main{
        margin: 0 auto;
        color: #e0e0e0;
    }

    #datosUser{
        display: block;
        border: solid 1px #3a3a3a;
        background-color: #2a2a2a;
        border-radius: 5px;
        height: 50px;
        margin: 15px auto;
        padding: 10px;

        transition: all 0.3s ease-in-out;
    }

    #datosUser:hover{
        background-color: #3a3a3a;
        transform: scale(105%);
    }

</style>
<div class="container">
    <main>
        <h2>Datos del usuario</h2>
        <span id="datosUser">
            <p>Nombre: FICA FS</p>
        </span>
        <span id="datosUser">
            <p>Area profesional: Tecnologias de la Información.</p>
        </span>
        <span id="datosUser">
            <p>Correo: ficafs@gmail.com</p>
        </span>
        <span id="datosUser">
            <p>Telefono: 551-2566-1313</p>
        </span>
    </main>
</div>