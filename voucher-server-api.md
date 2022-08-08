# 1. Endpoint: 

`POST /finalize-voucher-purchase`

Request:

```ts
type RequestBody = {
  safeAddress : string, // "0x4568236725783625783243873253..."
  voucherProviderId: string, // z.b. "goodbuy"
}
```

Response:

200: ok
```ts
type ResponseBody = {}
```
4??: fehler

# 2. Endpoint

`GET /voucher-providers`

Request:

```ts
type RequestBody = {}
```

Response:

200: ok
```ts
type ResponseBody = Array<VoucherProvider>
```

4??: fehler

# 3. Endpoint

`GET /vouchers-of-user/<safeAddress>`

Request:

```ts
type RequestBody = {}
```

Response:

200: ok
```ts
type ResponseBody = Array<Voucher>
```

4??: fehler

-----------------------------------------------------------------


# Types:

```ts
type VoucherProvider = {
  id: string,
  name: string,
  logoUrl: string,
  shopUrl: string,
  availableOffers: Array<VoucherOffer>
}

type VoucherOffer = {
  amount: number, // Euro-Cent
  countAvailable: number
}

type Voucher = {
  voucherProviderId: string,
  voucherCode: string
}
```
