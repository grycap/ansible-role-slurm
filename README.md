[![License](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)
[![CI](https://github.com/grycap/ansible-role-slurm/actions/workflows/main.yaml/badge.svg)](https://github.com/grycap/ansible-role-slurm/actions/workflows/main.yaml)

SLURM cluster Role
=======================

Install [SLURM cluster](http://slurm.schedmd.com/).

Role Variables
--------------

The variables that can be passed to this role and a brief description about them are as follows.

	# SLURM version to install (in case of RH systems)
	slurm_version: 20.02.7
	# List of servers to download the slurm code
	slurm_mirrors: [ "http://ftpgrycap.i3m.upv.es/src/", "https://download.schedmd.com/slurm/" ]
	# Type of node to install: front or wn
	slurm_type_of_node: front
	# Name of the SLURM server
	slurm_server_name: slurmserver
	# IP address of the SLURM server
	slurm_server_ip: 127.0.0.1
	# Prefix to set to the SLURM working nodes
	slurm_vnode_prefix: vnode-
	# List of the names of the WNs
	slurm_wn_nodenames: []
	# Number of CPUs of the WNs
	slurm_wn_cpus: 1
	# Amount of memory of the WNs (in MB, see RealMemory). If 0 it is not set
	slurm_wn_mem: 0
	# GRES specification for the WN
	slurm_wn_gres: ""
	# GRES types specification for the WN
	slurm_wn_gres_tpes: ""
	# GRES conf data file
	slurm_wn_gres_conf: "AutoDetect=nvml"
	# Default user for ssh and slurm management
	# Default ssh user
	user: user1
	# Install DRMAA library
	drmaa_lib_install: false
	drmaa_lib_version: 1.0.7
	# SLURM default configuration options
	slurm_default_conf_options:
		AuthType: auth/munge
		CryptoType: crypto/munge
		FirstJobId: 1
		JobRequeue: 0
		JobSubmitPlugins: all_partitions
		ProctrackType: proctrack/pgid
		ReturnToService: 2
		SlurmctldPidFile: /var/run/slurmctld.pid
		SlurmctldPort: 6817
		SlurmdPidFile: /var/run/slurmctld.pid
		SlurmdPort: 6818
		SlurmdSpoolDir: /var/spool/slurm
		SlurmUser: slurm
		StateSaveLocation: /var/slurm/checkpoint
		SwitchType: switch/none
		TaskPlugin: task/none
		InactiveLimit: 0
		KillWait: 30
		MessageTimeout: 30
		MinJobAge: 300
		SlurmctldTimeout: 30
		SlurmdTimeout: 40
		Waittime: 0
		FastSchedule: 1
		SchedulerType: sched/backfill
		SelectType: select/linear
		AccountingStorageType: accounting_storage/none
		ClusterName: cluster
		JobCompType: jobcomp/none
		JobAcctGatherFrequency: 30
		JobAcctGatherType: jobacct_gather/none
		SlurmctldDebug: debug5
		SlurmctldLogFile: /var/log/slurm/slurmctld.log
		SlurmdDebug: debug5
		SlurmdLogFile: /var/log/slurm/slurmd.log
	# SLURM user configuration options
	slurm_conf_options: {}
	# SLURM configuration options for cgroup
	slurm_cgroup_conf_options:
		CgroupPlugin: cgroup/v1

Example Playbook
----------------

This an example of how to install a SLURM cluster:
```
  - hosts: server
  roles:
  - { role: 'grycap.slurm', slurm_type_of_node: 'front', slurm_server_ip: '{{ansible_default_ipv4}}', slurm_wn_nodenames: "{{ groups['wns']|map('extract', hostvars, 'ansible_hostname')|list }}" }
```
```
  - hosts: wns
  roles:
  - { role: 'grycap.slurm', slurm_type_of_node: 'wn', slurm_server_ip: "{{hostvars['server']['ansible_default_ipv4']}}" }
```
Contributing to the role
========================
In order to keep the code clean, pushing changes to the master branch has been disabled. If you want to contribute, you have to create a branch, upload your changes and then create a pull request.  
Thanks
