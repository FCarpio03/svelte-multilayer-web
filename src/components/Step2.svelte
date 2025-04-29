<script>
    import { createEventDispatcher } from 'svelte';

    export let data;
    const dispatch = createEventDispatcher();

    const plans = [
        { name: 'Básico', monthly: 5, yearly: 50, icon: 'fa-solid fa-face-smile' },
        { name: 'Estándar', monthly: 7, yearly: 75, icon: 'fa-solid fa-face-grin-stars' },
        { name: 'Premium', monthly: 10, yearly: 100, icon: 'fa-solid fa-crown' }
    ];

    const handlePlanClick = (planName) => {
        data.type = planName;
        dispatch('update', { type: planName });
    };

    const toggleBilling = (isYearly) => {
        data.isYearly = isYearly;
        dispatch('update', { isYearly });
    };
</script>

<style>
    .step-content {
        display: flex;
        flex-direction: column;
        gap: 1.5rem;
        width: 100%;
        max-width: 600px;
        margin: 0 auto;
        padding: 0 0.5rem;
    }

    .step-title {
        font-size: 1.75rem;
        font-weight: 700;
        color: #483EFF;
        text-align: center;
        margin: 0 0 0.5rem 0;
    }

    .description-dos {
        color: black;
        text-align: center;
        margin: 0 0 1rem 0;
        font-size: 1rem;
        line-height: 1.5;
    }

    .plans {
        display: flex;
        flex-direction: column;
        gap: 1rem;
        width: 100%;
    }

    .plan {
        border: 2px solid #ccc;
        border-radius: 12px;
        padding: 1rem 1.5rem;
        cursor: pointer;
        transition: all 0.3s ease;
        background: white;
        color: #333;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .plan.selected {
        border-color: #483EFF;
        background: #eaf0ff;
        box-shadow: 0 0 8px rgba(72, 63, 255, 0.2);
    }

    .plan-info {
        display: flex;
        flex-direction: column;
    }

    .plan-title {
        font-weight: 600;
        font-size: 1.1rem;
    }

    .plan-price {
        font-size: 0.95rem;
        color: #24a506;
        margin-top: 0.2rem;
    }

    .plan-icon {
        font-size: 1.5rem;
        color: #483EFF;
    }

    .billing-toggle {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 1rem;
        background: #eaeaea;
        border-radius: 12px;
        padding: 0.5rem;
        margin-top: 1rem;
    }

    .billing-option {
        padding: 0.5rem 1rem;
        border-radius: 8px;
        cursor: pointer;
        font-weight: 600;
        color: #555;
        transition: 0.3s ease;
        text-align: center;
        flex: 1;
    }

    .billing-option.active {
        background: #483EFF;
        color: white;
    }

    @media screen and (max-width: 768px) {
        .step-title {
            font-size: 1.5rem;
        }

        .description-dos {
            font-size: 0.95rem;
        }

        .plan {
            padding: 0.8rem 1.2rem;
        }

        .plan-title {
            font-size: 1rem;
        }

        .plan-price {
            font-size: 0.9rem;
        }
    }

    @media screen and (max-width: 480px) {
        .step-title {
            font-size: 1.3rem;
        }

        .description-dos {
            font-size: 0.9rem;
        }

        .plan {
            padding: 0.8rem 1rem;
        }

        .plan-icon {
            font-size: 1.3rem;
        }

        .billing-option {
            padding: 0.4rem 0.8rem;
            font-size: 0.9rem;
        }
    }

    @media screen and (max-width: 320px) {
        .step-title {
            font-size: 1.2rem;
        }

        .plan {
            padding: 0.7rem 0.8rem;
        }

        .plan-title {
            font-size: 0.9rem;
        }

        .plan-price {
            font-size: 0.85rem;
        }

        .billing-option {
            padding: 0.3rem 0.6rem;
            font-size: 0.85rem;
        }
    }
</style>

<div class="step-content">
    <h2 class="step-title"><i class="fa-solid fa-object-ungroup"></i> Selecciona tu plan</h2>
    <p class="description-dos"><strong><i class="fa-solid fa-book-open-reader"></i> Tienes la opción de elegir entre 3 planes, el Básico, Estándar y Premium. Después elige si lo quieres Mensual o Anual. <i class="fa-solid fa-book-open-reader"></i></strong></p>

    <div class="plans">
        {#each plans as plan}
            <div
                    class="plan {data.type === plan.name ? 'selected' : ''}"
                    on:click={() => handlePlanClick(plan.name)}
            >
                <div class="plan-info">
                    <div class="plan-title">{plan.name}</div>
                    <div class="plan-price">
                        ${data.isYearly ? plan.yearly + '/año' : plan.monthly + '/mes'}
                    </div>
                </div>
                <div class="plan-icon">
                    <i class={plan.icon}></i>
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