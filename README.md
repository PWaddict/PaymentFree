# PaymentFree Module for ProcessWire 3.x

ProcessWire module to accept FREE orders for digital giveaways.

## Requirements

- ProcessWire 3.x
- [PaymentModule](https://github.com/apeisa/PaymentModule/tree/PW3) (PW3 branch) ProcessWire module

## Usage

After you installed the module all you have to do is to set a condition via the API when PaymentFree should be enabled.
On your checkout template you normally have a code like this:

```PHP
$checkout = $modules->get("PadOnePageCheckout");
$checkout->setPaymentModule("PaymentPayPalExpressCheckout");
$checkout->setShippingModule("ShippingFixed");
echo $checkout->render();
```
You should replace it with something like the below example where we check if the order's total price is 0 and then we set the PaymentFree as PaymentModule where the user only have to click a button to complete the order and get the digital content for FREE without any actual payment getting involved.

```PHP
$checkout = $modules->get("PadOnePageCheckout");
if ($this->session->orderId) {
  $order = $this->pages->get($this->session->orderId);
  if ($order->pad_price_total <= 0) {
    $checkout->setPaymentModule("PaymentFree");
  } else {
    $checkout->setPaymentModule("PaymentPayPalExpressCheckout");
  }
}
$checkout->setShippingModule("ShippingFixed");
echo $checkout->render();
```
DO NOT select this module as payment method in PaymentModule settings.

## Changelog

### 1.0.0 (23 October 2018)

- Initial release

## License

GPL 2.0
