# I2C Bus aktivieren

``` dts title="/boot/dietpiEnv.txt"
overlay= ... i2c0 i2c2
```

# Clock auf 1M hoch setzten
in /boot/...?
``` shell
sudo dtc -I dtb -O dts sun8i-h3-nanopi-neo.dtb -o sun8i-h3-nanopi-neo.dts
```

Edit section in *.dts and recompile the dts:

``` shell
dtc -I dts -O dtb sun8i-h3-nanopi-neo.dts -o sun8i-h3-nanopi-neo.dtb
```

The original dtb had no clock frequency entries for any of the i2c buses: i2c0 (i2c@01c2ac00), i2c1 (i2c@01c2b000) and i2c2 (i2c@01c2b400). Add a line to the i2c@01c2b000 (i2c) section (or whichever bus you're wishing to change):

 ``` dts
 clock-frequency = <0xF4240>;
 ``` 
 
  400 khz: <0x61A80>
 1000 khz: <0xF4240>

## Beispiel
``` dts title="sun8i-h3-nanopi-neo.dts"
i2c@1c2ac00 {
    compatible = "allwinner,sun6i-a31-i2c";
    reg = <0x1c2ac00 0x400>;
    interrupts = <0x00 0x06 0x04>;
    clocks = <0x03 0x3b>;
    resets = <0x03 0x2e>;
    pinctrl-names = "default";
    pinctrl-0 = <0x1a>;
    status = "disabled";
    #address-cells = <0x01>;
    #size-cells = <0x00>;
    phandle = <0x67>;
    clock-frequency = <0xF4240>;
};
```