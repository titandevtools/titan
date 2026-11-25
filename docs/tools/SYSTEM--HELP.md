## 39. `titan system` — Native Windows Environment, Hardware, Disk, Network & Process Inspector

### Verbatim Help Manual
```text
Usage: titan system <command> [arguments] [-j|--json]

Commands:
  titan system --env                            List environment variables of the current process
  titan system --env-user                       List persistent user environment variables
  titan system --env-system                     List persistent system environment variables
  titan system --env-get NAME                   Print the value of one variable
  titan system --env-set NAME VALUE [--system]  Set a persistent variable (user scope by default)
  titan system --env-delete NAME [--system]     Delete a persistent variable
  titan system --env-search TEXT                Search names and values of the current environment
  titan system --path                           Show PATH entries with existence and duplicate checks
  titan system --info                           System summary
  titan system --about                          About this tool
  titan system --version                        Print the version
  titan system --os                             Operating system details
  titan system --hostname                       Computer names
  titan system --user                           Current user
  titan system --admin                          Check whether the process is elevated
  titan system --uptime                         Time since boot
  titan system --time                           Local and UTC time
  titan system --timezone                       Time zone details
  titan system --locale                         Locale and code pages
  titan system --cpu                            Processor details
  titan system --gpu                            Display adapters
  titan system --memory                         Memory usage
  titan system --bios                           BIOS and system identity
  titan system --board                          Motherboard details
  titan system --battery                        Battery status
  titan system --power                          Power source and active power plan
  titan system --screen                         Monitors and resolutions
  titan system --disk DRIVE                     Details of one drive, e.g. --disk "C:"
  titan system --disks                          All drives
  titan system --folders                        Well-known folder locations
  titan system --temp                           Temp folder path, file count and size
  titan system --network                        Network adapters and addresses
  titan system --ports                          Listening TCP ports and bound UDP ports
  titan system --processes [FILTER]             Running processes
  titan system --kill PID                       Terminate a process
  titan system --services [FILTER]              Windows services
  titan system --drivers [FILTER]               Kernel and file system drivers
  titan system --startup                        Startup programs
  titan system --installed [FILTER]             Installed applications
```

### Practical Examples
```powershell
titan system --info -j
titan system --path
titan system --disk "C:"
titan system --ports
titan system --env-set MY_VAR "value"
titan system --env-delete MY_VAR
```
