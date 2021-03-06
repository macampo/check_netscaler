# check_netscaler Nagios Plugin

A Nagios Plugin written for the Citrix NetScaler Application Delivery Controller. It's based on Perl and using the the NITRO REST API. No need for SNMP.

Currently the plugin has three different modes:

- **check_state:** check the current service state of vservers, servicegroups and services

- **check_threshold:** check system values like cpu/disk/ram usage by a threshold

- **check_string:** check system values to match for a specific string

This plugin works with VPX, MPX and SDX NetScaler Appliances. The api responses differ by appliance type and your installed license.

The plugin is in alpha state and feedback and feature requests are appreciated. Performance data and grahing will be shipped in a later version of this plugin.

The Nitro.pm by Citrix (released under the Apache License 2.0) is required for using this plugin.

# Installation

On a CentOS/RHEL machine execute the following commands to install all Perl dependencies (Nagios::Plugin, LWP, JSON):

    yum install perl-libwww-perl perl-JSON perl-Nagios-Plugin

Copy the Nitro.pm in the same directory as the check_netscaler.pl file or copy it to you @INC (include path).

# Known Issues

- Error Handling/Execption Handling
- Performance data not implemented yet

# Usage Examples

    NetScaler::VPNvServer::State
    ./check_netscaler.pl -H  192.168.100.100 -U nsroot -P nsroot -C check_vserver -I vpnvserver

    NetScaler::LBvServer::State
    ./check_netscaler.pl -H  192.168.100.100 -U nsroot -P nsroot-C check_vserver -I lbvserver

    NetScaler::System::Memory
    ./check_netscaler.pl -H  192.168.100.100 -U nsroot -P nsroot -C check_threshold_above -I system -F memusagepcnt -w 75 -c 80

    NetScaler::System::CPU
    ./check_netscaler.pl -H  192.168.100.100 -U nsroot -P nsroot -C check_threshold_above -I system -F cpuusagepcnt -w 75 -c 80

    NetScaler::System::CPU::MGMT
    ./check_netscaler.pl -H  192.168.100.100 -U nsroot -P nsroot -C check_threshold_above -I system -F mgmtcpuusagepcnt -w 75 -c 80

    NetScaler::System::Disk0
    ./check_netscaler.pl -H  192.168.100.100 -U nsroot -P nsroot -C check_threshold_above -I system -F disk0perusage -w 75 -c 80

    NetScaler::System::Disk1
    ./check_netscaler.pl -H  192.168.100.100 -U nsroot -P nsroot -C check_threshold_above -I system -F disk1perusage -w 75 -c 80

    NetScaler::HA::Status
    ./check_netscaler.pl -H  192.168.100.100 -U nsroot -P nsroot -C check_string_not -I hanode -F hacurstatus -w YES -c YES

    NetScaler::HA::State
    ./check_netscaler.pl -H  192.168.100.100 -U nsroot -P nsroot -C check_string_not -I hanode -F hacurstate -w UP -c UP

# API Documentation

You will find a full documentation about the NITRO API on your NetScaler Appliance in the "Download" area.

http://NSIP/nitro-rest.tgz (where NSIP is the IP address of your NetScaler appliance). 

# Tested Firmware

Tested with NetScaler 11 Build 64.34.
