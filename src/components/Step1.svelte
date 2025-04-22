<script>
    export let data = {
        name: '',
        email: '',
        phone: ''
    };

    const updateField = (field, value) => {
        data = { ...data, [field]: value };
        const event = new CustomEvent('update', {
            detail: { [field]: value }
        });
        dispatchEvent(event);
    };
</script>

<style>
    .step-content {
        margin-top: 2rem;
    }

    input {
        width: 100%;
        padding: 0.8rem;
        margin-bottom: 1rem;
        border: 1px solid #ccc;
        border-radius: 8px;
    }

    h2 {
        margin-bottom: 0.5rem;
    }

    p {
        margin-bottom: 1.5rem;
        color: #666;
    }
</style>

<div class="step-content">
    <h2>Información Personal</h2>
    <p>Por favor, proporciona tu nombre, correo electrónico y número de teléfono.</p>

    <input
            type="text"
            placeholder="Nombre"
            bind:value={data.name}
            on:input={(e) => updateField('name', e.target.value)}
    />

    <input
            type="email"
            placeholder="Correo electrónico"
            bind:value={data.email}
            on:input={(e) => updateField('email', e.target.value)}
    />

    <input
            type="tel"
            placeholder="Número de teléfono"
            bind:value={data.phone}
            on:input={(e) => updateField('phone', e.target.value)}
    />
</div>