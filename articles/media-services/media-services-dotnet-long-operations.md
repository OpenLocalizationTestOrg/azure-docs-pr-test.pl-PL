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
# <a name="delivering-live-streaming-with-azure-media-services"></a>Dostarczanie transmisję strumieniową na żywo za pomocą usługi Azure Media Services

## <a name="overview"></a>Omówienie

Microsoft Azure Media Services udostępnia interfejsy API, które wysyłają żądania operacji toostart usług tooMedia (na przykład: Utwórz, uruchom, Zatrzymaj lub usuwanie kanału). Operacje te są długotrwałe.

Hello .NET SDK usługi Media Services udostępnia interfejsy API, Wyślij żądanie hello i poczekaj, aż hello operacji toocomplete (wewnętrznie, powitalne interfejsy API są sondowanie postęp operacji niektórych odstępach). Na przykład w przypadku wywołania kanału. Funkcji Start(), metoda hello zwraca po rozpoczęciu hello kanału. Można również używać wersji asynchroniczne hello: oczekiwania kanału. StartAsync() (Aby uzyskać informacje dotyczące wzorca asynchronicznego opartego na zadaniach, zobacz [wybierz](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)). Interfejsy API, które Wyślij żądanie operacji, a następnie sondowania stanu hello aż do zakończenia operacji hello są nazywane "sondowania metody". Te metody (szczególnie wersję Async hello) są zalecane dla zaawansowanych aplikacji klienckich i/lub usług stanowych.

Brak scenariuszy, w którym aplikacja nie może czekać na długo działające żądanie http potrzebuje toopoll dla postęp operacji hello ręcznie. Typowym przykładem jest przeglądarką interakcji z usługą sieci web bezstanowe: gdy przeglądarka hello żąda toocreate kanał, usługi sieci web hello inicjuje operacją wymagającą dużo czasu i zwraca hello przeglądarki toohello identyfikator operacji. Przeglądarka Hello można następnie poprosić hello sieci web usługi tooget hello stan operacji na podstawie identyfikatora hello. Hello .NET SDK usługi Media Services udostępnia interfejsy API, które są przydatne w przypadku tego scenariusza. Te interfejsy API są nazywane "metod innych niż sondowania".
"Witaj z systemem innym niż sondowania metody" mają powitania po wzorzec nazewnictwa: wysyłanie*OperationName*operacji (na przykład SendCreateOperation). Wyślij*OperationName*operacji metody zwracają hello **IOperation** obiektu; hello zwrócony obiekt zawiera informacje, które mogą być używane tootrack hello operacji. Witaj wysyłania*OperationName*OperationAsync metody zwracają **zadań<IOperation>**.

Obecnie hello następujące klasy pomocy technicznej z systemem innym niż sondowania metody: **kanału**, **StreamingEndpoint**, i **Program**.

toopoll hello operacji stanu, użyj hello **GetOperation** metody na powitania **OperationBaseCollection** klasy. Użyj powitania po stan operacji dla interwałów toocheck hello: dla **kanału** i **StreamingEndpoint** operacji, użyj 30 sekund; dla **Program** operacji, użyj 10 Liczba sekund.

## <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).

## <a name="example"></a>Przykład

Witaj poniższym przykładzie zdefiniowano klasę o nazwie **ChannelOperations**. Ta definicja klasy może być punkt początkowy dla definicji klasy usługi sieci web. Dla uproszczenia hello następujących przykładach użyto hello wersji z systemem innym niż asynchronicznych metod.

przykład Witaj przedstawiono również sposób powitania klienta może używać tej klasy.

### <a name="channeloperations-class-definition"></a>Definicja klasy ChannelOperations

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

### <a name="hello-client-code"></a>Kod powitania klienta:
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



## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

