<script>
  import { onMount } from 'svelte';
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
    isSubmitted = true;
  };
</script>

<style>
  .app {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-color: #f0f0f0;
  }

  .form-container {
    background: white;
    padding: 2rem;
    border-radius: 15px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    width: 100%;
    max-width: 600px;
  }

  .steps-indicator {
    display: flex;
    justify-content: center;
    margin-bottom: 2rem;
    gap: 1rem;
  }

  .step {
    width: 35px;
    height: 35px;
    border-radius: 50%;
    border: 2px solid #ccc;
    display: flex;
    align-items: center;
    justify-content: center;
    background: white;
  }

  .step.active {
    background: #483EFF;
    color: white;
    border-color: #483EFF;
  }

  .navigation-buttons {
    display: flex;
    justify-content: space-between;
    margin-top: 2rem;
  }

  button {
    padding: 0.8rem 1.5rem;
    border: none;
    border-radius: 8px;
    cursor: pointer;
  }

  button:first-child {
    background: transparent;
    color: #666;
  }

  button:last-child {
    background: #483EFF;
    color: white;
  }
</style>

<div class="app">
  <div class="form-container">
    {#if !isSubmitted}
      <div class="steps-indicator">
        {#each [1,2,3,4] as step}
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
          <button on:click={prevStep}>Atrás</button>
        {/if}
        {#if currentStep < 4}
          <button on:click={nextStep}>Siguiente</button>
        {:else}
          <button on:click={confirm}>Confirmar</button>
        {/if}
      </div>
    {:else}
      <Step5 />
    {/if}
  </div>
</div>