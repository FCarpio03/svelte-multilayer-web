<script>
    import { createEventDispatcher } from 'svelte';

    export let data = {};
    const dispatch = createEventDispatcher();

    const handleChange = (e) => {
        dispatch('update', { [e.target.name]: e.target.value });
    };
</script>

<style>
    .step-content {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        gap: 1.2rem;
        width: 100%;
        max-width: 600px;
        margin: 0 auto;
    }

    .step-header {
        text-align: center;
        width: 100%;
        margin-bottom: 1rem;
    }

    .title {
        color: blue;
        font-size: 3.5rem;
        margin: 0;
        text-align: center;
        width: 100%;
    }

    .step-title {
        font-size: 1.75rem;
        font-weight: 700;
        color: #483EFF;
        text-align: center;
        margin: 0.5rem 0 1.5rem 0;
        width: 100%;
    }

    .input-group {
        display: flex;
        flex-direction: column;
        width: 100%;
        margin-bottom: 0.8rem;
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
        padding: 0.8rem 1rem;
        border-radius: 8px;
        width: 100%;
        box-sizing: border-box;
        font-size: 1rem;
        color: black;
    }

    input:focus {
        outline: none;
        border-color: var(--primary);
        background-color: #f8f9ff;
        box-shadow: 0 0 0 2px rgba(0, 68, 255, 0.1);
    }

    @media screen and (max-width: 768px) {
        .step-content {
            padding: 0 0.5rem;
        }

        .title {
            font-size: 3rem;
        }

        .step-title {
            font-size: 1.5rem;
        }
    }

    @media screen and (max-width: 480px) {
        .title {
            font-size: 2.5rem;
        }

        .step-title {
            font-size: 1.3rem;
            margin-bottom: 1rem;
        }

        input {
            padding: 0.7rem;
        }
    }

    @media screen and (max-width: 320px) {
        .title {
            font-size: 2rem;
        }

        .step-title {
            font-size: 1.2rem;
        }
    }
</style>

<div class="step-content">
    <div class="step-header">
        <h1 class="title"><i class="fa-solid fa-house"></i></h1>
        <h2 class="step-title">Información Personal</h2>
    </div>

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