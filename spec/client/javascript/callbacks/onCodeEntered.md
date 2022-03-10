# On Code Entered

Listen for buyers entering coupon/promo codes or gift cards, and update the totals for the transaction.

## Web - JavaScript

### Basic Callback

```javascript
const onCodeEntered = (data, actions) => {
    if (data.code.type === paypal.CODE_TYPE.COUPON && isValidCouponCode(data.code.value)) {
        return actions.order.patch([
            {
                op: 'replace',
                path: '/purchase_units/@reference_id=="default"/amount',
                value: {
                    currency_code: 'USD',
                    value: '8.00',
                    breakdown: {
                        item_total: {
                            currency_code: 'USD',
                            value: '10.00'
                        },
                        discount: {
                            currency_code: 'USD',
                            value: '2.00'
                        }
                    }
                }
            }
        ]);
    } else {
        return actions.reject();
    }
}
```

#### Data

- `orderID`: The orderID for the current transaction.
- `code`: The code entered
  - `type`: The code type. One of:
    - `coupon`: A coupon code
    - `giftcard`: A gift card 
  - `value`: The value of the coupon code

#### Actions

- `order`
  - `patch`: Patch the current transaction with new totals
- `reject`: Reject the code entered by the buyer

#### Return

- `Promise | undefined`
  - Return a `Promise`, or `undefined`. The buyer's checkout page will update once the promise has resolved, if a promise is passed.

### Patch the transaction amounts

- In `onCodeEntered`, call [Order Patch](https://developer.paypal.com/docs/api/orders/v2/#orders_patch) api to update the shipping and tax totals for the transaction.
  - If using [v2/orders](https://developer.paypal.com/docs/api/orders/v2), call from either your client or your server
  - If using any other api, call from your server

#### From your client

```javascript
const onCodeEntered = (data, actions) => {
    return actions.order.patch([
        {
            op: 'replace',
            path: '/purchase_units/@reference_id=="default"/amount',
            value: {
                currency_code: 'USD',
                value: '8.00',
                breakdown: {
                    item_total: {
                        currency_code: 'USD',
                        value: '10.00'
                    },
                    discount: {
                        currency_code: 'USD',
                        value: '2.00'
                    }
                }
            }
        }
    ]);
};
```

#### From your server

```javascript
const onCodeEntered = (data, actions) => {
    return fetch('https://my-server.com/api/paypal/update-cart-totals', {
        body: JSON.stringify({
            orderID: data.orderID,
            code: data.code
        })
    });
};
```

### Reject the code

```javascript
const onCodeEntered = (data, actions) => {
    return actions.reject();
};
```

## Types

```typescript
type OnCodeEntered = (
    data : OnCodeEnteredData,
    actions : OnCodeEnteredActions
) => undefined | Promise<undefined>

type OnCodeEnteredData = {
    orderID : string,
    code : {
        type : CODE_TYPE,
        value : string
    }
};

enum CODE_TYPE {
    COUPON = 'coupon',
    GIFTCARD = 'giftcard'
};

type OnCodeEnteredActions = {
    order : {
        patch : () =>
            Promise<PatchOrderResponse>
    },
    reject : () => Promise<void>
};

type PatchOrderResponse = {};
```