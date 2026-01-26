## The at command
The at utility allows you to schedule a one-time task for a specific hour or time. For Ubuntu/Debian/Mint systems:

```bash
sudo apt update && sudo apt install at
sudo systemctl enable --now atd
```
And then we can use it like this:

```bash
echo "your-command" | at 3:00pm
```

or
```bash
echo "your-command" | at now + 1 hour
```
example:

```bash
echo "rm -r testdir/" | at 03:00 tomorrow
```

to list all the jobs that will be running, we can use this handy command:

```bash
for j in $(atq | sort -k6,6 -k3,3M -k4,4 -k5,5 |cut -f 1); do atq |grep -P "^$j\t" ;at -c "$j" | tail -n 2; done
```

This command retrieves the list of pending tasks (atq) and sorts them chronologically by year, month, day, and time, and displays the entire script that will be executed.

