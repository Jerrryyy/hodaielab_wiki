---
title: Compute Resources
parent: Computing
---

# Local workstations

In the lab, everyone has their own workstation. Transfer of files (via `scp` / `rsync`)
or terminal connection (via `ssh`) is usually activated. For easy connection,
the IP address of each computer is mapped to a common name (e.g. *tn1.uhn*).
This mapping is defined in each computer through entries in the file `/etc/hosts`
making the mapped names available to all users of the computer. The mapped names can
be used in all bash commands instead of the corresponding IP addresses.

The current mapping looks as follows (check a particular computer for the IP addresses):

```bash
# Daniel's computer
XXX.XXX.XXX.XXX     tn1.uhn

# Nok's computer
XXX.XXX.XXX.XXX	    tn2.uhn

# Jonah's computer
XXX.XXX.XXX.XXX     tn3.uhn
XXX.XXX.XXX.XXX     backup_server.hodaielab

# Peter's computer
XXX.XXX.XXX.XXX	    tn4.uhn

# Matt's computer
XXX.XXX.XXX.XXX     tn5.uhn

# Tim's computer
XXX.XXX.XXX.XXX     tn6.uhn

# Jerry's computer
XXX.XXX.XXX.XXX     tn7.uhn

# Tim's lambda computer
XXX.XXX.XXX.XXX     tn8.uhn
```

# Scinet compute clusters

TBD (@Tim)

 * niagara
 * mist
 * data storage
   * $HOME
   * $SCRATCH
   * $PROJECT (we don't have that atm)
