---
title: "Konfiguracja aaaUsing PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux"
keywords: "Usługa aplikacji Azure, aplikacji sieci web, nodejs, pm2, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="e068c-104">Użyj konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e068c-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="e068c-105">TooNode.js stosu aplikacji hello jest ustawiona dla aplikacji sieci Web platformy Azure w systemie Linux, spowoduje wyświetlenie hello opcja tooset pliku startowym Node.js pokazane na powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="e068c-105">If you set hello application stack tooNode.js for Azure Web App on Linux, you get hello option tooset a Node.js startup file as shown in hello following image:</span></span>

![Ustawienia pliku uruchamiania Node.js][1]

<span data-ttu-id="e068c-107">Możesz użyć tej opcji toodo jedną z hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="e068c-107">You can use this option toodo one of hello following tasks:</span></span>

* <span data-ttu-id="e068c-108">Określ hello skryptu uruchamiania aplikacji Node.js (na przykład: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="e068c-108">Specify hello startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="e068c-109">Określ toouse pliku konfiguracji hello PM2 aplikacji Node.js (na przykład: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="e068c-109">Specify hello PM2 configuration file toouse for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="e068c-110">Toorestart procesów programu Node.js automatycznie po zmodyfikowaniu niektórych plików, należy użyć hello PM2 konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e068c-110">If you want your Node.js processes toorestart automatically when certain files are modified, use hello PM2 configuration.</span></span> <span data-ttu-id="e068c-111">W przeciwnym razie aplikacja nie będzie ponownie po otrzymaniu powiadomienia o zmianie (na przykład, gdy zmienia się kod aplikacji).</span><span class="sxs-lookup"><span data-stu-id="e068c-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="e068c-112">Możesz sprawdzić hello Node.js [przetworzyć pliku dokumentacji](http://pm2.keymetrics.io/docs/usage/application-declaration/) hello wszystkie opcje, lecz poniżej przedstawiono przykładowe można jako plik process.json:</span><span class="sxs-lookup"><span data-stu-id="e068c-112">You can check hello Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all hello options, but following is a sample of what you can use as your process.json file:</span></span>

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

<span data-ttu-id="e068c-113">Toonote ważnych rzeczy w tej konfiguracji to:</span><span class="sxs-lookup"><span data-stu-id="e068c-113">Important things toonote in this configuration are:</span></span>

* <span data-ttu-id="e068c-114">Właściwość "skrypt" Hello Określa skrypt początkowy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e068c-114">hello "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="e068c-115">Właściwość "instances" Hello określa liczbę wystąpień hello węzła procesu toolaunch.</span><span class="sxs-lookup"><span data-stu-id="e068c-115">hello "instances" property specifies how many instances of hello node process toolaunch.</span></span> <span data-ttu-id="e068c-116">Jeśli używasz aplikacji na większych maszyn wirtualnych, które mają wiele rdzeni, jest toomaximize dobrze zasobów przez ustawienie wyższej wartości w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="e068c-116">If you are running your application on larger VMs that have multiple cores, it's a good idea toomaximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="e068c-117">Witaj, "Obserwuj" tablicy oznacza wszystkie pliki, które chcesz toorestart hello węzła proces po zmianie.</span><span class="sxs-lookup"><span data-stu-id="e068c-117">hello "watch" array specifies all files that you want toorestart hello node process for when they change.</span></span>
* <span data-ttu-id="e068c-118">Dla "watch_options" hello aktualnie potrzebny toospecify "usePolling" jako true ze względu na sposób hello zawartości aplikacji jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="e068c-118">For hello "watch_options", you currently need toospecify "usePolling" as true because of hello way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e068c-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e068c-119">Next steps</span></span>
* [<span data-ttu-id="e068c-120">Co to jest aplikacja sieci Web Azure w systemie Linux?</span><span class="sxs-lookup"><span data-stu-id="e068c-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="e068c-121">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="e068c-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
