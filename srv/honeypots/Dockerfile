FROM alpine
EXPOSE 2222

RUN apk add --no-cache openssh \
	&& sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
	&& echo "root:root" | chpasswd

RUN echo -e '#!/bin/ash\n\nssh-keygen -A\n/usr/sbin/sshd -D -p 2222 -e "$@"' > /entrypoint.sh
RUN chmod 555 /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
