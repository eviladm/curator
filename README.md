# ansible curator with config_encoder_filters

An Ansible Role that installs [Elasticsearch Curator](https://github.com/elasticsearch/curator) on RedHat/CentOS or Debian/Ubuntu.
The role incorporates Config Encoder Filter by [Jiri Tyr] (https://github.com/jtyr/ansible-config_encoder_filters)
This role is based on [Jeff Geerling](https://www.jeffgeerling.com/), geerlingguy.elasticsearch-curator role, and works with new versions

## Requirements

On RedHat/CentOS, make sure you have the EPEL repository configured, so the `python-pip` package can be installed. You can install the EPEL repo by simply adding `geerlingguy.repo-epel` to your playbook's roles.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    elasticsearch_curator_cron_jobs:
      - {
        name: "Delete old elasticsearch indices.",
        job: "/usr/local/bin/curator delete --older-than 30",
        minute: "0",
        hour: "1"
      }
      - {
        name: "Close old elasticsearch indices.",
        job: "/usr/local/bin/curator close --older-than 14",
        minute: "30",
        hour: "1"
      }

curator.yml and actionfile.yml config can be changed using /vars/vars.yml using yaml encoder for CEF


	actionfile_config:
	  section1:
	    option11: value11
	    option12: value12
	curator_config:
	  section1:
	    option11: value11
	    option12: value12


## Dependencies

  - geerlingguy.repo-epel (RedHat/CentOS only)

## Example Playbook

    - hosts: search
      roles:
        - { role: curator }

## License

MIT / BSD

## Author Information

This role was created in 2018 by [Sascha Kain](https://github.com/eviladm)
