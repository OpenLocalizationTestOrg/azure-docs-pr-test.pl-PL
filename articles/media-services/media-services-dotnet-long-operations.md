---
title: "aaaPolling długotrwałe operacje | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób toopoll długotrwałej operacji."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="2b769-103">Dostarczanie transmisję strumieniową na żywo za pomocą usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="2b769-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="2b769-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2b769-104">Overview</span></span>

<span data-ttu-id="2b769-105">Microsoft Azure Media Services udostępnia interfejsy API, które wysyłają żądania operacji toostart usług tooMedia (na przykład: Utwórz, uruchom, Zatrzymaj lub usuwanie kanału).</span><span class="sxs-lookup"><span data-stu-id="2b769-105">Microsoft Azure Media Services offers APIs that send requests tooMedia Services toostart operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="2b769-106">Operacje te są długotrwałe.</span><span class="sxs-lookup"><span data-stu-id="2b769-106">These operations are long-running.</span></span>

<span data-ttu-id="2b769-107">Hello .NET SDK usługi Media Services udostępnia interfejsy API, Wyślij żądanie hello i poczekaj, aż hello operacji toocomplete (wewnętrznie, powitalne interfejsy API są sondowanie postęp operacji niektórych odstępach).</span><span class="sxs-lookup"><span data-stu-id="2b769-107">hello Media Services .NET SDK provides APIs that send hello request and wait for hello operation toocomplete (internally, hello APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="2b769-108">Na przykład w przypadku wywołania kanału. Funkcji Start(), metoda hello zwraca po rozpoczęciu hello kanału.</span><span class="sxs-lookup"><span data-stu-id="2b769-108">For example, when you call channel.Start(), hello method returns after hello channel is started.</span></span> <span data-ttu-id="2b769-109">Można również używać wersji asynchroniczne hello: oczekiwania kanału. StartAsync() (Aby uzyskać informacje dotyczące wzorca asynchronicznego opartego na zadaniach, zobacz [wybierz](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="2b769-109">You can also use hello asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="2b769-110">Interfejsy API, które Wyślij żądanie operacji, a następnie sondowania stanu hello aż do zakończenia operacji hello są nazywane "sondowania metody".</span><span class="sxs-lookup"><span data-stu-id="2b769-110">APIs that send an operation request and then poll for hello status until hello operation is complete are called “polling methods”.</span></span> <span data-ttu-id="2b769-111">Te metody (szczególnie wersję Async hello) są zalecane dla zaawansowanych aplikacji klienckich i/lub usług stanowych.</span><span class="sxs-lookup"><span data-stu-id="2b769-111">These methods (especially hello Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="2b769-112">Brak scenariuszy, w którym aplikacja nie może czekać na długo działające żądanie http potrzebuje toopoll dla postęp operacji hello ręcznie.</span><span class="sxs-lookup"><span data-stu-id="2b769-112">There are scenarios where an application cannot wait for a long running http request and wants toopoll for hello operation progress manually.</span></span> <span data-ttu-id="2b769-113">Typowym przykładem jest przeglądarką interakcji z usługą sieci web bezstanowe: gdy przeglądarka hello żąda toocreate kanał, usługi sieci web hello inicjuje operacją wymagającą dużo czasu i zwraca hello przeglądarki toohello identyfikator operacji.</span><span class="sxs-lookup"><span data-stu-id="2b769-113">A typical example would be a browser interacting with a stateless web service: when hello browser requests toocreate a channel, hello web service initiates a long running operation and returns hello operation ID toohello browser.</span></span> <span data-ttu-id="2b769-114">Przeglądarka Hello można następnie poprosić hello sieci web usługi tooget hello stan operacji na podstawie identyfikatora hello.</span><span class="sxs-lookup"><span data-stu-id="2b769-114">hello browser could then ask hello web service tooget hello operation status based on hello ID.</span></span> <span data-ttu-id="2b769-115">Hello .NET SDK usługi Media Services udostępnia interfejsy API, które są przydatne w przypadku tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="2b769-115">hello Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="2b769-116">Te interfejsy API są nazywane "metod innych niż sondowania".</span><span class="sxs-lookup"><span data-stu-id="2b769-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="2b769-117">"Witaj z systemem innym niż sondowania metody" mają powitania po wzorzec nazewnictwa: wysyłanie*OperationName*operacji (na przykład SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="2b769-117">hello “non-polling methods” have hello following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="2b769-118">Wyślij*OperationName*operacji metody zwracają hello **IOperation** obiektu; hello zwrócony obiekt zawiera informacje, które mogą być używane tootrack hello operacji.</span><span class="sxs-lookup"><span data-stu-id="2b769-118">Send*OperationName*Operation methods return hello **IOperation** object; hello returned object contains information that can be used tootrack hello operation.</span></span> <span data-ttu-id="2b769-119">Witaj wysyłania*OperationName*OperationAsync metody zwracają **zadań<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="2b769-119">hello Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="2b769-120">Obecnie hello następujące klasy pomocy technicznej z systemem innym niż sondowania metody: **kanału**, **StreamingEndpoint**, i **Program**.</span><span class="sxs-lookup"><span data-stu-id="2b769-120">Currently, hello following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="2b769-121">toopoll hello operacji stanu, użyj hello **GetOperation** metody na powitania **OperationBaseCollection** klasy.</span><span class="sxs-lookup"><span data-stu-id="2b769-121">toopoll for hello operation status, use hello **GetOperation** method on hello **OperationBaseCollection** class.</span></span> <span data-ttu-id="2b769-122">Użyj powitania po stan operacji dla interwałów toocheck hello: dla **kanału** i **StreamingEndpoint** operacji, użyj 30 sekund; dla **Program** operacji, użyj 10 Liczba sekund.</span><span class="sxs-lookup"><span data-stu-id="2b769-122">Use hello following intervals toocheck hello operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="2b769-123">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2b769-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="2b769-124">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="2b769-124">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="2b769-125">Przykład</span><span class="sxs-lookup"><span data-stu-id="2b769-125">Example</span></span>

<span data-ttu-id="2b769-126">Witaj poniższym przykładzie zdefiniowano klasę o nazwie **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="2b769-126">hello following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="2b769-127">Ta definicja klasy może być punkt początkowy dla definicji klasy usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="2b769-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="2b769-128">Dla uproszczenia hello następujących przykładach użyto hello wersji z systemem innym niż asynchronicznych metod.</span><span class="sxs-lookup"><span data-stu-id="2b769-128">For simplicity, hello following examples use hello non-async versions of methods.</span></span>

<span data-ttu-id="2b769-129">przykład Witaj przedstawiono również sposób powitania klienta może używać tej klasy.</span><span class="sxs-lookup"><span data-stu-id="2b769-129">hello example also shows how hello client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="2b769-130">Definicja klasy ChannelOperations</span><span class="sxs-lookup"><span data-stu-id="2b769-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
                StreamingProtocol = StreamingProtocol.RTMP,
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelInput001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelPreview001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="hello-client-code"></a><span data-ttu-id="2b769-131">Kod powitania klienta:</span><span class="sxs-lookup"><span data-stu-id="2b769-131">hello client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="2b769-132">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="2b769-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2b769-133">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="2b769-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

