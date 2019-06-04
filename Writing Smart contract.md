# Writing Smart contract 

aelf defines smart contracts through the GROTO protobuf service description file, which implements a smart contract environment that as good as a GRPC Server.

## Hello World Smart Contract Explaination

Simplified directory structure

```bash
.
├── AElf.Boilerplate.sln
├── protobuf
│   ├── hello_world.proto
├── src
│   ├── AElf.Boilerplate.Launcher
│   │   ├── bin
│   │   │   └── Debug
│   │   │       └── netcoreapp2.2
│   │   │           ├── AElf.Boilerplate.Launcher.dll
│   └── HelloWorldContract
│   │   ├── bin
│   │   │   └── Debug
│   │   │       └── netcoreapp2.2
│   │   │           ├── HelloWorldContract.dll
│       ├── HelloWorldContract.cs
│       ├── HelloWorldContract.csproj
```

### 1. In protobuf/hello_world.proto

    The corresponding rpc method is defined by the service, and the data format is defined by the message. More information can be found in the ```protobuf``` documentation.

### 2. In src/HelloWorldContract

     The corresponding protobuf file is referenced in ```HelloWorldContract.csproj.```

     The specific contract logic is implemented in ```HelloWorldContract.cs.```

### 3.src/HelloWorldContract/bin/Debug/netcoreapp2.2/HelloWorldContract.dll

     This file is the file generated after ```dotnet build``` is executed.

     In the Boilerplate template, when dotnet runs, it is automatically posted to the chain we started.

     If you need to publish your contract to other blockchain networks which based on AELF system, you only need to publish the corresponding dll.

### 4. Code Explanation

```protobuf
// definition of protobuf
Syntax = "proto3";

Import "aelf_options.proto";
Import "google/protobuf/empty.proto";

option csharp_namespace = "HelloWorldContract";

service HelloWorldContract {

    option (aelf.csharp_state) = "HelloWorldContractState";

    // defines the method of the contract, and the return of the method
     Rpc Hello (google.protobuf.Empty) returns (HelloReturn) { }
}

/ / Define the data format of the returned data
Message HelloReturn {
     String Value = 1;
}
```

```C#
// Logic implementation in C#
Using Google.Protobuf.WellKnownTypes;

Namespace HelloWorldContract
{
     Public partial class HelloWorldContract : HelloWorldContractContainer.HelloWorldContractBase
     {
         Public override HelloReturn Hello(Empty input)
         {
             Return new HelloReturn {Value = "Hello world!"};
         }
}
```

## Adding Contract Method Tutorial

We add an ```Add``` method, enter two integer parameters ```a``` and ```b``` to output ```a + b```

### 1. Methods for addiung definitions and definitions for different data type in ```hello_world.proto file``` file

```proto
Syntax = "proto3";

Import "aelf_options.proto";
Import "google/protobuf/empty.proto";

Option csharp_namespace = "HelloWorldContract";

Service HelloWorldContract {

     Option (aelf.csharp_state) = "HelloWorldContractState";

     Rpc Hello (google.protobuf.Empty) returns (HelloReturn) { }

     Rpc Add (AddInput) returns (AddOutput) { }
}

Message HelloReturn {
     String Value = 1;
}


Message AddInput {
     Sint64 A = 1;
     Sint64 B = 2;
}

// AddOutpu definition
Message AddOutput {
     Sint64 Value = 1;
}
```
### 2. Add new logic to ``` HelloWorldContract.cs```

```C#
Using Google.Protobuf.WellKnownTypes;

Namespace HelloWorldContract
{
     Public partial class HelloWorldContract : HelloWorldContractContainer.HelloWorldContractBase
     {
         Public override HelloReturn Hello(Empty input)
         {
             Return new HelloReturn {Value = "Hello world!"};
         }

         Public override AddOutput Add(AddInput input) {
             Return new AddOutput {Value = input.A + input.B};
         }
     }
}
```

### 3. Recompile and start the chain

Execute dotnet build at ```src/AElf.Boilerplate.Launcher``` to complete compilation

Dotnet run ```bin/Debug/netcoreapp2.2/AElf.Boilerplate.Launcher```

The new contract will be automatically published to the chain.

### 4. Use the new contract through the JS file

```bash
Cd web/JSSDK
# Execute node, enter the command line interface of nodejs
Node
```

Enter the following js input
```js
const AElf = require('aelf-sdk');
const Wallet = AElf.wallet;
const sha256 = AElf.utils.sha256;

// address: 65dDNxzcd35jESiidFXN5JV8Z7pCwaFnepuYQToNefSgqk9
const defaultPrivateKey = 'bdb3b39ef4cd18c2697a920eb6d9e8c3cf1a930570beb37d04fb52400092c42b';

const wallet = Wallet.getWalletByPrivateKey(defaultPrivateKey);
const aelf = new AElf(new AElf.providers.HttpProvider(
    'http://127.0.0.1:1235/chain',
    null,
    null,
    null,
    [{
        name: 'Accept',
        value: 'text/plain;v=1.0'
    }]
));

const helloWorldContractName = 'HelloWorldContract';
const {
    GenesisContractAddress
} = aelf.chain.getChainStatus();
const zeroC = aelf.chain.contractAt(GenesisContractAddress, wallet);
const helloWorldContractAddress = zeroC.GetContractAddressByName.call(sha256(helloWorldContractName));
const helloWorldC = aelf.chain.contractAt(helloWorldContractAddress, wallet);


helloWorldC.Add.call({A: 1, B:3}, (error, result) => {console.log(error, result);})
```

Wait a second to see the result

```js
null { Value: '4' }
```

If you can't see the result, check the following:

1. Confirm that the compilation was successful.

2. Confirm that the chain is running.

3. Confirm that JS code entered correctly.
