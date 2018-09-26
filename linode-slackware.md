# Linode Slackware

For setting up Slackware 14.2 on Linode.

## Change hostname

    vi /etc/HOSTNAME

## Add user

    adduser jmp
    usermod -a -G wheel jmp

## Upgrade the system

    slackpkg update gpg
    slackpkg update
    slackpkg install-new
    slackpkg upgrade-all
    slackpkg clean-system

## Make Vim work

    slackpkg install perl python

## Secure SSH

    echo "Port 4242" >> /etc/ssh/sshd_config
    echo "PermitRootLogin no" >> /etc/ssh/sshd_config

## Install Apache

    slackpkg install httpd sqlite
    chmod 755 /etc/rc.d/rc.httpd
    /etc/rc.d/rc.httpd start

## Configure Apache

Modify `ServerName`:

    vim /etc/httpd/httpd.conf
