<template>
  <div class="container d-flex justify-content-center bg-white shadow-lg">
      <div class="row m-0 p-0">
          <div class="col-6 p-5" id="paypal-button-container"></div>
          <p id="responseMessage"></p>
          <!-- <p>{{ msg }}</p>
          <button @click="addText">Change text</button> -->
      </div>
  </div>
</template>

<script>

export default {

data() {
  return {
    msg: "TEST",
  };
},
methods: {
  addText() {
    this.msg = "Another TEST";
  }
},
mounted() {
  let flag = false;
  // Get the <p> element by its ID
  let responseMessage = document.getElementById("responseMessage");
  window.paypal
    .Buttons({
      style: {
        shape: "rect",
        layout: "vertical",
      },
      async createOrder() {
        var endPoint = flag == false ? "https://localhost:7165/CreateOrder" : "https://www.bloggyapi.com/CreateOrder";

        try {
          const response = await fetch(endPoint, {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify([
              {
                category: "eBooks",
                name: "The Art of Capturing Payments",
                description: "Make Money",
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
          // Set the text content of the <p> element
          responseMessage.classList.add("alert", "alert-danger");
          responseMessage.textContent = `Could not initiate PayPal Checkout...<br><br>${error}`;
          resultMessage(`Could not initiate PayPal Checkout...<br><br>${error}`);
        }
      },
      async onApprove(data, actions) {
        try {
          var endPoint = flag == false ? "https://localhost:7165/CapturePayment" : "https://www.bloggyapi.com/CapturePayment";
          const response = await fetch(endPoint, {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify(data.orderID),
          });

          const orderData = await response.json();
          if (orderData.StatusCode === 201) {
            responseMessage.classList.add("alert", "alert-info");
            responseMessage.textContent = "Your order has been placed. Thank you!";
          }
        } catch (error) {
          responseMessage.textContent = `Sorry, your transaction could not be processed...<br><br>${error}`;
        }
      },
    })
    .render("#paypal-button-container");
},
};
</script>
