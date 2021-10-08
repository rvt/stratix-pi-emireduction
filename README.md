# stratix-pi-emireduction
Documention on what I did to reduce AMI on stratux with a PI4


# Set the PI4 on a fixed frequency to ensure stable performance

See also :    https://www.raspberrypi.com/documentation/computers/config_txt.html#never_over_voltage
Discussions : https://forums.raspberrypi.com/viewtopic.php?f=29&t=6201&start=250

Enabled and set in `/etc/config.txt`

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
# They say might be implemented in pi4 at some stage..
hdmi_blanking=1
hdmi_mode=1

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
