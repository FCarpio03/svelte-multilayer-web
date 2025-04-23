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
        gap: 2rem;
        padding: 2rem;
        background-color: #fff;
        border-radius: 16px;
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.05);
        max-width: 500px;
        margin: 0 auto;
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
        color: #333;
        font-size: 0.95rem;
    }

    input {
        padding: 0.9rem;
        border: 2px solid #ccc;
        border-radius: 12px;
        font-size: 1rem;
        transition: all 0.3s ease;
    }

    input:focus {
        outline: none;
        border-color: #483EFF;
        box-shadow: 0 0 5px rgba(72, 63, 255, 0.2);
    }
</style>

<div class="step-content">
    <h2 class="step-title">Información Personal</h2>

    <div class="input-group">
        <label for="name">Nombre completo</label>
        <input
                id="name"
                name="name"
                type="text"
                placeholder="Juan Pérez"
                bind:value={data.name}
                on:input={handleChange}
        />
    </div>

    <div class="input-group">
        <label for="email">Correo electrónico</label>
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
        <label for="phone">Teléfono</label>
        <input
                id="phone"
                name="phone"
                type="tel"
                placeholder="809-555-1234"
                bind:value={data.phone}
                on:input={handleChange}
        />
    </div>
</div>
