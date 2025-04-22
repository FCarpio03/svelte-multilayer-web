<script>
    export let data = {
        type: '',
        isYearly: false
    };

    const plans = [
        { name: 'Arcade', monthly: 9, yearly: 90 },
        { name: 'Advanced', monthly: 12, yearly: 120 },
        { name: 'Pro', monthly: 15, yearly: 150 }
    ];

    const selectPlan = (plan) => {
        data = { ...data, type: plan };
        dispatchEvent(new CustomEvent('update', {
            detail: { type: plan }
        }));
    };

    const toggleBilling = () => {
        data = { ...data, isYearly: !data.isYearly };
        dispatchEvent(new CustomEvent('update', {
            detail: { isYearly: data.isYearly }
        }));
    };
</script>

<style>
    .plans {
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }

    .plan {
        padding: 1rem;
        border: 2px solid #ccc;
        border-radius: 10px;
        cursor: pointer;
    }

    .plan.selected {
        border-color: #483EFF;
        background-color: #f0f4ff;
    }

    .billing-toggle {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 1rem;
        margin-top: 1.5rem;
    }

    .toggle-switch {
        cursor: pointer;
    }
</style>

<div class="step-content">
    <h2>Selecciona tu plan</h2>
    <p>Tienes la opción de pagar mensual o anualmente.</p>

    <div class="plans">
        {#each plans as plan}
            <div
                    class="plan {data.type === plan.name ? 'selected' : ''}"
                    on:click={() => selectPlan(plan.name)}
            >
                <strong>{plan.name}</strong><br />
                {#if data.isYearly}
                    ${plan.yearly}/año
                {:else}
                    ${plan.monthly}/mes
                {/if}
            </div>
        {/each}
    </div>

    <div class="billing-toggle">
        <span>Mensual</span>
        <label class="toggle-switch">
            <input type="checkbox" checked={data.isYearly} on:change={toggleBilling} />
        </label>
        <span>Anual</span>
    </div>
</div>
