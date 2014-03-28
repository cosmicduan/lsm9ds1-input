Please use the following steps to integrate the LSM9DS1 driver into your kernel:

- copy the lsm9ds1.h file into "include/linux/input" folder.

- copy both lsm9ds1_acc_gyr.c and lsm9ds1_mag.c files into "drivers/input/misc" folder.

- edit the drivers/input/misc/Makefile to include object files:
o   obj-$(CONFIG_INPUT_LSM9DS1)    += lsm9ds1_mag.o lsm9ds1_acc_gyr.o.

- add a configuration entry into the Kconfig file like the following:

....
   config INPUT_LSM9DS1
	tristate "STMicroelectronics LSM9DS1"
	depends on INPUT
	help
	  Say Y here to enable STMicroelectronics LSM9DS1 inertial module.
....

To enable this driver you have to make the needed changes in the board file or into device tree.
The binding for device tree is shown below:

lsm9ds1-ag@0x6B {
        compatible = "st,lsm9ds1-acc-gyr";
        reg = <0x6B>;
        rot-matrix = /bits/ 16 <(1) (0) (0)
                     (0) (1) (0)
                     (0) (0) (1)>;
        g-poll-interval = <100>;
        g-min-interval = <2>;
        g-fs-range = <0>;
        x-poll-interval = <100>;
        x-min-interval = <1>;
        x-fs-range = <0>;
        aa-filter-bw = <0>;
    };

    lsm9ds1-m@0x1E {
        compatible = "st,lsm9ds1-mag";
        reg = <0x1E>;
        rot-matrix = /bits/ 16 <(1) (0) (0)
                     (0) (1) (0)
                     (0) (0) (1)>;
        poll-interval = <100>;
        min-interval = <13>;
        fs-range = <0>;
    };

 
