<script>
  import Step1 from './components/Step1.svelte';
  import Step2 from './components/Step2.svelte';
  import Step3 from './components/Step3.svelte';
  import Step4 from './components/Step4.svelte';
  import Step5 from './components/Step5.svelte';

  let currentStep = 1;
  let isSubmitted = false;

  let formData = {
    personalInfo: {
      name: '',
      email: '',
      phone: ''
    },
    plan: {
      type: '',
      isYearly: false
    },
    addons: [],
    summary: {}
  };

  const handleInputChange = (stepKey, data) => {
    formData = {
      ...formData,
      [stepKey]: {
        ...formData[stepKey],
        ...data
      }
    };
  };

  const handleAddonChange = (addons) => {
    formData = {
      ...formData,
      addons
    };
  };

  const nextStep = () => {
    if (currentStep < 4) currentStep += 1;
  };

  const prevStep = () => {
    if (currentStep > 1) currentStep -= 1;
  };

  const confirm = () => {
    currentStep = 5; // Esto cambia al paso final cuando el botón de confirmar es presionado.
    isSubmitted = true; // Marca que la confirmación ha sido realizada
  };
</script>

<style>
  :root {
    --primary: #483EFF;
    --background: #f0f4ff;
    --text: #333;
    --card-bg: #fff;
    --border: #ccc;
    --radius: 1rem;
    --transition: 0.3s ease;
  }

  body {
    margin: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: var(--background);
    color: var(--text);
  }

  .app {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background: var(--background);
    padding: 2rem;
  }

  .form-container {
    background: var(--card-bg);
    padding: 2.5rem;
    border-radius: var(--radius);
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
    width: 100%;
    max-width: 700px;
  }

  .steps-indicator {
    display: flex;
    justify-content: space-between;
    margin-bottom: 2.5rem;
  }

  .step {
    width: 45px;
    height: 45px;
    border-radius: 50%;
    background: #ddd;
    color: #555;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    transition: var(--transition);
  }

  .step.active {
    background: var(--primary);
    color: #fff;
  }

  .navigation-buttons {
    display: flex;
    justify-content: space-between;
    margin-top: 2.5rem;
  }

  .btn {
    padding: 0.9rem 2rem;
    border-radius: 8px;
    border: none;
    font-weight: bold;
    font-size: 1rem;
    transition: var(--transition);
  }

  .btn-back {
    background: transparent;
    border: 2px solid var(--primary);
    color: var(--primary);
  }

  .btn-next {
    background: var(--primary);
    color: white;
  }

  .btn:hover {
    opacity: 0.9;
  }

  /* Estilo para ocultar la navegación en el último paso */
  .no-navigation .navigation-buttons {
    display: none;
  }
</style>

<div class="app">
  <div class="form-container">
    {#if !isSubmitted}
      <div class="steps-indicator">
        {#each [1, 2, 3, 4] as step}
          <div class="step {currentStep === step ? 'active' : ''}">{step}</div>
        {/each}
      </div>

      {#if currentStep === 1}
        <Step1 bind:data={formData.personalInfo} on:update={(e) => handleInputChange('personalInfo', e.detail)} />
      {:else if currentStep === 2}
        <Step2 bind:data={formData.plan} on:update={(e) => handleInputChange('plan', e.detail)} />
      {:else if currentStep === 3}
        <Step3 bind:selected={formData.addons} on:update={(e) => handleAddonChange(e.detail)} />
      {:else if currentStep === 4}
        <Step4 {formData} />
      {/if}

      <div class="navigation-buttons">
        {#if currentStep > 1}
          <button class="btn btn-back" on:click={prevStep}>Atrás</button>
        {/if}
        {#if currentStep < 4}
          <button class="btn btn-next" on:click={nextStep}>Siguiente</button>
        {:else}
          <button class="btn btn-next" on:click={confirm}>Confirmar</button>
        {/if}
      </div>
    {:else}
      <div class="no-navigation">
        <Step5 {formData} />
      </div>
    {/if}
  </div>
</div>
