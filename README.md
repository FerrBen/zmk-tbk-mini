# TBK Mini

ZMK config for **TBK Mini** — a hand-wired split Corne (3x6 + thumbs) running on
two `nice_nano_v2` controllers. Keys only: no OLED, no encoder.

Pin/matrix wiring is taken from the
[Sputnik Handwired Split Corne](https://github.com/vostoklabs/Sputnik-Handwired-Split-Corne-Keyboard-)
build (the original `zmk-config` there was missing the keymap, `west.yml`,
`module.yml`, `Kconfig.shield` and a combined split matrix transform — those are
all filled in here).

## Building

Push to GitHub and the `Build ZMK firmware` action produces:

- `tbk_mini_left-nice_nano_v2-zmk.uf2`  (central / USB + BLE)
- `tbk_mini_right-nice_nano_v2-zmk.uf2` (peripheral)
- `settings_reset-nice_nano_v2-zmk.uf2` (flash to both halves to clear BLE pairing if needed)

Or build locally / with the ZMK VS Code container.

## Wiring

`nice_nano_v2` GPIOs, `col2row` diode direction.

**Left**  — rows: `P1.00 P0.11 P1.04 P1.06`  cols: `P0.09 P0.10 P1.11 P1.13 P1.15 P0.02`
**Right** — rows: `P0.29 P1.13 P0.10 P0.09`  cols: `P1.06 P1.04 P0.11 P1.00 P0.24 P0.22`

## Matrix / keymap notes

Standard **42-key Corne**: three 6-key alpha rows per side plus **3 thumbs per
side** on the inner columns (transform `RC(3,3..5)` left, `RC(3,6..8)` right).

Thumb keys (per side, inner→outer for left / outer→inner for right):

- **Space** — layer-tap: tap = Space, hold = Lower
- **Bksp**  — layer-tap: tap = Backspace, hold = Raise
- **Del** (left) / **Enter** (right)

Holding a Space (Lower) + a Bksp (Raise) thumb together reaches the Adjust layer.

Layers: Base / Lower (numbers, symbols, F-keys) / Raise (nav) / Adjust
(Bluetooth + USB/BLE output, via Lower+Raise).

On the **Adjust** layer, the bottom-row outer keys are reset controls, one per
half (each only resets the side it's on):

- outer corner (`Z`/`?` position) = `&bootloader` — enter UF2 flashing mode
- next key in (`X`/`.` position) = `&sys_reset` — soft reboot
