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
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="083ca-103">Omówienie usługi Azure API standardowe .NET połączeń hybrydowych przekazywania</span><span class="sxs-lookup"><span data-stu-id="083ca-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="083ca-104">Ten artykuł zawiera podsumowanie klucza hello Azure przekazywania hybrydowego połączenia .NET Standard [interfejsów API klienta](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="083ca-104">This article summarizes some of hello key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="083ca-105">Konstruktor ciągów połączenia przekaźnika</span><span class="sxs-lookup"><span data-stu-id="083ca-105">Relay Connection String Builder</span></span>

<span data-ttu-id="083ca-106">Witaj [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] klasy formatuje parametry połączenia, które są określone tooRelay połączeń hybrydowych było możliwe.</span><span class="sxs-lookup"><span data-stu-id="083ca-106">hello [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific tooRelay Hybrid Connections.</span></span> <span data-ttu-id="083ca-107">Można użyć jej tooverify hello formatu ciągu połączenia lub toobuild ciąg połączenia od początku.</span><span class="sxs-lookup"><span data-stu-id="083ca-107">You can use it tooverify hello format of a connection string, or toobuild a connection string from scratch.</span></span> <span data-ttu-id="083ca-108">Zobacz hello następującego kodu, na przykład:</span><span class="sxs-lookup"><span data-stu-id="083ca-108">See hello following code for an example:</span></span>

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

<span data-ttu-id="083ca-109">Można również przekazać połączenie bezpośrednio ciągu toohello `RelayConnectionStringBuilder` metody.</span><span class="sxs-lookup"><span data-stu-id="083ca-109">You can also pass a connection string directly toohello `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="083ca-110">Ta operacja pozwala tooverify, który hello ciągu połączenia jest w nieprawidłowym formacie.</span><span class="sxs-lookup"><span data-stu-id="083ca-110">This operation enables you tooverify that hello connection string is in a valid format.</span></span> <span data-ttu-id="083ca-111">Jeśli którekolwiek z parametrów hello są nieprawidłowe, generuje konstruktora hello `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="083ca-111">If any of hello parameters are invalid, hello constructor generates an `ArgumentException`.</span></span>

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

## <a name="hybrid-connection-stream"></a><span data-ttu-id="083ca-112">Strumień połączenia hybrydowego</span><span class="sxs-lookup"><span data-stu-id="083ca-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="083ca-113">Witaj [HybridConnectionStream] [ HCStream] klasy jest toosend obiekt podstawowy używany hello i odbieranie danych z punktem końcowym przekaźnika usługi Azure, czy użytkownik pracuje z [HybridConnectionClient] [ HCClient], lub [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="083ca-113">hello [HybridConnectionStream][HCStream] class is hello primary object used toosend and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="083ca-114">Pobieranie strumienia połączenia hybrydowego</span><span class="sxs-lookup"><span data-stu-id="083ca-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="083ca-115">Odbiornik</span><span class="sxs-lookup"><span data-stu-id="083ca-115">Listener</span></span>
<span data-ttu-id="083ca-116">Przy użyciu [HybridConnectionListener][HCListener], możesz uzyskać `HybridConnectionStream` obiektów w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="083ca-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="083ca-117">Klient</span><span class="sxs-lookup"><span data-stu-id="083ca-117">Client</span></span>
<span data-ttu-id="083ca-118">Przy użyciu [HybridConnectionClient][HCClient], możesz uzyskać `HybridConnectionStream` obiektów w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="083ca-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="083ca-119">Odbieranie danych</span><span class="sxs-lookup"><span data-stu-id="083ca-119">Receiving data</span></span>
<span data-ttu-id="083ca-120">Witaj [HybridConnectionStream] [ HCStream] klasa umożliwia komunikację dwukierunkową.</span><span class="sxs-lookup"><span data-stu-id="083ca-120">hello [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="083ca-121">W większości przypadków stale pojawi się ze strumienia hello.</span><span class="sxs-lookup"><span data-stu-id="083ca-121">In most cases, you continuously receive from hello stream.</span></span> <span data-ttu-id="083ca-122">Podczas czytania tekst ze strumienia hello, można również toouse [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) obiektu, który umożliwia łatwiejsze analizowania hello danych.</span><span class="sxs-lookup"><span data-stu-id="083ca-122">If you are reading text from hello stream, you may also want toouse a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of hello data.</span></span> <span data-ttu-id="083ca-123">Na przykład mogą odczytywać dane jako tekst, a nie jako `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="083ca-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="083ca-124">Witaj następujący kod odczytuje poszczególnych wierszy tekstu ze strumienia hello dopóki żądanie anulowania:</span><span class="sxs-lookup"><span data-stu-id="083ca-124">hello following code reads individual lines of text from hello stream until a cancellation is requested:</span></span>

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

### <a name="sending-data"></a><span data-ttu-id="083ca-125">Wysyłanie danych</span><span class="sxs-lookup"><span data-stu-id="083ca-125">Sending data</span></span>
<span data-ttu-id="083ca-126">Po połączeniu, możesz wysłać punktu końcowego przekazywania toohello wiadomości.</span><span class="sxs-lookup"><span data-stu-id="083ca-126">Once you have a connection established, you can send a message toohello Relay endpoint.</span></span> <span data-ttu-id="083ca-127">Ponieważ obiekt połączenia hello dziedziczy [strumienia](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), wysyłania danych jako `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="083ca-127">Because hello connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="083ca-128">powitania po przykładzie pokazano, jak toodo to:</span><span class="sxs-lookup"><span data-stu-id="083ca-128">hello following example shows how toodo this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="083ca-129">Jednak jeśli toosend tekst bezpośrednio, bez konieczności ciąg hello tooencode każdorazowo, można zawijać hello `hybridConnectionStream` obiekt z [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) obiektu.</span><span class="sxs-lookup"><span data-stu-id="083ca-129">However, if you want toosend text directly, without needing tooencode hello string each time, you can wrap hello `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="083ca-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="083ca-130">Next steps</span></span>
<span data-ttu-id="083ca-131">toolearn więcej informacji na temat przekaźnika usługi Azure, odwiedź te linki:</span><span class="sxs-lookup"><span data-stu-id="083ca-131">toolearn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="083ca-132">Odwołanie Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="083ca-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="083ca-133">Co to jest usługa Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="083ca-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="083ca-134">Interfejsy API dostępne przekazywania</span><span class="sxs-lookup"><span data-stu-id="083ca-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener