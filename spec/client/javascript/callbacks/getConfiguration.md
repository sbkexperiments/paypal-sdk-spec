# Get Configuration

Callback used to fetch merchant customizations for a payment button.

This callback will be invoked whenever the user takes an action which requires merchant customizations, e.g.

- Clicking a payment button 

This customization data is needed before `createOrder` callback is executed and hence cannot be part of the `order` resource.

## Examples

### Create order from client

```javascript
const getConfiguration = (data) => {
    return {
      apple: {
        shipping: {
          address: "HIDE",
          name: "EDIT",
          email: "EDIT",
          phone: "EDIT"
        }
      }
    };
}
```

## Notes

- Merchant should not make any api calls to their backend server within this callback.
- Possible enums for `shipping.address`, `shipping.name`, `shipping.email` and `shipping.phone` are EDIT, VIEW_ONLY, HIDE.
