# AnsiblePiRad
ansible playbook for Raspberry Pi setup for Wifi
PiRadsetup.yaml
Overview

PiRadsetup.yaml is a ready-to-use configuration for setting up a remote Kismet sensor on a Raspberry Pi (or similar device).
This YAML file automates the installation, configuration, and secure provisioning of a headless device for remote wireless monitoring and data collection using Kismet.
Features

    Automatic Kismet Sensor Installation:
    Installs and configures Kismet in sensor/remote mode for seamless integration with a central Kismet server.

    Secure Remote Access:
    Sets up SSH keys and tightens security for unattended/field deployments.

    WiFi Adapter Support:
    Enables monitor mode on supported adapters for advanced packet capture.

    Customizable Networking:
    Configure WiFi or Ethernet, static IPs, and hostname as needed.

    Auto-Updates & Health:
    Runs updates, enables logging, and can be easily extended for watchdogs or health checks.

Usage

    Clone this repository

git clone https://github.com/yourusername/PiRadsetup
cd PiRadsetup

Customize the YAML
Edit PiRadsetup.yaml with your WiFi details, SSH keys, and any custom settings.

Deploy to your Raspberry Pi

    cloud-init:
    Place PiRadsetup.yaml as user-data on your bootable SD card.

    Ansible:
    Run the playbook:

        ansible-playbook -i <your-inventory> PiRadsetup.yaml

    Boot & Monitor
    Power on your Pi.
    Once provisioned, it will connect to your Kismet server and begin remote capture automatically.

Example PiRadsetup.yaml Snippet

users:
  - name: pi
    groups: sudo
    ssh_authorized_keys:
      - ssh-rsa AAAAB3...yourpublickey...

packages:
  - git
  - python3
  - kismet

runcmd:
  - apt update && apt upgrade -y
  - systemctl enable kismet
  - systemctl start kismet
  - echo 'Configured for remote sensor mode'

Requirements

    Raspberry Pi (any model with sufficient resources; Pi 3 or later recommended)

    Raspberry Pi OS Lite (or Debian/Ubuntu equivalent)

    Supported WiFi adapter (for monitor mode)

    Internet connection for initial setup

Customization

    Edit device names, network interfaces, and Kismet configuration as needed.

    Add additional monitoring tools or scripts for advanced deployments.

    Integrate with your organization's monitoring/alerting pipeline if required.

Troubleshooting

    Kismet Not Starting:
    Check systemctl status kismet or Kismet logs in /var/log/.

    WiFi Adapter Issues:
    Ensure your adapter supports monitor mode and drivers are installed.

    Network Issues:
    Verify static IP or WiFi credentials in the YAML file.
