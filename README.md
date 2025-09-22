Are you tired of fake-time or other tools that handle synching your clock with the target lab? 

Please place this script into /usr/bin or another directory in sudo secure_path, don't forget to chmod +x the file after creation 

Usage:

  sudo lab-time LAB_IP

  sudo lab-time stop

  sudo lab-time status

  sudo lab-time -h | --help

What it does:
  1. Writes an override file at /etc/systemd/timesyncd.conf.d/90-lab-time.conf
     with your lab DC as the only NTP source.
  2. Restarts systemd-timesyncd and enables NTP.
  3. If available, runs: ntpdate -u <DC> to step the clock immediately.
  4. "stop" removes the override and restarts timesyncd so defaults resume.

Examples:
  sudo lab-time 10.8.10.160     Start syncing to the DC at 10.8.10.160

  sudo lab-time status            Show current source and last sync time

  sudo lab-time stop              Return to system defaults

Safety:
  This simple script does not back up custom timesync settings. On stop it
  deletes only the lab override and timesyncd falls back to distro defaults.
