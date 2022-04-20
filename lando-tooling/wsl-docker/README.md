# Xdebug in WSL Docker based Lando

# Introduction
Lando is way faster on windows when entirely within in WSL. However, that sometimes makes xdebug connections to IDEs
outside of WSL more challenging. This is mostly due to incorrectly reported IP addresses. For this reason instead of
relying on the autodetected IP address, I usually use thus custom [php.ini](php.ini) and [lando file](.lando.local.yml)
in combination with some custom start-up commands:

```
alias l-rebuild='z=`grep -E "[0-9.]{3,20}" /etc/resolv.conf -o` && sed -i "s/\b[0-9.]\{3,20\}\b/$z/" php.ini && lando rebuild -y'
alias l-start='z=`grep -E "[0-9.]{3,20}" /etc/resolv.conf -o` && sed -i "s/\b[0-9.]\{3,20\}\b/$z/" php.ini && lando start'
alias l-restart='z=`grep -E "[0-9.]{3,20}" /etc/resolv.conf -o` && sed -i "s/\b[0-9.]\{3,20\}\b/$z/" php.ini && lando restart -y'
```
