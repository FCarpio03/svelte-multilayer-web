<script>
    export let data = {};
    export let update;

    const handleChange = (e) => {
        update({ [e.target.name]: e.target.value });
    };
</script>

<style>
    .step-content {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 0.5rem;
        padding: 1rem;
        background-color: #fff;
        border-radius: 16px;
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
        width: 600px;
    }

    .step-title {
        font-size: 1.75rem;
        font-weight: 700;
        color: #483EFF;
        text-align: center;
    }

    .input-group {
        display: flex;
        flex-direction: column;
        width: 100%;
    }

    label {
        font-weight: 600;
        margin-bottom: 0.4rem;
        color: #000000;
        font-size: 0.95rem;
    }

    input {
        background-color: white;
        border: 1px solid var(--border);
        padding: 0.8rem;
        border-radius: 8px;
        width: 95%;
        font-size: 1rem;
        color: black;
    }

    input:focus {
        outline: none;
        border-color: var(--primary);
        background-color: #f8f9ff;
    }
    .title{
        color: blue;
        font-size: 4rem;
    }
</style>

<div class="main-title">

</div>

<div class="step-content">
    <h1 class="title"><i class="fa-solid fa-house"></i></h1>
    <h2 class="step-title">Información Personal</h2>

    <div class="input-group">
        <label for="name"><strong>Nombre completo</strong></label>
        <input
                id="name"
                name="name"
                type="text"
                placeholder="Jose Perez"
                bind:value={data.name}
                on:input={handleChange}
        />
    </div>

    <div class="input-group">
        <label for="email"><strong>Correo electrónico</strong></label>
        <input
                id="email"
                name="email"
                type="email"
                placeholder="correo@ejemplo.com"
                bind:value={data.email}
                on:input={handleChange}
        />
    </div>

    <div class="input-group">
        <label for="phone"><strong>Teléfono</strong></label>
        <input
                id="phone"
                name="phone"
                type="tel"
                placeholder="123-456-7899"
                bind:value={data.phone}
                on:input={handleChange}
        />
    </div>
</div>