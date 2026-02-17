# Japanese IC Card Reader (React Native)

A mobile application built with **React Native** that leverages NFC technology to read and display data from Japanese transit cards (Suica, PASMO, ICOCA, etc.). This app provides real-time balance checks and a detailed transaction history directly from the card's FeliCa chip.

---

## 🚀 Features

* **Real-time Balance:** Instantly view the remaining yen on your card.
* **Transaction History:** Decodes the last 10 transactions, including:
* **Process Type:** Fare, Charge, Adjustment, Purchase, etc.
* **Terminal Info:** Identifies if the transaction happened at a Gate, Vending Machine, or on a Bus.
* **Usage Amount:** Calculates the difference ( or ) between transactions.
* **Date:** Extracts the precise date of activity.


* **Brand Detection:** Automatically identifies the issuer (e.g., Suica, PASMO, ICOCA, Sugoca, Nimoca).
* **Dark Mode Support:** Dynamic UI that adapts to system-wide appearance settings.
* **Haptic Feedback:** Vibrates upon a successful scan for a premium feel.

---

## 🛠️ Technical Overview

The app uses `react-native-nfc-manager` to communicate with the **FeliCa (NfcF)** standard used in Japan.

### How it works:

1. **Polling:** Requests a connection using the `0xff, 0xff` system code.
2. **Brand Identification:** Queries the Issuer Service ID (`0x008b`) to map the card to a specific provider.
3. **Multi-block Read:** Uses a single optimized command to read 10 blocks of history data from the `0x090f` service.
4. **Byte Parsing:** Bit-shifts raw hex data to extract dates and balances.
* *Balance Formula:* `block[10] + (block[11] << 8)`



---

## 📱 Getting Started

### Prerequisites

* An NFC-enabled Android or iOS device.
* Physical Japanese IC Card (Suica, PASMO, etc.).
* React Native development environment configured.

### Installation

1. **Clone the repository:**
```bash
git clone https://github.com/your-username/ic-card-reader.git
cd ic-card-reader

```


2. **Install dependencies:**
```bash
npm install
# or
yarn install

```


3. **Android Setup:**
* Ensure `<uses-permission android:name="android.permission.NFC" />` is in your `AndroidManifest.xml`.


4. **Run the app:**
```bash
npx react-native run-android

```



---

## 🗺️ Supported Mapping

| Category | Supported Labels |
| --- | --- |
| **Issuers** | Suica, ICOCA, Pasmo, Sugoca, Nimoca |
| **Terminals** | Ticket Kiosks, Buses, Vending Machines, Gates, Retail, etc. |
| **Processes** | Fares, Charges, Reissues, Purchases, Staff Adjustments |

---

## ⚠️ Important Note

This app reads **publicly accessible data** on the IC cards. It does not access private encrypted sectors, nor does it have the ability to write data or "refill" cards.

---
