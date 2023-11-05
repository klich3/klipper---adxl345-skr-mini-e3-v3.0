# Klipper - ADXL345 SKR MINI E3 v3.0

Different methods to connect ADXL345 to SKR MINI 3E v3

in your configuration file we add at the beginning of your configuration file
comment out the `[input_shaper]` so there are no problems.

```
[include adxl345.cfg]
```

Depending on how you are going to connect it you have to comment or uncomment pertinent parts

# SPI 1

| pin row | pin row |
| --------| ------- |
| 1 -  x | 2 - x|
| 3 - NSS | 4 - CLK |
| 5 - MOSI | 6 - MISO |
| 7 - 3.3v vcc | 8 - GND |

![spi1-port-wiring](images/spi1-port.jpg)

```
[adxl345]
cs_pin: PD9
spi_bus: spi1
```

---

# I/O PORT

|PD0 | PD2 | PD3 | PD4 | PD5 |
|-----|-----|-----|-----|-----|
| cs  | scl | sda | sd0 |  x |
| NSS | CLK | MOSI| MISO|  x |

![io-port-wiring](images/io-port.jpg)

```
[adxl345]
cs_pin: PD0
spi_software_miso_pin: PD4
spi_software_sclk_pin: PD2
spi_software_mosi_pin: PD3
```

---

## Pinout
![pinout](images/miniE3-v30-pinout.png)
![sk3](images/skr.png)

## G-Code Commands

1) command `MEASURE_AXES_NOISE` Should be somewhere in the range of ~1-100
2) `TEST_RESONANCES AXIS=X`
3) `TEST_RESONANCES AXIS=Y`
4) ~/klipper/scripts/calibrate_shaper.py /tmp/resonances_x_*.csv -o /tmp/shaper_calibrate_x.png
    ~/klipper/scripts/calibrate_shaper.py /tmp/resonances_y_*.csv -o /tmp/shaper_calibrate_y.png