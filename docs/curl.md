# CURL command

## Introduction

- `curl` is a command-line tool and library for transferring data with URLs.
  - It supports these protocols: DICT, FILE, FTP, FTPS, GOPHER, GOPHERS, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, MQTT, POP3, POP3S, RTMP, RTMPS, RTSP, SCP, SFTP, SMB, SMBS, SMTP, SMTPS, TELNET or TFTP. The command is designed to work without user interaction.

## Command

- Download a file from Github: `curl -O <url_to_file>`
  - `-O` to perserve the original filename
- `curl -vvv telnet://hostname:port`
  - `-vvv`: This option increases the verbosity of curl output.
  - `telnet://hostname:port`: This part of the command specifies the URL to connect to. It tells `curl` to use the `Telnet` protocol to connect to the specified hostname and port.
