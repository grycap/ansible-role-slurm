[![License](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)
[![Build Status](https://travis-ci.org/grycap/ansible-role-slurm.svg?branch=master)](https://travis-ci.org/grycap/ansible-role-slurm)

SLURM cluster Role
=======================

Install [SLURM cluster](http://slurm.schedmd.com/).

Role Variables
--------------

The variables that can be passed to this role and a brief description about them are as follows.

	# SLURM version to install (in case of RH systems)
	slurm_version: 14.11.3
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
	# Default ssh user
	user: user1

Example Playbook
----------------

This an example of how to install a SLURM cluster:

    - hosts: server
      roles:
      - { role: 'grycap.slurm', slurm_type_of_node: 'front', slurm_server_ip: '{{ansible_default_ipv4}}', slurm_wn_nodenames: "{{ groups['wns']|map('extract', hostvars, 'ansible_hostname')|list }}" }

    - hosts: wns
      roles:
      - { role: 'grycap.slurm', slurm_type_of_node: 'wn', slurm_server_ip: "{{hostvars['server']['ansible_default_ipv4']}}" }

Contributing to the role
========================
In order to keep the code clean, pushing changes to the master branch has been disabled. If you want to contribute, you have to create a branch, upload your changes and then create a pull request.  
Thanks
