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
        width: 100%;
        max-width: 600px;
        margin: 0 auto;
        padding: 0 0.5rem;
    }

    h2 {
        margin: 0;
        font-size: 1.8rem;
        color: var(--text);
        text-align: center;
    }

    p.description {
        color: #000000;
        margin: 0.5rem 0 1rem 0;
        text-align: center;
        font-size: 1rem;
    }

    .addons {
        display: flex;
        flex-direction: column;
        gap: 1rem;
        width: 100%;
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
        background: #e4f2ff;
    }

    .addon-info {
        display: flex;
        flex-direction: column;
        flex: 1;
    }

    .addon-name {
        font-weight: bold;
        margin-bottom: 0.2rem;
        color: var(--text);
    }

    .addon-description {
        font-size: 0.9rem;
        color: #000000;
    }

    .addon-price {
        font-weight: bold;
        color: green;
        white-space: nowrap;
        margin-left: 0.5rem;
    }

    @media screen and (max-width: 768px) {
        h2 {
            font-size: 1.5rem;
        }

        p.description {
            font-size: 0.95rem;
        }

        .addon {
            padding: 1rem;
        }

        .addon-name {
            font-size: 0.95rem;
        }

        .addon-description {
            font-size: 0.85rem;
        }

        .addon-price {
            font-size: 0.9rem;
        }
    }

    @media screen and (max-width: 480px) {
        h2 {
            font-size: 1.3rem;
        }

        p.description {
            font-size: 0.9rem;
        }

        .addon {
            padding: 0.8rem;
            flex-direction: column;
            align-items: flex-start;
        }

        .addon-price {
            margin-top: 0.5rem;
            margin-left: 0;
        }
    }

    @media screen and (max-width: 320px) {
        h2 {
            font-size: 1.2rem;
        }

        .addon {
            padding: 0.7rem;
        }

        .addon-name {
            font-size: 0.9rem;
        }

        .addon-description {
            font-size: 0.8rem;
        }

        .addon-price {
            font-size: 0.85rem;
        }
    }
</style>

<div class="step-content">
    <h2><i class="fa-solid fa-table-columns"></i> Selecciona complementos</h2>
    <p class="description"><i class="fa-solid fa-money-bill"></i><strong>Mejora tu experiencia con servicios adicionales</strong><i class="fa-solid fa-money-bill"></i></p>

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
                <div class="addon-price">+${addon.monthly}/mes</div>
            </div>
        {/each}
    </div>
</div>