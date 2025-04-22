<script>
    export let data = [];

    const addonsList = [
        {
            name: 'Online service',
            description: 'Acceso a juegos multijugador',
            monthly: 1,
            yearly: 10
        },
        {
            name: 'Larger storage',
            description: '1TB adicional de almacenamiento en la nube',
            monthly: 2,
            yearly: 20
        },
        {
            name: 'Customizable Profile',
            description: 'Tema personalizado para tu perfil',
            monthly: 2,
            yearly: 20
        }
    ];

    const toggleAddon = (addon) => {
        let newData;
        if (data.find(a => a.name === addon.name)) {
            newData = data.filter(a => a.name !== addon.name);
        } else {
            newData = [...data, addon];
        }

        data = newData;
        dispatchEvent(new CustomEvent('update', { detail: newData }));
    };

    const isSelected = (addon) => {
        return data.some(a => a.name === addon.name);
    };
</script>

<style>
    .addons {
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }

    .addon {
        border: 2px solid #ccc;
        padding: 1rem;
        border-radius: 10px;
        cursor: pointer;
    }

    .addon.selected {
        border-color: #483EFF;
        background-color: #f0f4ff;
    }

    .addon-description {
        color: #666;
        font-size: 0.9rem;
    }
</style>

<div class="step-content">
    <h2>Selecciona complementos</h2>
    <p>Los complementos mejoran tu experiencia de juego.</p>

    <div class="addons">
        {#each addonsList as addon}
            <div
                    class="addon {isSelected(addon) ? 'selected' : ''}"
                    on:click={() => toggleAddon(addon)}
            >
                <strong>{addon.name}</strong><br />
                <span class="addon-description">{addon.description}</span><br />
                +${addon.monthly}/mes o +${addon.yearly}/año
            </div>
        {/each}
    </div>
</div>