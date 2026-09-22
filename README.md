# Facility Code / Card Number Calculator

A small, self-contained HTML tool for converting between a Wiegand 26-bit **facility code**, **card number**, **hex card code**, and **raw Wiegand value** (the 8-digit hex many readers and panel logs show) — in any direction, live, as you type.

No build step, no dependencies, no server. Open the file in a browser and it just works, online or off.

## Features

- **Four live-linked fields** — edit the facility code, card number, hex value, or raw Wiegand value, and the rest update automatically.
- **Parity checking** — raw Wiegand values are checked against their parity bits, so a misread or mistyped value gets flagged.
- **Visual breakdown** — a color-coded diagram shows how the 8-bit facility code and 16-bit card number each convert to hex and combine into the final 24-bit code.
- **Input validation** — out-of-range or malformed values are flagged inline (facility code 0–255, card number 0–65535, hex up to 6 digits, raw Wiegand up to 03FFFFFF).
- **Mobile-friendly** — designed for a narrow viewport so it's just as usable on a phone as a desktop.
- **Fully portable** — the entire app is one `.html` file. Save it, email it, put it on a USB stick, or open it straight from your downloads folder — no installation required.

## Usage

1. Download `index.html` (optionally renaming it to something like `hid-calculator.html`.
2. Open it in any modern web browser (desktop or mobile).
3. Type into any one of the fields — the others fill in automatically.
4. The **How this is calculated** section at the bottom of the card shows the conversion visualized.

## How it works

Facility code and card number are combined into a single number using:

```
combined = facilityCode × 65536 + cardNumber
```

That combined number, written in hexadecimal, is the badge's hex card code. Going the other direction, dividing the hex value by 65536 recovers the facility code, and the remainder recovers the card number.

The **raw Wiegand** value is what a reader actually sends: the same 24 data bits with a parity bit added at each end.

- The leading bit is **even parity** over the first 12 data bits.
- The trailing bit is **odd parity** over the last 12 data bits.

The result is written as 8 hex digits. For example, facility 22 / card 8618 is hex `1621AA` and raw `002C4354`. Because the leading parity bit shifts every digit by one bit, the raw value doesn't visibly contain the hex code.

## License

Licensed under [Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/). You're free to share and adapt this for non-commercial purposes, with attribution. (Also linked from within the app itself, via the "CC BY-NC 4.0" link in the footer.)
