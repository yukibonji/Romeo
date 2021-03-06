Romeo
=====

Romeo is an F# implementation of the secure API protocol used by Cryptocurrency Exchange Vault Of Satoshi, see https://www.vaultofsatoshi.com/api

keywords: hmac message verification


Example of usage
================

Placing an order at the exchange.

```fsharp
open Romeo.Client

let place_order (config : Config) (units: Currency) (price : Currency) (order_type : string) : PlaceOrderResponse =
  let data = 
    [| ("type", order_type)
    ; ("order_currency","BTC")
    ; ("units[precision]",units.precision)
    ; ("units[value]",units.value)
    ; ("units[value_int]", units.value_int)
    ; ("payment_currency","CAD")
    ; ("price[precision]", price.precision)
    ; ("price[value]", price.value)
    ; ("price[value_int]", price.value_int)|]
  let bytes = call config "/trade/place" data 
  from_json bytes
```

On the server side
==================

If you happen to use Suave (http://suave.io) to code your API there is a web part for it.

```fsharp
val verify (secret : string -> string) (success_part : string -> WebPart) : WebPart
```

Where `secret` is a function that returns the `shared_secret` given an `api_key` and `success_part` your API web part.

NuGet
=====

To install Romeo, run the following command in the Package Manager Console

```bash
PM> Install-Package Romeo
```
