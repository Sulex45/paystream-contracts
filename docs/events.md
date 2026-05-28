# Contract Event Schema

This document describes all on-chain events emitted by the PayStream stream contract.
Each event has a **topic** (used for filtering) and a **data payload**.

---

## StreamCreated

Fired when an employer creates a new salary stream.

- **Topic:** `("created", stream_id: u64)`
- **Data:** `(employer: Address, employee: Address, rate_per_second: i128)`

| Field | Type | Description |
|---|---|---|
| `employer` | `Address` | Address that funded the stream |
| `employee` | `Address` | Address that receives streamed tokens |
| `rate_per_second` | `i128` | Tokens streamed per second |

**Example payload:**
```json
{
  "topic": ["created", 1],
  "data": {
    "employer": "GABC...XYZ",
    "employee": "GDZY...ABC",
    "rate_per_second": 100
  }
}
```

---

## Withdrawn

Fired when an employee withdraws earned tokens from a stream.

- **Topic:** `("withdraw", stream_id: u64)`
- **Data:** `(employee: Address, amount: i128)`

| Field | Type | Description |
|---|---|---|
| `employee` | `Address` | Address that received the tokens |
| `amount` | `i128` | Number of tokens withdrawn |

**Example payload:**
```json
{
  "topic": ["withdraw", 1],
  "data": {
    "employee": "GDZY...ABC",
    "amount": 500
  }
}
```

---

## Paused

Fired when an employer pauses a stream, stopping token accrual.

- **Topic:** `("paused", stream_id: u64)`
- **Data:** `()`

| Field | Type | Description |
|---|---|---|
| *(none)* | — | No additional data |

**Example payload:**
```json
{
  "topic": ["paused", 1],
  "data": {}
}
```

---

## Resumed

Fired when an employer resumes a paused stream.

- **Topic:** `("resumed", stream_id: u64)`
- **Data:** `()`

| Field | Type | Description |
|---|---|---|
| *(none)* | — | No additional data |

**Example payload:**
```json
{
  "topic": ["resumed", 1],
  "data": {}
}
```

---

## Cancelled

Fired when an employer cancels a stream. Earned tokens are sent to the employee; remainder is refunded to the employer.

- **Topic:** `("cancelled", stream_id: u64)`
- **Data:** `()`

| Field | Type | Description |
|---|---|---|
| *(none)* | — | No additional data |

**Example payload:**
```json
{
  "topic": ["cancelled", 1],
  "data": {}
}
```

---

## ToppedUp

Fired when an employer adds more funds to an active stream.

- **Topic:** `("topup", stream_id: u64)`
- **Data:** `(employer: Address, amount: i128)`

| Field | Type | Description |
|---|---|---|
| `employer` | `Address` | Address that added the funds |
| `amount` | `i128` | Number of tokens added |

**Example payload:**
```json
{
  "topic": ["topup", 1],
  "data": {
    "employer": "GABC...XYZ",
    "amount": 1000
  }
}
```

---

## StreamTransferred

Fired when an employee transfers their stream rights to another address.

- **Topic:** `("transferred", stream_id: u64)`
- **Data:** `(previous_employee: Address, new_employee: Address)`

| Field | Type | Description |
|---|---|---|
| `previous_employee` | `Address` | Address that previously held the stream rights |
| `new_employee` | `Address` | Address that now holds the stream rights |

**Example payload:**
```json
{
  "topic": ["transferred", 1],
  "data": {
    "previous_employee": "GDZY...ABC",
    "new_employee": "GBRW...DEF"
  }
}
```
