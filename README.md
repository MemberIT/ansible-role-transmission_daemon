# ansible-role-transmission-daemon

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-transmission-daemon.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-transmission-daemon)

Linux - A fast, easy, and free bittorrent client 

## Requirements

This role requires that you have the epel repository installed, if RedHat.

 * https://galaxy.ansible.com/linuxhq/epel/

## Role Variables

Available variables are listed below, along with default values:

    td_alt_speed_down: 50
    td_alt_speed_enabled: false
    td_alt_speed_time_begin: 540
    td_alt_speed_time_day: 127
    td_alt_speed_time_enabled: false
    td_alt_speed_time_end: 1020
    td_alt_speed_up: 50
    td_bind_address_ipv4: '0.0.0.0'
    td_bind_address_ipv6: '::'
    td_blocklist_enabled: false
    td_blocklist_url: 'http://www.example.com/blocklist'
    td_cache_size_mb: 4
    td_dht_enabled: true
    td_download_dir: '/var/lib/transmission/Downloads'
    td_download_queue_enabled: true
    td_download_queue_size: 5
    td_encryption: 1
    td_groups: []
    td_idle_seeding_limit: 30
    td_idle_seeding_limit_enabled: false
    td_incomplete_dir: '/var/lib/transmission/Downloads'
    td_incomplete_dir_enabled: false
    td_lpd_enabled: false
    td_message_level: 1
    td_peer_congestion_algorithm: ''
    td_peer_id_ttl_hours: 6
    td_peer_limit_global: 200
    td_peer_limit_per_torrent: 50
    td_peer_port: 51413
    td_peer_port_random_high: 65535
    td_peer_port_random_low: 1024
    td_peer_port_random_on_start: false
    td_peer_socket_tos: 'default'
    td_pex_enabled: true
    td_port_forwarding_enabled: true
    td_preallocation: 1
    td_prefetch_enabled: true
    td_queue_stalled_enabled: true
    td_queue_stalled_minutes: 30
    td_ratio_limit: 2
    td_ratio_limit_enabled: false
    td_rename_partial_files: true
    td_rpc_authentication_required: true
    td_rpc_bind_address: '0.0.0.0'
    td_rpc_enabled: true
    td_rpc_host_whitelist: []
    td_rpc_host_whitelist_enabled: true
    td_rpc_password: '{81c0bf5837de960f693ce3df337bc5f30dce6ebezuTWtlG8'
    td_rpc_port: 9091
    td_rpc_url: '/transmission/'
    td_rpc_username: transmission
    td_rpc_whitelist: [ '127.0.0.1' ]
    td_rpc_whitelist_enabled: true
    td_scrape_paused_torrents_enabled: true
    td_script_torrent_done_enabled: false
    td_script_torrent_done_filename:
    td_seed_queue_enabled: false
    td_seed_queue_size: 10
    td_service_enabled: true
    td_speed_limit_down: 100
    td_speed_limit_down_enabled: false
    td_speed_limit_up: 100
    td_speed_limit_up_enabled: false
    td_start_added_torrents: true
    td_torrents: []
    td_trash_original_torrent_files: false
    td_umask: 18
    td_upload_slots_per_torrent: 14
    td_utp_enabled: true

By default, the transmission rpc password is 'transmission'

## Dependencies

None

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.transmission-daemon
          td_bind_address_ipv4: "{{ ansible_tun0.ipv4.address if ansible_tun0 is defined else ansible_default_ipv4.address }}"
          td_bind_address_ipv6: "fe80::"
          td_blocklist_enabled: true
          td_blocklist_url: 'http://john.bitsurge.net/public/biglist.p2p.gz'
          td_dht_enabled: false
          td_download_dir: /transmission/default
          td_groups:
            - couchpotato
            - medusa
          td_incomplete_dir: /transmission/default
          td_peer_port: "{{ td_peer_port_random_high|random(start=td_peer_port_random_low) }}"
          td_peer_port_random_on_start: true
          td_pex_enabled: false
          td_ratio_limit: 2
          td_ratio_limit_enabled: true
          td_rpc_authentication_required: false
          td_rpc_bind_address: "{{ ansible_default_ipv4.address }}"
          td_service_enabled: false
          td_speed_limit_down: 8000
          td_speed_limit_down_enabled: true
          td_rpc_whitelist:
            - 127.0.0.1
            - 192.168.0.*
          td_torrents:
            - http://centos.mirror.lstn.net/7/isos/x86_64/CentOS-7-x86_64-DVD-1708.torrent
            - http://centos.mirror.lstn.net/7/isos/x86_64/CentOS-7-x86_64-Everything-1708.torrent
            - http://centos.mirror.lstn.net/7/isos/x86_64/CentOS-7-x86_64-LiveGNOME-1708.torrent
            - http://centos.mirror.lstn.net/7/isos/x86_64/CentOS-7-x86_64-LiveKDE-1708.torrent
            - http://centos.mirror.lstn.net/7/isos/x86_64/CentOS-7-x86_64-Minimal-1708.torrent
            - http://centos.mirror.lstn.net/7/isos/x86_64/CentOS-7-x86_64-NetInstall-1708.torrent
          td_umask: 2

## License

Copyright (C) 2018 Taylor Kimball <tkimball@linuxhq.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>.
