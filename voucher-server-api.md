# 1. Endpoint:

Initiates a purchase when a transaction of a user to the xbge address occured, but no corresponding voucher was found.

`POST /finalize-voucher-purchase`

Request:

```ts
type RequestBody = {
  safeAddress: string; // e.g. "0x4568236725783625783243873253..."
  voucherProviderId: string; // e.g. "goodbuy"
  amount: number; // Euro-Cent
  transactionId: string; // e.g. "20046-7"
}
```

Response:

200: ok
```ts
type ResponseBody = {};
```
4??: error

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

4??: error

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

4??: error

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

4??: error

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

-----------------------------------------------------------------

# Encryption / Decryption of voucher codes:

```ts
import crypto from "crypto";

const exampleSecretKey = "QTbY4bCBk8DByPqXzvib7tEwBzQdSYDo";

export const encrypt = (secretKey: string, data: string) => {
  const cipher = crypto.createCipheriv("AES-256-ECB", secretKey, null);
  let encrypted = cipher.update(data, "utf8", "base64");
  encrypted += cipher.final("base64");
  return encrypted;
};

export const decrypt = (secretKey: string, data: string) => {
  const decipheriv = crypto.createDecipheriv("AES-256-ECB", secretKey, null);
  let decryptediv = decipheriv.update(data, "base64", "utf8");
  decryptediv += decipheriv.final("utf8");
  return decryptediv;
};

const encrypted = encrypt(exampleSecretKey, "Encrypt-Me :-)");
console.log("encrypted: ", encrypted);
console.log("decrypted: ", decrypt(exampleSecretKey, encrypted));
```
