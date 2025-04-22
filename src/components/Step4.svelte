<script>
    export let personalInfo = {};
    export let plan = {};
    export let addons = [];

    const planDetails = {
        Arcade: { monthly: 9, yearly: 90 },
        Advanced: { monthly: 12, yearly: 120 },
        Pro: { monthly: 15, yearly: 150 }
    };

    const total = plan.isYearly
        ? planDetails[plan.type].yearly
        : planDetails[plan.type].monthly;

    const addonsTotal = addons.reduce((sum, addon) => {
        return plan.isYearly ? sum + addon.yearly : sum + addon.monthly;
    }, 0);

    const finalTotal = total + addonsTotal;
</script>

<style>
    .summary {
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }

    .summary-info {
        margin-top: 1rem;
    }

    .summary-info p {
        margin: 0.5rem 0;
    }

    .total {
        font-size: 1.2rem;
        font-weight: bold;
        margin-top: 1rem;
    }
</style>

<div class="step-content">
    <h2>Resumen</h2>
    <p>Verifica que todo esté correcto antes de confirmar tu suscripción.</p>

    <div class="summary">
        <div class="summary-info">
            <p><strong>Nombre:</strong> {personalInfo.name}</p>
            <p><strong>Correo electrónico:</strong> {personalInfo.email}</p>
            <p><strong>Número de teléfono:</strong> {personalInfo.phone}</p>
        </div>

        <div class="summary-info">
            <p><strong>Plan:</strong> {plan.type}</p>
            <p><strong>Facturación:</strong> {plan.isYearly ? 'Anual' : 'Mensual'}</p>
        </div>

        <div class="summary-info">
            <strong>Complementos:</strong>
            {#if addons.length > 0}
                <ul>
                    {#each addons as addon}
                        <li>{addon.name} +${plan.isYearly ? addon.yearly : addon.monthly}</li>
                    {/each}
                </ul>
            {:else}
                <p>No has seleccionado complementos.</p>
            {/if}
        </div>

        <div class="total">
            <p><strong>Total:</strong> ${finalTotal} / {plan.isYearly ? 'año' : 'mes'}</p>
        </div>
    </div>
</div>
