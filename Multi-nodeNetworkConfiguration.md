# Multi-node Network Configuration

## Environment:

Need to install redis or SSDB

After clone it, copy the key in the keys directory to ```~/.local/share/aelf/keys/```

(For Windows environment, please copy to ```C:\Users\your account\AppData\Local\aelf\keys```)

## Build and Run

### Build

```bash
cd aelf-boilerplate/chain/src/AElf.Boilerplate.Launcher/
dotnet build
```
### Start the first node:

```bash
Cd aelf-boilerplate/chain/multi-node-config/configInfo/bp1
Dotnet ../../../src/AElf.Boilerplate.Launcher/bin/Debug/netcoreapp2.2/AElf.Boilerplate.Launcher.dll
```

### Create a new terminal to start the second node

```bash
Cd aelf-boilerplate/chain/multi-node-config/configInfo/bp1
Dotnet ../../../src/AElf.Boilerplate.Launcher/bin/Debug/netcoreapp2.2/AElf.Boilerplate.Launcher.dll
```

### Create a new terminal to start the third node

```bash
Cd aelf-boilerplate/chain/multi-node-config/configInfo/bp1
Dotnet ../../../src/AElf.Boilerplate.Launcher/bin/Debug/netcoreapp2.2/AElf.Boilerplate.Launcher.dll
```
