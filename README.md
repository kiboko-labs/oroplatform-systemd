Use OroPlatform with systemd
============================

Marello
-------

Write this into `/etc/init.d/marello` file

```bash
#!/bin/sh -e

### BEGIN INIT INFO
# Provides:          marello
# Required-Start:    $local_fs $remote_fs $network $syslog $named $nginx
# Required-Stop:     $local_fs $remote_fs $network $syslog $named $nginx
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: starts the marello message queue consumer
# Description:       starts marello message queue consumer using start-stop-daemon
### END INIT INFO

DAEMON="/home/marello/htdocs/app/console"
DAEMON_OPT="oro:message-queue:consume --env prod"
DAEMON_USER="marello"
DAEMON_NAME="marello"

PATH="/sbin:/bin:/usr/sbin:/usr/bin"

if [ ! -x $DAEMON ]
then
    exit 0
fi

. /lib/lsb/init-functions

d_start () {
    log_daemon_msg "Starting system $DAEMON_NAME Daemon"
    start-stop-daemon --background --name $DAEMON_NAME --start --quiet --chuid $DAEMON_USER --exec $DAEMON -- $DAEMON_OPT
    log_end_msg $?
}

d_stop () {
    log_daemon_msg "Stopping system $DAEMON_NAME Daemon"
    start-stop-daemon --name $DAEMON_NAME --stop --retry 5 --quiet
    log_end_msg $?
}

case "$1" in
        start|stop)
                d_${1}
                ;;

        restart|reload|force-reload)
                d_stop
                d_start
                ;;

        force-stop)
                d_stop
                killall -q $DAEMON_NAME || true
                sleep 2
                killall -q -9 $DAEMON_NAME || true

                ;;

        status)
                status_of_proc "$DAEMON_NAME" "$DAEMON" "system-wide $DAEMON_NAME" && exit 0 || exit $?
                ;;
        *)
                echo "Usage: /etc/init.d/$DAEMON_NAME {start|stop|force-stop|restart|reload|force-reload|status}"
                exit 1
                ;;
esac
exit 0
```

Then run 

```bash
chmod +x /etc/init.d/marello
systemctl enable marello.service
```

OroCRM
-------

Write this into `/etc/init.d/orocrm` file

```bash
#!/bin/sh -e

### BEGIN INIT INFO
# Provides:          orocrm
# Required-Start:    $local_fs $remote_fs $network $syslog $named $nginx
# Required-Stop:     $local_fs $remote_fs $network $syslog $named $nginx
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: starts the orocrm message queue consumer
# Description:       starts orocrm message queue consumer using start-stop-daemon
### END INIT INFO

DAEMON="/home/orocrm/htdocs/app/console"
DAEMON_OPT="oro:message-queue:consume --env prod"
DAEMON_USER="orocrm"
DAEMON_NAME="orocrm"

PATH="/sbin:/bin:/usr/sbin:/usr/bin"

if [ ! -x $DAEMON ]
then
    exit 0
fi

. /lib/lsb/init-functions

d_start () {
    log_daemon_msg "Starting system $DAEMON_NAME Daemon"
    start-stop-daemon --background --name $DAEMON_NAME --start --quiet --chuid $DAEMON_USER --exec $DAEMON -- $DAEMON_OPT
    log_end_msg $?
}

d_stop () {
    log_daemon_msg "Stopping system $DAEMON_NAME Daemon"
    start-stop-daemon --name $DAEMON_NAME --stop --retry 5 --quiet
    log_end_msg $?
}

case "$1" in
        start|stop)
                d_${1}
                ;;

        restart|reload|force-reload)
                d_stop
                d_start
                ;;

        force-stop)
                d_stop
                killall -q $DAEMON_NAME || true
                sleep 2
                killall -q -9 $DAEMON_NAME || true

                ;;

        status)
                status_of_proc "$DAEMON_NAME" "$DAEMON" "system-wide $DAEMON_NAME" && exit 0 || exit $?
                ;;
        *)
                echo "Usage: /etc/init.d/$DAEMON_NAME {start|stop|force-stop|restart|reload|force-reload|status}"
                exit 1
                ;;
esac
exit 0
```

Then run 

```bash
chmod +x /etc/init.d/orocrm
systemctl enable orocrm.service
```

OroCommerce
-------

Write this into `/etc/init.d/orocommerce` file

```bash
#!/bin/sh -e

### BEGIN INIT INFO
# Provides:          orocommerce
# Required-Start:    $local_fs $remote_fs $network $syslog $named $nginx
# Required-Stop:     $local_fs $remote_fs $network $syslog $named $nginx
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: starts the orocommerce message queue consumer
# Description:       starts orocommerce message queue consumer using start-stop-daemon
### END INIT INFO

DAEMON="/home/orocommerce/htdocs/app/console"
DAEMON_OPT="oro:message-queue:consume --env prod"
DAEMON_USER="orocommerce"
DAEMON_NAME="orocommerce"

PATH="/sbin:/bin:/usr/sbin:/usr/bin"

if [ ! -x $DAEMON ]
then
    exit 0
fi

. /lib/lsb/init-functions

d_start () {
    log_daemon_msg "Starting system $DAEMON_NAME Daemon"
    start-stop-daemon --background --name $DAEMON_NAME --start --quiet --chuid $DAEMON_USER --exec $DAEMON -- $DAEMON_OPT
    log_end_msg $?
}

d_stop () {
    log_daemon_msg "Stopping system $DAEMON_NAME Daemon"
    start-stop-daemon --name $DAEMON_NAME --stop --retry 5 --quiet
    log_end_msg $?
}

case "$1" in
        start|stop)
                d_${1}
                ;;

        restart|reload|force-reload)
                d_stop
                d_start
                ;;

        force-stop)
                d_stop
                killall -q $DAEMON_NAME || true
                sleep 2
                killall -q -9 $DAEMON_NAME || true

                ;;

        status)
                status_of_proc "$DAEMON_NAME" "$DAEMON" "system-wide $DAEMON_NAME" && exit 0 || exit $?
                ;;
        *)
                echo "Usage: /etc/init.d/$DAEMON_NAME {start|stop|force-stop|restart|reload|force-reload|status}"
                exit 1
                ;;
esac
exit 0
```

Then run 

```bash
chmod +x /etc/init.d/orocommerce
systemctl enable orocommerce.service
```
