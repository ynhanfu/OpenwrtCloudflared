# How to Install Cloudflared on OpenWrt

Installing Cloudflared on OpenWrt can be a bit tricky if you rely on the `opkg` package manager, as the Cloudflared version available there might be outdated. This is particularly true for devices with specialized hardware, like those found in wired chips. To ensure you have the latest version of Cloudflared compatible with your device, follow these steps:

1. **Download the Latest Version**: Visit the [Cloudflared releases page](https://github.com/cloudflare/cloudflared/releases) and download the appropriate version for your device. For example, if you're using a Raspberry Pi with OpenWrt, you might need `cloudflared-linux-aarch64.rpm`.

2. **Identify Your CPU Architecture**: Use the `uname -m` command on your OpenWrt device to determine your CPU architecture. For instance:

    ```sh
    root@OpenWrt:~# uname -m
    aarch64
    ```

3. **Extract the Cloudflared Binary**: Unpack the `.rpm` file into a `.cpio` file, and then extract the contents of the `.cpio` file to obtain the Cloudflared binary executable. This process transforms:

    `cloudflared-linux-aarch64.rpm` → `cloudflared-2.cpio` → `cloudflared`

4. **Prepare the Binary for Transfer**: As OpenWrt devices may have limited storage and lack certain unpacking tools, it's best to package the Cloudflared binary into a `.zip` file on your desktop.

5. **Transfer the Binary to Your Device**: You can use tools like `scp` to copy the Cloudflared binary to your OpenWrt device. Alternatively, you can host the binary on your desktop and have your device download it. For instance:

    ```sh
    python3 -m http.server 8000
    ```

    This command hosts the content on port 8000.

6. **Copy the Binary to `/usr/bin/cloudflared`**: Once the binary is on your device, move it to the appropriate location.

7. **Create a Service File**: Use a text editor to create a service file for Cloudflared, e.g., `vi /usr/bin/cloudflared`, and populate it with the necessary configuration. You can use a template for this purpose.

8. **Set Up Your Tunnel**: Replace the placeholder token value in the service file with your actual token. You can obtain a token by setting up a tunnel on the Cloudflare website.

9. **Make the Script Executable**: Ensure the service file is executable by running:

    ```sh
    chmod +x /usr/bin/cloudflared
    ```

10. **Enable the Service**: Enable the Cloudflared service:

    ```sh
    /usr/bin/cloudflared enable
    ```

11. **Start the Cloudflared Tunnel**: Initiate the Cloudflared tunnel:

    ```sh
    /usr/bin/cloudflared start
    ```

12. **Reboot and Test**: Reboot your device to test the Cloudflared setup. You can then return to the Cloudflared website to configure your public host.

By following these steps, you should have Cloudflared up and running on your OpenWrt device, allowing you to enjoy its features and benefits. Happy browsing! 😊
