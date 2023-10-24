<script lang="ts">
  export let handleSubmit: () => void
  export let formCompleted: boolean
  export let cardholderName: string
  export let cardNumber: string
  export let errors: any
  export let expirationMonth: string
  export let expirationYear: string
  export let cvc: string

  const updateCardholderName = (e: Event) => {
    cardholderName = (e.target as HTMLInputElement).value
  }

  const formatCardNumber = () => {
    cardNumber = cardNumber.replace(/[^0-9]/g, '');

    cardNumber = cardNumber.replace(/(.{4})/g, '$1 ').trim();

    if (cardNumber.length > 16) {
      cardNumber = cardNumber.slice(0, 19);
    }
  }

  const formatMonth = () => {
    expirationMonth = expirationMonth.replace(/[^0-9]/g, '')

    if (expirationMonth.length > 2) {
      expirationMonth = expirationMonth.slice(0, 2)
    }
  }

  const formatYear = () => {
    expirationYear = expirationYear.replace(/[^0-9]/g, '')

    if (expirationYear.length > 2) {
      expirationYear = expirationYear.slice(0, 2)
    }
  }

  const formatCvc = () => {
    cvc = cvc.replace(/[^0-9]/g, '')

    if (cvc.length > 3) {
      cvc = cvc.slice(0, 3)
    }
  }
</script>


<form on:submit|preventDefault={handleSubmit} class={`${formCompleted ? 'hidden' : ''}`}>
  <div class="single-input">
    <label for="name">Cardholder Name</label>
    <input type="text" id="name" bind:value={cardholderName} on:input={updateCardholderName}>
    {#if errors.cardholderName}<span>{errors.cardholderName}</span>{/if}
  </div>
  <div class="single-input">
    <label for="card-number">Card Number</label>
    <input type="text" id="card-number" bind:value={cardNumber} on:input={formatCardNumber}>
    {#if errors.cardNumber}<span>{errors.cardNumber}</span>{/if}
  </div>
  <div class="input-container">
    <div class="multiple-input">
      <p>MM / YY</p>
      <input type="text" bind:value={expirationMonth} on:input={formatMonth}>
      <input type="text" bind:value={expirationYear} on:input={formatYear}>
      {#if errors.expiration}<span>{errors.expiration}</span>{/if}
    </div>
    <div class="single-input">
      <label for="cvc">CVC</label>
      <input type="text" id="cvc" bind:value={cvc} on:input={formatCvc}>
      {#if errors.cvc}<span>{errors.cvc}</span>{/if}
    </div>
  </div>
  <button class="btn-primary" type="submit">Confirm</button>
</form>