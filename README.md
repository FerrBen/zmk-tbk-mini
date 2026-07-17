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

The matrix is a full **4 rows x 6 columns per side** (48 positions total). Rows
0-2 are the three alpha rows; **row 3 is the thumb row**. Because the physical
thumb column wiring isn't documented in the source build, all 6 thumb columns per
side are given bindings in `config/tbk_mini.keymap`, so every switch you actually
wired will produce a key. Once you confirm which thumb columns are populated,
trim/rearrange `default_layer` row 3 to taste.

Layers: Base / Lower (numbers, symbols, F-keys) / Raise (nav) / Adjust
(Bluetooth + USB/BLE output, via Lower+Raise).
