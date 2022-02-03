# stratix-pi-emireduction
Documention on what I did to reduce AMI on stratux with a PI4


# Set the PI4 on a fixed frequency to ensure stable performance

See also :    https://www.raspberrypi.com/documentation/computers/config_txt.html#never_over_voltage
Discussions : https://forums.raspberrypi.com/viewtopic.php?f=29&t=6201&start=250

Enabled and set in `/boot/config.txt`

```console
# Reduce EMI
arm_freq=600
arm_freq_min=600
gpu_freq=325
gpu_freq_min=325
over_voltage=-4
over_voltage_min=-4
over_voltage_sdram=-4
over_voltage_sdram_c=-4
over_voltage_sdram_i=-4
over_voltage_sdram_p=-4
# hdmi_blanking=1 might be implemented in pi4 at some stage, we are just trying 2 not sure if that works...
hdmi_blanking=2

# Other not needed.
disable_splash=1
```

Add in `/etc/rc.local` before the exit 0 call (The above min/max frequency should also disable CPU scaling

```bash
for governor in $(ls /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor)
do
    echo "Powersave" > $governor
done
```
