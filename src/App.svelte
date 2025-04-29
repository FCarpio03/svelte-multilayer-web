<script>
  import Step1 from './components/Step1.svelte';
  import Step2 from './components/Step2.svelte';
  import Step3 from './components/Step3.svelte';
  import Step4 from './components/Step4.svelte';
  import Step5 from './components/Step5.svelte';
  import '@fortawesome/fontawesome-free/css/all.min.css';

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
    currentStep = 5;
    isSubmitted = true;
  };
</script>

<style>
  :root {
    --primary: #0044ff;
    --background: transparent;
    --text: #0044ff;
    --card-bg: #fff;
    --border: #ccc;
    --radius: 1rem;
    --transition: 0.3s ease;
    --background-image: url("/public/image/background.svg");
    --background-size: cover;
    --font-custom: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    --position: relative;
  }

  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    src: url("/public/fonts/Ubuntu-Bold.ttf");
    color: var(--text);
    background-image: url("/public/image/background.svg");
    background-size: cover;
    position: var(--position);
    margin: 0;
    padding: 0;
  }

  .app {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    padding: 1rem;
    background-image: url("/public/image/background.svg");
    background-size: cover;
    position: relative;
  }

  .form-container {
    background: var(--card-bg);
    padding: 2.5rem;
    border-radius: var(--radius);
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
    width: 100%;
    max-width: 700px;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    position: var(--position);
  }

  .steps-indicator {
    display: flex;
    justify-content: space-between;
    max-width: 400px;
    margin: 0 auto 2rem auto;
  }

  .step {
    width: 60px;
    height: 60px;
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
    gap: 1rem;
    margin-top: 1.5rem;
  }

  .btn {
    padding: 0.9rem 2rem;
    border-radius: 8px;
    border: none;
    font-weight: bold;
    font-size: 1rem;
    transition: var(--transition);
    cursor: pointer;
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
    transform: translateY(-2px);
  }

  .no-navigation .navigation-buttons {
    display: none;
  }

  @media screen and (max-width: 768px) {
    .form-container {
      padding: 1.5rem;
      margin: 1rem;
      max-width: 100%;
    }

    .btn {
      padding: 0.7rem 1.5rem;
      font-size: 0.9rem;
    }

    .step {
      width: 50px;
      height: 50px;
      font-size: 0.9rem;
    }

    .steps-indicator {
      max-width: 300px;
    }
  }

  @media screen and (max-width: 480px) {
    .app {
      padding: 0.5rem;
    }

    .form-container {
      padding: 1rem;
      margin: 0.5rem;
      border-radius: 0.8rem;
    }

    .navigation-buttons {
      flex-direction: row;
      width: 100%;
    }

    .btn {
      width: 48%;
      padding: 0.8rem 0;
      text-align: center;
    }

    .steps-indicator {
      gap: 0.5rem;
      max-width: 250px;
    }

    .step {
      width: 40px;
      height: 40px;
      font-size: 0.8rem;
    }
  }

  @media screen and (max-width: 320px) {
    .form-container {
      padding: 0.8rem;
    }

    .btn {
      font-size: 0.8rem;
      padding: 0.6rem 0;
    }

    .step {
      width: 35px;
      height: 35px;
    }
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
        <Step1 data={formData.personalInfo} update={(e) => handleInputChange('personalInfo', e.detail)}/>
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
        {:else}
          <div></div>
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