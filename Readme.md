# systemd-screenlock

## Description

This is a collection of systemd service files and programs which enable a user
to automatically let systemd lock its X session when it goes to sleep.


## Usage

To use it one just has to activate two simple systemd services.

1. The system service which is activated by the sleep target and sends a lock message
   to all active sessions.

   ```bash
   systemctl enable screenlock.service
   ```

2. The user service waiting for the lock message and actually locking the screen.

   ```bash
   systemctl --user enable lock-forward@slimlock.service
   ```

   Therefore it is necessary that your systemd user session knowns the XDG_SESSION_ID
   and the DISPLAY environment variables.

   Alternatively, one could also simply start the lock-forward tool directly when the
   user logs in.

   ```bash
   lock-forward slimlock
   ```

### Combine with manual locking

Some screen locker are not able to properly determine that the screen is already locked.
Hence, if you already locked your screen manually and later put your computer to sleep,
it will be locked twice. To prevent such an annoyance, it is also possible to use the
lock-forward program to manually lock the screen. By using the following command, 
lock-forward will properly lock your screen if it is not yet locked, as well as make sure
that it is not locked later when the computer goes to sleep.

```bash
lock-now
```
