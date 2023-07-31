# bluealsa-sysvinit

Sysvinit (init.d) script for BlueAlsa.

## Instructions

1. Install BlueAlsa:

    ```
    # apt install bluez-alsa-utils
    ```
2. Edit `~/.asoundrc`:

    ```
    defaults.bluealsa {
        service "org.bluealsa"
        interface "hci0"            # your Bluetooth controller
        device "C8:7B:23:CF:C6:A7"  # your headset Bluetooth MAC address
        profile "a2dp"
    }

    pcm.!default bluealsa
    ctl.!default bluealsa
    ```
3. Install and start sysvinit script:

    ```
    # cp bluealsa /etc/init.d
    # update-rc.d bluealsa defaults
    # update-rc.d bluealsa enable
    # service bluealsa start
    ```

4. Connect to your Bluetooth device:
   * Put your Bluetooth device in pairing mode
   * Run `bluetoothctl` and run next commands there:

     ```
     scan on
     pair XX:XX:XX:XX:XX:XX
     trust XX:XX:XX:XX:XX:XX
     connect XX:XX:XX:XX:XX:XX
     ```

5. Test:

    ```
    $ aplay -D bluealsa /usr/share/sounds/alsa/Front_Center.wav
    ```

## Authors

**Sam Protsenko**

## License

The project is licensed under the GPLv3.

## References

[1] https://introt.github.io/docs/raspberrypi/bluealsa.html
