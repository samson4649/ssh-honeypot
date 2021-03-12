FROM alpine:3.9
EXPOSE 2222

RUN apk add --no-cache openssh \
	&& sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
	&& echo "root:root" | chpasswd

RUN echo -e '#!/bin/ash\n\nssh-keygen -A\n/usr/sbin/sshd -D -p 2222 -e "$@"' > /init \
	&& echo -e "\n#####################################################\n\nUNAUTHORIZED ACCESS TO THIS DEVICE IS PROHIBITED\nYou must have explicit, authorized permission to access or configure this device.\nUnauthorized attempts and actions to access or use this system may result in civil and/or \ncriminal penalties.\nAll activities performed on this device are logged and monitored.\n\n#####################################################\n" > /etc/motd

RUN chmod 555 /init

ENTRYPOINT ["/init"]
