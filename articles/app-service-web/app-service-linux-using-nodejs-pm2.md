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
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a>Użyj konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


TooNode.js stosu aplikacji hello jest ustawiona dla aplikacji sieci Web platformy Azure w systemie Linux, spowoduje wyświetlenie hello opcja tooset pliku startowym Node.js pokazane na powitania po obrazu:

![Ustawienia pliku uruchamiania Node.js][1]

Możesz użyć tej opcji toodo jedną z hello następujące zadania:

* Określ hello skryptu uruchamiania aplikacji Node.js (na przykład: /bin/server.js).
* Określ toouse pliku konfiguracji hello PM2 aplikacji Node.js (na przykład: /foo/process.json).
  
  > [!NOTE]
  > Toorestart procesów programu Node.js automatycznie po zmodyfikowaniu niektórych plików, należy użyć hello PM2 konfiguracji. W przeciwnym razie aplikacja nie będzie ponownie po otrzymaniu powiadomienia o zmianie (na przykład, gdy zmienia się kod aplikacji).
  > 
  > 

Możesz sprawdzić hello Node.js [przetworzyć pliku dokumentacji](http://pm2.keymetrics.io/docs/usage/application-declaration/) hello wszystkie opcje, lecz poniżej przedstawiono przykładowe można jako plik process.json:

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

Toonote ważnych rzeczy w tej konfiguracji to:

* Właściwość "skrypt" Hello Określa skrypt początkowy aplikacji.
* Właściwość "instances" Hello określa liczbę wystąpień hello węzła procesu toolaunch. Jeśli używasz aplikacji na większych maszyn wirtualnych, które mają wiele rdzeni, jest toomaximize dobrze zasobów przez ustawienie wyższej wartości w tym miejscu.
* Witaj, "Obserwuj" tablicy oznacza wszystkie pliki, które chcesz toorestart hello węzła proces po zmianie.
* Dla "watch_options" hello aktualnie potrzebny toospecify "usePolling" jako true ze względu na sposób hello zawartości aplikacji jest zainstalowany.

## <a name="next-steps"></a>Następne kroki
* [Co to jest aplikacja sieci Web Azure w systemie Linux?](app-service-linux-intro.md)
* [Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
