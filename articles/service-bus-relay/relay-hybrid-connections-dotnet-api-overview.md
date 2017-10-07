---
title: "aaaOverview hello standardowych interfejsów API Azure przekazywania .NET | Dokumentacja firmy Microsoft"
description: "Przekazywania omówienie standardowy interfejs API .NET"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: c90e00e809bd44eb0fbbff5eb03dfc8afa486523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a>Omówienie usługi Azure API standardowe .NET połączeń hybrydowych przekazywania

Ten artykuł zawiera podsumowanie klucza hello Azure przekazywania hybrydowego połączenia .NET Standard [interfejsów API klienta](/dotnet/api/microsoft.azure.relay).
  
## <a name="relay-connection-string-builder"></a>Konstruktor ciągów połączenia przekaźnika

Witaj [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] klasy formatuje parametry połączenia, które są określone tooRelay połączeń hybrydowych było możliwe. Można użyć jej tooverify hello formatu ciągu połączenia lub toobuild ciąg połączenia od początku. Zobacz hello następującego kodu, na przykład:

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of hello Hybrid Connection}";
var sharedAccessKeyName = "{SAS key name}";
var sharedAccessKey = "{SAS key value}";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

Można również przekazać połączenie bezpośrednio ciągu toohello `RelayConnectionStringBuilder` metody. Ta operacja pozwala tooverify, który hello ciągu połączenia jest w nieprawidłowym formacie. Jeśli którekolwiek z parametrów hello są nieprawidłowe, generuje konstruktora hello `ArgumentException`.

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare hello connectionStringBuilder so that it can be used outside of hello loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create hello connectionStringBuilder using hello supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a>Strumień połączenia hybrydowego
Witaj [HybridConnectionStream] [ HCStream] klasy jest toosend obiekt podstawowy używany hello i odbieranie danych z punktem końcowym przekaźnika usługi Azure, czy użytkownik pracuje z [HybridConnectionClient] [ HCClient], lub [HybridConnectionListener][HCListener].

### <a name="getting-a-hybrid-connection-stream"></a>Pobieranie strumienia połączenia hybrydowego

#### <a name="listener"></a>Odbiornik
Przy użyciu [HybridConnectionListener][HCListener], możesz uzyskać `HybridConnectionStream` obiektów w następujący sposób:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a>Klient
Przy użyciu [HybridConnectionClient][HCClient], możesz uzyskać `HybridConnectionStream` obiektów w następujący sposób:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a>Odbieranie danych
Witaj [HybridConnectionStream] [ HCStream] klasa umożliwia komunikację dwukierunkową. W większości przypadków stale pojawi się ze strumienia hello. Podczas czytania tekst ze strumienia hello, można również toouse [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) obiektu, który umożliwia łatwiejsze analizowania hello danych. Na przykład mogą odczytywać dane jako tekst, a nie jako `byte[]`.

Witaj następujący kod odczytuje poszczególnych wierszy tekstu ze strumienia hello dopóki żądanie anulowania:

```csharp
// Create a CancellationToken, so that we can cancel hello while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from hello 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of hello processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a>Wysyłanie danych
Po połączeniu, możesz wysłać punktu końcowego przekazywania toohello wiadomości. Ponieważ obiekt połączenia hello dziedziczy [strumienia](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), wysyłania danych jako `byte[]`. powitania po przykładzie pokazano, jak toodo to:

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

Jednak jeśli toosend tekst bezpośrednio, bez konieczności ciąg hello tooencode każdorazowo, można zawijać hello `hybridConnectionStream` obiekt z [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) obiektu.

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat przekaźnika usługi Azure, odwiedź te linki:

* [Odwołanie Microsoft.Azure.Relay](/dotnet/api/microsoft.azure.relay)
* [Co to jest usługa Azure Relay?](relay-what-is-it.md)
* [Interfejsy API dostępne przekazywania](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener