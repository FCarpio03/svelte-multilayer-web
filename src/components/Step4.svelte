<script>
    export let formData;

    const { personalInfo, plan, addons } = formData;
    const basePrices = {
        Básico: plan.isYearly ? 50 : 5,
        Estándar: plan.isYearly ? 75 : 7,
        Premium: plan.isYearly ? 100 : 10
    };

    const addonPrices = {
        'Acceso a juegos multijugador': plan.isYearly ? 20 : 2,
        '1TB adicional de almacenamiento en la nube': plan.isYearly ? 10 : 1,
        'Tema personalizado para tu perfil': plan.isYearly ? 20 : 2
    };

    const planPrice = basePrices[plan.type] || 0;
    const addonsTotal = addons.reduce((total, addon) => total + (addonPrices[addon] || 0), 0);
    const total = planPrice + addonsTotal;
</script>

<style>
    .step-content {
        display: flex;
        flex-direction: column;
        gap: 1.5rem;
        color: var(--text);
    }

    h2 {
        margin: 0;
        font-size: 2rem;
        color: var(--primary);
        text-align: center;
    }

    .section {
        background: var(--card-bg);
        padding: 1.5rem;
        border-radius: 1rem;
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }

    .section h3 {
        font-size: 1.6rem;
        color: var(--primary);
        margin-bottom: 1rem;
    }

    .addon {
        display: flex;
        justify-content: space-between;
        margin-bottom: 1rem;
    }

    .addon span {
        color: #333;
    }

    .addon-price {
        font-weight: bold;
        color: var(--primary);
    }

    .total {
        font-size: 1.2rem;
        font-weight: bold;
        text-align: right;
        color: var(--primary);
        margin-top: 1.5rem;
    }
</style>

<div class="step-content">
    <h2>Resumen de tu suscripción</h2>

    <div class="section">
        <h3>Información personal</h3>
        <p><strong>Nombre:</strong> {personalInfo.name}</p>
        <p><strong>Email:</strong> {personalInfo.email}</p>
        <p><strong>Teléfono:</strong> {personalInfo.phone}</p>
    </div>

    <div class="section">
        <h3>Plan seleccionado</h3>
        <p>{plan.type} ({plan.isYearly ? 'Anual' : 'Mensual'})</p>
        <p><strong>Precio:</strong> ${planPrice}</p>
    </div>

    <div class="section">
        <h3>Servicios adicionales</h3>
        {#if addons.length > 0}
            {#each addons as addon}
                <div class="addon">
                    <span>{addon}</span>
                    <span class="addon-price">${addonPrices[addon] || 0}</span>
                </div>
            {/each}
        {:else}
            <p>No seleccionaste servicios adicionales.</p>
        {/if}
    </div>

    <div class="total">
        Total: ${total}
    </div>
</div>
