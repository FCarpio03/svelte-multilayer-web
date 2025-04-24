<script>
    export let data;

    const plans = [
        { name: 'Básico', monthly: 5, yearly: 50, icon: 'fa-solid fa-face-smile' },
        { name: 'Estándar', monthly: 7, yearly: 75, icon: 'fa-solid fa-face-grin-stars' },
        { name: 'Premium', monthly: 10, yearly: 100, icon: 'fa-solid fa-crown' }

    ];

    const handlePlanClick = (planName) => {
        data.type = planName;
    };

    const toggleBilling = (isYearly) => {
        data.isYearly = isYearly;
    };

</script>

<style>
    .step-content {
        display: flex;
        flex-direction: column;
        gap: 1rem;
        padding: 0.1rem;
        max-width: 600px;
        background: #f9f9f9;
        border-radius: 16px;
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.05);
    }

    .step-title {
        font-size: 1.75rem;
        font-weight: 700;
        color: #483EFF;
        text-align: center;
        padding: 0rem;
    }

    .plans {
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }

    .plan {
        border: 2px solid #ccc;
        border-radius: 12px;
        padding: 1rem 1.5rem;
        cursor: pointer;
        transition: all 0.3s ease;
        background: white;
        color: #333;
    }

    .plan.selected {
        border-color: #483EFF;
        background: #eaf0ff;
        box-shadow: 0 0 8px rgba(72, 63, 255, 0.2);
    }

    .plan-title {
        font-weight: 600;
        font-size: 1.1rem;
    }

    .plan-price {
        font-size: 0.95rem;
        color: #24a506;
    }

    .billing-toggle {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 1rem;
        background: #eaeaea;
        border-radius: 12px;
        padding: 0.5rem;
    }

    .billing-option {
        padding: 0.5rem 1rem;
        border-radius: 8px;
        cursor: pointer;
        font-weight: 600;
        color: #555;
        transition: 0.3s ease;
    }

    .billing-option.active {
        background: #483EFF;
        color: white;
    }

    .description-dos{
        color: black;
    }

</style>

<div class="step-content">
    <h2 class="step-title"><i class="fa-solid fa-object-ungroup"></i> Selecciona tu plan</h2>
    <p class="description-dos"><strong><i class="fa-solid fa-book-open-reader"></i>Tienes la opcion de elejir entre 3 planes, el Basico, Estandar y Premium. Despues elije si lo quieres Mensual o Anual.<i class="fa-solid fa-book-open-reader"></i></strong></p>

    <div class="plans">
        {#each plans as plan}
            <div
                    class="plan {data.type === plan.name ? 'selected' : ''}"
                    on:click={() => handlePlanClick(plan.name)}
            >
                <div class="plan-title">{plan.name}</div>
                <div class="plan-price">
                    ${data.isYearly ? plan.yearly + '/año' : plan.monthly + '/mes'}
                </div>
            </div>
        {/each}
    </div>

    <div class="billing-toggle">
        <div
                class="billing-option {data.isYearly ? '' : 'active'}"
                on:click={() => toggleBilling(false)}
        >
            Mensual
        </div>
        <div
                class="billing-option {data.isYearly ? 'active' : ''}"
                on:click={() => toggleBilling(true)}
        >
            Anual
        </div>
    </div>
</div>