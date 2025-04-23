<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    export let selected = [];

    const addonsList = [
        {
            name: 'Acceso a juegos multijugador',
            description: 'Juega en línea con amigos',
            monthly: 2,
            yearly: 20
        },
        {
            name: '1TB adicional de almacenamiento en la nube',
            description: 'Guarda tus partidas y archivos en la nube',
            monthly: 1,
            yearly: 10
        },
        {
            name: 'Tema personalizado para tu perfil',
            description: 'Personaliza tu apariencia',
            monthly: 2,
            yearly: 20
        }
    ];

    const toggleAddon = (addonName) => {
        const updated = selected.includes(addonName)
            ? selected.filter(name => name !== addonName)
            : [...selected, addonName];

        dispatch('update', updated);
    };

    const isSelected = (addonName) => selected.includes(addonName);
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
        font-size: 1.8rem;
        color: var(--text);
    }

    p.description {
        color: #666;
        margin: 0;
    }

    .addons {
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }

    .addon {
        padding: 1.2rem;
        border: 2px solid #ccc;
        border-radius: 1rem;
        transition: 0.3s ease;
        cursor: pointer;
        background: var(--card-bg);
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .addon.selected {
        border-color: var(--primary);
        background: var(--background);
    }

    .addon-info {
        display: flex;
        flex-direction: column;
    }

    .addon-name {
        font-weight: bold;
        margin-bottom: 0.2rem;
        color: var(--text);
    }

    .addon-description {
        font-size: 0.9rem;
        color: #555;
    }

    .addon-price {
        font-weight: bold;
        color: var(--primary);
    }
</style>

<div class="step-content">
    <h2>Selecciona complementos</h2>
    <p class="description">Mejora tu experiencia con servicios adicionales.</p>

    <div class="addons">
        {#each addonsList as addon}
            <div
                    class="addon {isSelected(addon.name) ? 'selected' : ''}"
                    on:click={() => toggleAddon(addon.name)}
            >
                <div class="addon-info">
                    <span class="addon-name">{addon.name}</span>
                    <span class="addon-description">{addon.description}</span>
                </div>
                <div class="addon-price">+${addon.monthly}/mes o +${addon.yearly}/año</div>
            </div>
        {/each}
    </div>
</div>
