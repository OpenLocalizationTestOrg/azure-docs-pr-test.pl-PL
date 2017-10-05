---
title: "Konfigurowanie usługi Azure Media Services dane telemetryczne z platformą .NET | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób użycia telemetrii usługi Azure Media Services przy użyciu zestawu .NET SDK."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f8f55e37-0714-49ea-bf4a-e6c1319bec44
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 1d857f3d062d8d1b15c64fa4b8c3e27ad6c2247e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-azure-media-services-telemetry-with-net"></a><span data-ttu-id="fcd35-103">Konfigurowanie usługi Azure Media Services dane telemetryczne z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="fcd35-103">Configuring Azure Media Services telemetry with .NET</span></span>

<span data-ttu-id="fcd35-104">W tym temacie opisano ogólne kroki, które może wykonać podczas konfigurowania telemetrii usługi Azure Media Services (AMS) przy użyciu zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="fcd35-104">This topic describes general steps that you might take when configuring the Azure Media Services (AMS) telemetry using .NET SDK.</span></span> 

>[!NOTE]
><span data-ttu-id="fcd35-105">Aby uzyskać szczegółowy opis co to jest AMS telemetrii oraz sposób pobrać go, zobacz [omówienie](media-services-telemetry-overview.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="fcd35-105">For the detailed explanation of what is AMS telemetry and how to consume it, see the [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="fcd35-106">Dane telemetryczne można korzystać w jednym z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="fcd35-106">You can consume telemetry data in one of the following ways:</span></span>

- <span data-ttu-id="fcd35-107">Odczytywanie danych bezpośrednio z magazynem tabel Azure (np. przy użyciu zestawu SDK usługi Magazyn).</span><span class="sxs-lookup"><span data-stu-id="fcd35-107">Read data directly from Azure Table Storage (e.g. using the Storage SDK).</span></span> <span data-ttu-id="fcd35-108">Opis tabel do przechowywania danych telemetrycznych zawiera **wykorzystywanie informacji telemetrii** w [to](https://msdn.microsoft.com/library/mt742089.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="fcd35-108">For the description of telemetry storage tables, see the **Consuming telemetry information** in [this](https://msdn.microsoft.com/library/mt742089.aspx) topic.</span></span>

<span data-ttu-id="fcd35-109">Lub</span><span class="sxs-lookup"><span data-stu-id="fcd35-109">Or</span></span>

- <span data-ttu-id="fcd35-110">Użyć funkcji w SDK .NET usługi Media Services do odczytywania danych z magazynu.</span><span class="sxs-lookup"><span data-stu-id="fcd35-110">Use the support in the Media Services .NET SDK for reading storage data.</span></span> <span data-ttu-id="fcd35-111">W tym temacie pokazano, jak włączyć dane telemetryczne dla określonego konta usługi AMS oraz jak zapytania metryki przy użyciu zestawu SDK .NET usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="fcd35-111">This topic shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span></span>  

## <a name="configuring-telemetry-for-a-media-services-account"></a><span data-ttu-id="fcd35-112">Konfigurowanie dane telemetryczne dla konta usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="fcd35-112">Configuring telemetry for a Media Services account</span></span>

<span data-ttu-id="fcd35-113">Poniższe kroki są wymagane do włączenia telemetrii:</span><span class="sxs-lookup"><span data-stu-id="fcd35-113">The following steps are needed to enable telemetry:</span></span>

- <span data-ttu-id="fcd35-114">Uzyskiwanie poświadczeń konta usługi Magazyn dołączany do konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="fcd35-114">Get the credentials of the storage account attached to the Media Services account.</span></span> 
- <span data-ttu-id="fcd35-115">Tworzenie punktu końcowego powiadomienia o **EndPointType** ustawioną **AzureTable** i endPointAddress wskazujący tabeli magazynu.</span><span class="sxs-lookup"><span data-stu-id="fcd35-115">Create a Notification Endpoint with **EndPointType** set to **AzureTable** and endPointAddress pointing to the storage table.</span></span>

        INotificationEndPoint notificationEndPoint = 
                      _context.NotificationEndPoints.Create("monitoring", 
                      NotificationEndPointType.AzureTable,
                      "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/");

- <span data-ttu-id="fcd35-116">Tworzenie konfiguracji monitorowania ustawienia usługi, które chcesz monitorować.</span><span class="sxs-lookup"><span data-stu-id="fcd35-116">Create a monitoring configuration settings for the services you want to monitor.</span></span> <span data-ttu-id="fcd35-117">Nie więcej niż jednego ustawienia konfiguracji monitorowania jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="fcd35-117">No more than one monitoring configuration settings is allowed.</span></span> 
  
        IMonitoringConfiguration monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
            new List<ComponentMonitoringSetting>()
            {
                new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)
            });

## <a name="consuming-telemetry-information"></a><span data-ttu-id="fcd35-118">Wykorzystywanie informacji telemetrii</span><span class="sxs-lookup"><span data-stu-id="fcd35-118">Consuming telemetry information</span></span>

<span data-ttu-id="fcd35-119">Informacji o odbierającą telemetrii, zobacz [to](media-services-telemetry-overview.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="fcd35-119">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="fcd35-120">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fcd35-120">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="fcd35-121">Skonfiguruj środowisko projektowe i wypełnij plik app.config przy użyciu informacji dotyczących połączenia, zgodnie z opisem w sekcji [Projektowanie usługi Media Services na platformie .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="fcd35-121">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

2. <span data-ttu-id="fcd35-122">Dodaj następujący element do **appSettings** zdefiniowane w pliku app.config:</span><span class="sxs-lookup"><span data-stu-id="fcd35-122">Add the following element to **appSettings** defined in your app.config file:</span></span>

    <add key="StorageAccountName" value="storage_name" />
 
## <a name="example"></a><span data-ttu-id="fcd35-123">Przykład</span><span class="sxs-lookup"><span data-stu-id="fcd35-123">Example</span></span>  
    
<span data-ttu-id="fcd35-124">Poniższy przykład przedstawia, jak włączyć dane telemetryczne dla określonego konta usługi AMS i jak wykonać zapytanie metryki przy użyciu zestawu SDK .NET usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="fcd35-124">The following example shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span></span>  

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSMetrics
    {
        class Program
        {
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly string _mediaServicesStorageAccountName =
            ConfigurationManager.AppSettings["StorageAccountName"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static IStreamingEndpoint _streamingEndpoint = null;
        private static IChannel _channel = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            _streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            _channel = _context.Channels.FirstOrDefault();

            var monitoringConfigurations = _context.MonitoringConfigurations;
            IMonitoringConfiguration monitoringConfiguration = null;

            // No more than one monitoring configuration settings is allowed.
            if (monitoringConfigurations.ToArray().Length != 0)
            {
            monitoringConfiguration = _context.MonitoringConfigurations.FirstOrDefault();
            }
            else
            {
            INotificationEndPoint notificationEndPoint =
                      _context.NotificationEndPoints.Create("monitoring",
                      NotificationEndPointType.AzureTable, GetTableEndPoint());

            monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
                new List<ComponentMonitoringSetting>()
                {
                    new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                    new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)

                });
            }

            //Print metrics for a Streaming Endpoint.
            PrintStreamingEndpointMetrics();

            Console.ReadLine();
        }

        private static string GetTableEndPoint()
        {
            return "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/";
        }

        private static void PrintStreamingEndpointMetrics()
        {
            Console.WriteLine(string.Format("Telemetry for streaming endpoint '{0}'", _streamingEndpoint.Name));

            DateTime timerangeEnd = DateTime.UtcNow;
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some streaming endpoint metrics.
            var telemetry = _streamingEndpoint.GetTelemetry();

            var res = telemetry.GetStreamingEndpointRequestLogs(timerangeStart, timerangeEnd);

            Console.Title = "Streaming endpoint metrics:";

            foreach (var log in res)
            {
            Console.WriteLine("AccountId: {0}", log.AccountId);
            Console.WriteLine("BytesSent: {0}", log.BytesSent);
            Console.WriteLine("EndToEndLatency: {0}", log.EndToEndLatency);
            Console.WriteLine("HostName: {0}", log.HostName);
            Console.WriteLine("ObservedTime: {0}", log.ObservedTime);
            Console.WriteLine("PartitionKey: {0}", log.PartitionKey);
            Console.WriteLine("RequestCount: {0}", log.RequestCount);
            Console.WriteLine("ResultCode: {0}", log.ResultCode);
            Console.WriteLine("RowKey: {0}", log.RowKey);
            Console.WriteLine("ServerLatency: {0}", log.ServerLatency);
            Console.WriteLine("StatusCode: {0}", log.StatusCode);
            Console.WriteLine("StreamingEndpointId: {0}", log.StreamingEndpointId);
            Console.WriteLine();
            }

            Console.WriteLine();
        }

        private static void PrintChannelMetrics()
        {
            if (_channel == null)
            {
            Console.WriteLine("There are no channels in this AMS account");
            return;
            }

            Console.WriteLine(string.Format("Telemetry for channel '{0}'", _channel.Name));

            DateTime timerangeEnd = DateTime.UtcNow; 
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some channel metrics.
            var telemetry = _channel.GetTelemetry();

            var channelMetrics = telemetry.GetChannelHeartbeats(timerangeStart, timerangeEnd);

            // Print the channel metrics.
            Console.WriteLine("Channel metrics:");

            foreach (var channelHeartbeat in channelMetrics.OrderBy(x => x.ObservedTime))
            {
            Console.WriteLine(
                "    Observed time: {0}, Last timestamp: {1}, Incoming bitrate: {2}",
                channelHeartbeat.ObservedTime,
                channelHeartbeat.LastTimestamp,
                channelHeartbeat.IncomingBitrate);
            }

            Console.WriteLine();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="fcd35-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fcd35-125">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fcd35-126">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="fcd35-126">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
