<script lang="ts">
  import '../lib/css/styles.css'
  import Card from '../components/Card.svelte';
  import FormThanks from '../components/FormThanks.svelte'
  import CardForm from '../components/CardForm.svelte'
  let cardholderName: string
  let expirationMonth: string
  let expirationYear: string
  let cvc: string
  let cardNumber: string = ''
  let errors: any = {}
  let formCompleted: boolean

  const handleSubmit = () => {
    errors = {} 

    if (!cardholderName) {
      errors.cardholderName = "Can't be blank"
    }
    
    if (!cardNumber) {
      errors.cardNumber = "Can't be blank"
    } else if (!isValidCardNumber(cardNumber)) {
      errors.cardNumber = "Invalid Format"
    }
    
    if (!expirationMonth || !expirationYear) {
      errors.expiration = "Can't be blank"
    }

    if (!cvc) {
      errors.cvc = "Can't be blank"
    } else if (!isCvcValid(cvc)) {
      errors.cvc = "Invalid Format"
    }

    if (Object.keys(errors).length === 0) {
      formCompleted = true
    }
  }

  const isValidCardNumber = (cardNumber: string) => {
    return /^\d{4} \d{4} \d{4} \d{4}$/.test(cardNumber)
  }

  const isCvcValid = (cvc: string) => {
    return /^\d{3,4}$/.test(cvc)
  }
</script>

<main>
  <Card 
    bind:cardNumber={cardNumber} 
    bind:cardholderName={cardholderName} 
    bind:expirationMonth={expirationMonth} 
    bind:expirationYear={expirationYear} 
  />  

  <CardForm 
    formCompleted={formCompleted} 
    errors={errors} 
    bind:cvc={cvc} 
    handleSubmit={handleSubmit}  
    bind:cardNumber={cardNumber} 
    bind:cardholderName={cardholderName} 
    bind:expirationMonth={expirationMonth} 
    bind:expirationYear={expirationYear} 
  />

  {#if formCompleted} 
    <FormThanks />
  {/if}
</main>