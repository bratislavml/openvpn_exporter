# Prometheus OpenVPN exporter

This repository provides code for a simple Prometheus metrics exporter
for [OpenVPN](https://openvpn.net/). Right now it can parse files
generated by OpenVPN's `--status`, having one of the following formats:

* Client statistics,
* Server statistics with `--status-version 2` (comma delimited),
* Server statistics with `--status-version 3` (tab delimited).

As it is not uncommon to run multiple instances of OpenVPN on a single
system (e.g., multiple servers, multiple clients or a mixture of both),
this exporter can be configured to scrape and export the status of
multiple status files, using the `-openvpn.status_paths` command line
flag. Paths need to be comma separated.

Please refer to this utility's `main()` function for a full list of
supported command line flags.

## Client statistics

For clients status files, the exporter generates metrics that may look
like this:

```
openvpn_client_auth_read_bytes_total{status_path="..."} 3.08854782e+08
openvpn_client_post_compress_bytes_total{status_path="..."} 4.5446864e+07
openvpn_client_post_decompress_bytes_total{status_path="..."} 2.16965355e+08
openvpn_client_pre_compress_bytes_total{status_path="..."} 4.538819e+07
openvpn_client_pre_decompress_bytes_total{status_path="..."} 1.62596168e+08
openvpn_client_tcp_udp_read_bytes_total{status_path="..."} 2.92806201e+08
openvpn_client_tcp_udp_write_bytes_total{status_path="..."} 1.97558969e+08
openvpn_client_tun_tap_read_bytes_total{status_path="..."} 1.53789941e+08
openvpn_client_tun_tap_write_bytes_total{status_path="..."} 3.08764078e+08
openvpn_status_update_time_seconds{status_path="..."} 1.490092749e+09
openvpn_up{status_path="..."} 1
```

## Server statistics

For server status files (both version 2 and 3), the exporter generates
metrics that may look like this:

```
openvpn_server_clients{status_path="..."} 5
openvpn_server_routes{status_path="..."} 5
openvpn_status_update_time_seconds{status_path="..."} 1.490089154e+09
openvpn_up{status_path="..."} 1
```
