# Linode Slackware

For setting up Slackware 14.2 on Linode.

## Installation

### Booting the installer

    boot: ↵
    Enter 1 to select keyboard map: 1↵         Select keyboard map
    Select “qwerty/fi.map” and press ↵.
    Type 1↵ to confirm keymap.
    slackware login: root↵                     Log in as root (no password)

### Partitioning the hard disk

    # fdisk /dev/sda↵
    Command (m for help): g↵                   Changes disk label to GPT
    Creating the boot partition
    Command (m for help): n↵
    Partition number: ↵
    First sector: ↵
    Last sector: +260M↵
    Command (m for help): t↵
    Hex code (type L to list all codes): 1↵

### Creating the swap partition

    Command (m for help): n↵
    Partition number: ↵
    First sector: ↵
    Last sector: +1G↵
    Command (m for help): t↵
    Partition number (1, 2, default 2): ↵
    Hex code (type L to list all codes): 19↵   Linux swap

### Creating the root partition

    Command (m for help): n↵
    Partition number: ↵
    First sector: ↵
    Last sector: ↵

### Writing partition changes to disk

    Command (m for help): w↵

### Running setup

    # setup
    a↵                     Set up swap partition
    Ok↵
    No↵                    Don’t check for bad blocks.
    Ok↵                    Changes added to fstab
    Select↵                Select installation partition
    Format↵                Quick format
    Ext4↵
    Yes↵                   Format EFI partition /etc/sda1
    Install from CD/DVD


## Post-install configuration

### Change hostname

    vi /etc/HOSTNAME

### Add user

    adduser jmp
    usermod -a -G wheel jmp

### Upgrade the system

    slackpkg update gpg
    slackpkg update
    slackpkg install-new
    slackpkg upgrade-all
    slackpkg clean-system

### Make Vim work

    slackpkg install perl python

### Secure SSH

    echo "Port 4242" >> /etc/ssh/sshd_config
    echo "PermitRootLogin no" >> /etc/ssh/sshd_config

### Install Apache

    slackpkg install httpd sqlite
    chmod 755 /etc/rc.d/rc.httpd
    /etc/rc.d/rc.httpd start

### Configure Apache

Modify `ServerName`:

    vim /etc/httpd/httpd.conf
