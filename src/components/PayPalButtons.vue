<template>
  <div class="container d-flex justify-content-center bg-white shadow-lg">
      <div class="row m-0 p-0">
          <div class="col-6 p-5" id="paypal-button-container"></div>
      </div>
  </div>
</template>

<script>

export default {
data() {
  return {

  };
},
methods: {
},
mounted() {

  window.paypal
    .Buttons({
      style: {
        shape: "rect",
        layout: "vertical",
      },
      async createOrder() {
        try {
          const response = await fetch("https://www.bloggyapi.com/CreateOrder", {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify([
              {
                category: "Test",
                name: "Test",
                description: "Test",
                price: 1,
                quantity: 1,
              },
            ]),
          });

          const orderData = await response.json();

          if (orderData.id) {
            return orderData.id;
          } else {
            const errorDetail = orderData?.details?.[0];
            const errorMessage = errorDetail
              ? `${errorDetail.issue} ${errorDetail.description} (${orderData.debug_id})`
              : JSON.stringify(orderData);

            throw new Error(errorMessage);
          }
        } catch (error) {
          console.error(error);
          resultMessage(`Could not initiate PayPal Checkout...<br><br>${error}`);
        }
      },
      async onApprove(data, actions) {
        try {
          const response = await fetch(`https://www.bloggyapi.com/CapturePayment`, {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify(data.orderID),
          });

          const orderData = await response.json();
          if (orderData.StatusCode === 201) {
            resultMessage("Your order has been placed. Thank you!");
          }
        } catch (error) {
          console.error(error);
          resultMessage(`Sorry, your transaction could not be processed...<br><br>${error}`);
        }
      },
    })
    .render("#paypal-button-container");
},
};
</script>
