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
        width: 100%;
        max-width: 600px;
        margin: 0 auto;
        padding: 0 0.5rem;
    }

    h2 {
        font-size: 2rem;
        color: var(--primary);
        text-align: center;
        margin-bottom: 1.5rem;
        margin-top: 0;
    }

    .confirmation-card {
        background: var(--card-bg);
        padding: 2rem;
        border-radius: 1rem;
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        width: 100%;
        text-align: center;
    }

    .confirmation-card h3 {
        font-size: 1.6rem;
        color: black;
        margin-bottom: 1.5rem;
        margin-top: 0;
    }

    .confirmation-card p {
        font-size: 1rem;
        margin-bottom: 1.5rem;
        color: #555;
    }

    .summary {
        display: flex;
        flex-direction: column;
        gap: 0.8rem;
        text-align: left;
        font-size: 1.1rem;
        background: #f9f9f9;
        padding: 1.5rem;
        border-radius: 0.8rem;
        margin-bottom: 1.5rem;
    }

    .summary p {
        margin: 0;
        padding-bottom: 0.5rem;
        border-bottom: 1px dashed #ddd;
    }

    .summary p:last-child {
        border-bottom: none;
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
        margin-top: 1rem;
        cursor: pointer;
        transition: 0.3s ease;
    }

    .btn:hover {
        opacity: 0.9;
    }

    @media screen and (max-width: 768px) {
        h2 {
            font-size: 1.8rem;
        }

        .confirmation-card {
            padding: 1.5rem;
        }

        .confirmation-card h3 {
            font-size: 1.4rem;
        }

        .summary {
            padding: 1.2rem;
        }
    }

    @media screen and (max-width: 480px) {
        h2 {
            font-size: 1.6rem;
            margin-bottom: 1rem;
        }

        .step-content {
            gap: 1.5rem;
            padding: 0;
        }

        .confirmation-card {
            padding: 1.2rem;
            border-radius: 0.8rem;
        }

        .confirmation-card h3 {
            font-size: 1.3rem;
            margin-bottom: 1rem;
        }

        .summary {
            padding: 1rem;
            font-size: 1rem;
            gap: 0.5rem;
        }

        .btn {
            padding: 0.8rem 2rem;
            font-size: 0.9rem;
            width: 100%;
        }
    }

    @media screen and (max-width: 320px) {
        h2 {
            font-size: 1.4rem;
        }

        .confirmation-card {
            padding: 1rem;
        }

        .confirmation-card h3 {
            font-size: 1.2rem;
        }

        .summary {
            padding: 0.8rem;
            font-size: 0.9rem;
        }

        .btn {
            padding: 0.8rem;
        }
    }
</style>

<div class="step-content">
    <h2><i class="fa-solid fa-user"></i>¡Gracias por tu suscripción!</h2>

    <div class="confirmation-card">
        <h3><strong><i class="fa-solid fa-money-bill-1-wave"></i>Comprobante de tu suscripción<i class="fa-solid fa-money-bill-1-wave"></i></strong></h3>

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

        <p>Si todo es correcto, ¡estás listo para comenzar! Si necesitas realizar algún cambio, puedes volver a empezar.</p>

        <button class="btn" on:click={() => window.location.reload()}>Volver al Inicio</button>
    </div>
</div>