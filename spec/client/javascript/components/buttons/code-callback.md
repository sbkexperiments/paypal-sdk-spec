# On Code Entered Callback

Listen for buyers entering coupon/promo codes or gift cards, and update the totals for the transaction.

## Callback

```javascript
paypal.Buttons({
    onCodeEntered: (data, actions) => {
        if (data.code.type === paypal.CODE_TYPE.COUPON && isValidCouponCode(data.code.value)) {
            return actions.order.patch(...opts);
        } else {
            return actions.reject();
        }
    }
}).render('#paypal-buttons-container')
```

See:

- [`onCodeEntered`](../../callbacks/onCodeEntered.md)
