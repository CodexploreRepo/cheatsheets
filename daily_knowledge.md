# Daily Knowledge

## Day 1

### `scp` file transfer from one machine to another

- For example (transfer file from machine A to machine B):
  - Generate public & private key pairs, share the public key to Machine B, and Machine A will keep the private key
- `scp -i /location_in_machine_A/to/private/key -v -P 64022 file_path machineB@ip_address:/path/to/store/inB/`
  - `-i` Identity
  - `-v` verbose to debug
  - `-P` port (note P should be in captital letter)

### Curl

- `curl` is a command-line tool and library for transferring data with URLs.
- `curl -vvv telnet://hostname:port`
  - `-vvv`: This option increases the verbosity of curl output.
  - `telnet://hostname:port`: This part of the command specifies the URL to connect to. It tells `curl` to use the `Telnet` protocol to connect to the specified hostname and port.

### Telnet

Telnet is a network protocol and a command-line tool that allows you to remotely access and manage devices or systems over a network.

### Shell

- `ls -ltr`: This will display a detailed list of files and directories in the current directory, sorted by modification time, with the oldest entries listed first.
- `printenv` to print all the environment variables
- `echo $PATH` to print all the paths
- `unzip file.zip -d directory_path` to unzip a file
