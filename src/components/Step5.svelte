<script>
    export let formData;
</script>

<style>
    .step-content {
        display: flex;
        flex-direction: column;
        gap: 2rem;
        color: var(--text);
        align-items: center;
    }

    h2 {
        font-size: 2.2rem;
        color: var(--primary);
        text-align: center;
        margin-bottom: 2rem;
    }

    .confirmation-card {
        background: var(--card-bg);
        padding: 2rem;
        border-radius: 1rem;
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        width: 100%;
        max-width: 600px;
        text-align: center;
    }

    .confirmation-card h3 {
        font-size: 1.8rem;
        color: var(--primary);
        margin-bottom: 1.5rem;
    }

    .confirmation-card p {
        font-size: 1rem;
        margin-bottom: 1.5rem;
        color: #555;
    }

    .summary {
        display: flex;
        flex-direction: column;
        gap: 1rem;
        text-align: left;
        font-size: 1.1rem;
    }

    .summary p {
        margin: 0;
    }

    .summary strong {
        color: var(--primary);
    }

    .btn {
        padding: 1rem 2.5rem;
        border-radius: 8px;
        border: none;
        font-size: 1rem;
        font-weight: bold;
        background: var(--primary);
        color: white;
        margin-top: 2rem;
        cursor: pointer;
        transition: 0.3s ease;
    }

    .btn:hover {
        opacity: 0.9;
    }
</style>

<div class="step-content">
    <h2>¡Gracias por tu suscripción!</h2>

    <div class="confirmation-card">
        <h3>Resumen de tu suscripción</h3>

        <div class="summary">
            <p><strong>Nombre:</strong> {formData.personalInfo.name}</p>
            <p><strong>Email:</strong> {formData.personalInfo.email}</p>
            <p><strong>Teléfono:</strong> {formData.personalInfo.phone}</p>
            <p><strong>Plan Seleccionado:</strong> {formData.plan.type} ({formData.plan.isYearly ? 'Anual' : 'Mensual'})</p>
            <p><strong>Total:</strong> ${formData.plan.type === 'Básico' ? (formData.plan.isYearly ? 50 : 5) :
                formData.plan.type === 'Estándar' ? (formData.plan.isYearly ? 75 : 7) :
                    (formData.plan.isYearly ? 100 : 10)}</p>
            <p><strong>Servicios Adicionales:</strong> {#if formData.addons.length > 0}{formData.addons.join(', ')}{:else}Ninguno{/if}</p>
        </div>

        <p>Si todo es correcto, ¡estás listo para comenzar! Si necesitas realizar algún cambio, puedes volver atrás.</p>

        <button class="btn" on:click={() => window.location.reload()}>Volver al Inicio</button>
    </div>
</div>
