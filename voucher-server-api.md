# 1. Endpoint:

Initiates a purchase when a transaction of a user to the xbge address occured, but no corresponding voucher was found.

`POST /finalize-voucher-purchase`

Request:

```ts
type RequestBody = {
  safeAddress: string; // "0x4568236725783625783243873253..."
  voucherProviderId: string; // z.b. "goodbuy"
  amount: number; // Euro-Cent
}
```

Response:

200: ok
```ts
type ResponseBody = {};
```
4??: fehler

# 2. Endpoint

Returns all avalable vouchers and corresponding amounts to be displayed in the shop interface.

`GET /voucher-providers`

Request:

```ts
type RequestBody = {};
```

Response:

200: ok
```ts
type ResponseBody = Array<VoucherProvider>;
```

4??: fehler

# 3. Endpoint

Returns all vouchers bought by a specific user, identified by the safe address.

`GET /vouchers-of-user/<safeAddress>`

Request:

```ts
type RequestBody = {};
```

Response:

200: ok
```ts
type ResponseBody = Array<Voucher>;
```

4??: fehler

# 4. Endpoint

Returns all vouchers that have been sold, after a given timestamp.

`GET /vouchers`

Request:

```ts
type RequestBody = {
  timestamp: string;
};
```

Response:

200: ok
```ts
type ResponseBody = Array<Voucher>;
```

4??: fehler

-----------------------------------------------------------------


# Types:

```ts
type VoucherProvider = {
  id: string;
  name: string;
  logoUrl: string;
  shopUrl: string;
  availableOffers: Array<VoucherOffer>;
}

type VoucherOffer = {
  amount: number; // Euro-Cent
  countAvailable: number;
}

type Voucher = {
  voucherProviderId: string;
  voucherAmount: number; // Euro-Cent
  voucherCode: string;
  sold: null | SoldVoucher; // null until it was sold
}

type SoldVoucher = {
  transactionId: string;
  safeAddress: string;
  timestamp: string;
}
```
