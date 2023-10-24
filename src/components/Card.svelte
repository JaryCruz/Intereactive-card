<script lang="ts">
  export let cardholderName: string
  export let cardNumber: string
  export let expirationMonth: string
  export let expirationYear: string
</script>

<div class="card">
  <div class="card-logo">
    <div class="circle"></div>
    <div class="small-circle"></div>
  </div>
  <div class="card-number">
    {cardNumber ? cardNumber : '0000 0000 0000 0000'}
  </div>
  <div class="personal-details">
    <p class="card-name">{cardholderName ? cardholderName : 'First Last' }</p>
    <p class="card-exp">
      <span>
        {expirationMonth ? expirationMonth : '00' } 
      </span>
      /
      <span>
        {expirationYear ? expirationYear : '00' } 
      </span>
    </p>
  </div>
</div>