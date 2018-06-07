# prebellico
Passive internal reconnaissance tool

Prebellico in its simplest form is a 100% passive network reconnissiance tool designed to gather as much information about the target environment without transmission. Execution is simple. Simply launch Prebellico with python as a root user at startup or within a GNU Screen session and the information it gathers will be dumped to the screen as well as logged within a specific location. By default Prebellio will only operate in a 100% passive state, while working to ignore traffic generated by the sniffing interface. If more specific functionality is desired, simply leverage the various options built into Prebellico:

usage: prebellico.py.beta [-h] [-i INF] [-f FILE] [-l LOG] [-d DB] [-e EXTRA]
                          [-t TARGETS] [-w WAIT] [-s] [-p] [-a] [-q]

optional arguments:
  -h, --help            show this help message and exit
  -i INF, --inf INF     Specify the interface you want Prebellico to listen
                        on. By default Prebellico will hunt for interfaces and
                        ask the user to specify an interface if one is not
                        provided here.
  -f FILE, --file FILE  Specify a PCAP file to read from instead of a network
                        interface. By default Prebellico assumes that traffic
                        is to be read from a network interface.
  -l LOG, --log LOG     Specify an output file. By default Prebellico will log
                        to "prebellico.out" if a logfile is not specified.
  -d DB, --db DB        Specify an sqlite db file you want to write to. By
                        default this will create, if need be, and write to
                        "prebellico.db" if not specified by the user, as long
                        as the file is an actual Prebellico DB that the user
                        can read from.
  -e EXTRA, --extra EXTRA
                        Specify extra filtering using PCAP based syntax. By
                        default, "ip or arp or aarp and not host 0.0.0.0 and
                        not host <interface_IP>" is used as a filter.
  -t TARGETS, --targets TARGETS
                        Specify targets of interest.
  -w WAIT, --wait WAIT  Specify a period of time in hours to wait for new
                        intelligence before shifting to a new form of
                        intelligence gathering.
  -s, --subsume         Include traffic from the target interface from
                        Prebellico output. By default this traffic is excluded
                        to ensure data generated by the interface while
                        interacting with the environment does not taint the
                        "fingerprint" of the target environment.
  -p, --semipassive     Perform semi-passive data collection after a specified
                        period of time where no new passive intelligence is
                        aquired.
  -a, --semiaggressive  Perform semi-aggressive data collection after a
                        specififed period of time where no new passive or
                        semi-passive intelligence is aquired.
  -q, --quiet           Remove the Prebellico banner at the start of the
                        script.

Note that Prebellico has the ability to process a PCAP file with a maximum SNAPLEN of 262144 bytes prior to an engagement. This is useful for things like processing historical data obtained elsewhere or for scope validation purposes prior to engagement kickoff. You can also merge this data during the engagement by copying the database over and specifying the database and logfile at launch time, if so desired.

Soon prebellico will start to track the time between intelligence updates, and if so desired, work to move into a semi-passive mode after a user defined period of lack of intelligence, or after a specific period, leveraging the information it has obtained to further enumerate resources within the environment.

Prebellico also has the ability to understand what is permitted within the environment from network egress point. Eventually Prebellico, if told to do so, will leverage this information and establish a C2 connection using observed egress patters to report back to a listener the information it knows about a network.
