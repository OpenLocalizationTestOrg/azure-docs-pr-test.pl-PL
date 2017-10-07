---
title: tooAzure aaaIntroduction aplikacji sieci Web w systemie Linux | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat aplikacji sieci Web platformy Azure w systemie Linux."
keywords: "Usługa aplikacji Azure, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a>Wprowadzenie tooAzure aplikacji sieci Web w systemie Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Omówienie
Klienci mogą użyć aplikacji sieci Web aplikacji sieci web toohost Linux natywnie w systemie Linux dla stosy obsługiwanej aplikacji. Witaj poniższej sekcji przedstawiono stosy aplikacji hello, które są obecnie obsługiwane. 

## <a name="features"></a>Funkcje
Aplikacji w systemie Linux sieci Web obsługuje obecnie następujące stosy aplikacji hello:

* Node.js
    * 4.4
    * 4.5
    * 6.2
    * 6.6
    * 6.9
    * 6.10
    * 6.11
    * 8.0
    * 8.1
* PHP
    * 5.6
    * 7.0
* Oprogramowanie .NET core
    * 1.0
    * 1.1
* Ruby
    * 2.3

Klienci mogą wdrożyć swoich aplikacji przy użyciu:

* FTP
* Lokalne Git
* GitHub
* Bitbucket

Do skalowania aplikacji:

* Klientów można skalować aplikacji sieci web górę i w dół, zmieniając warstwę hello ich planu usługi aplikacji
* Klienci mogą skalowanie aplikacji i uruchamiać wiele wystąpień aplikacji w obrębie hello ich jednostki SKU

Dla Kudu, niektóre podstawowe funkcje hello:

* Środowisk
* Wdrożenia
* Podstawowe konsoli
* SSH

Dla opracowywania oprogramowania:

* Środowiska przejściowe
* ACR i DockerHub CI/CD

## <a name="limitations"></a>Ograniczenia
Witaj portalu Azure zawiera tylko funkcje, które obecnie działają dla aplikacji sieci Web w systemie Linux i ukrywa hello rest. Jak możemy włączyć funkcje dodatkowe, będą one widoczne w portalu hello.

Niektóre funkcje, takie jak integracji sieci wirtualnej, Azure Active Directory/uwierzytelniania innej firmy lub Kudu rozszerzenia lokacji, nie są jeszcze dostępne. Gdy te funkcje są dostępne, aktualizujemy nasze dokumentację i blog o zmianach hello.

Ta publicznej wersji zapoznawczej jest obecnie dostępna tylko w następujących regionach hello:

* Zachodnie stany USA
* Wschodnie stany USA
* Europa Zachodnia
* Europa Północna
* Środkowo-południowe stany USA
* Środkowo-północne stany USA
* Azja Południowo-Wschodnia
* Azja Wschodnia
* Australia Wschodnia
* Japonia Wschodnia
* Brazylia Południowa
* Indie Południowe

Web Apps w systemie Linux jest obsługiwana tylko w planie usługi aplikacji dedykowanych hello i nie ma warstwy bezpłatna lub udostępnione. Ponadto planów usługi App Service dla zwykłych oraz aplikacje sieci web systemu Linux wzajemnie się wykluczają, więc nie można utworzyć aplikacji sieci web systemu Linux w planie usługi aplikacji z systemem innym niż Linux.

Web Apps w systemie Linux należy utworzyć w grupie zasobów, która nie zawiera aplikacji sieci web z systemem innym niż Linux w hello tego samego regionu.

## <a name="troubleshooting"></a>Rozwiązywanie problemów ##

Aplikacji nie powiedzie się toostart lub toocheck hello rejestrowania z aplikacji, sprawdź hello dzienniki w katalogu LogFiles hello Docker. Za pomocą witryny SCM, lub za pośrednictwem protokołu FTP można uzyskać dostępu do tego katalogu.
toolog hello `stdout` i `stderr` z Twojej kontenera należy tooenable **rejestrowania kontenera Docker** w obszarze **dzienników diagnostycznych**.

![Włączanie rejestrowania][2]

![Przy użyciu dzienników Docker tooview Kudu][1]

Można uzyskać dostępu do hello SCM lokacji z **zaawansowane narzędzia** w hello **narzędzi programistycznych** menu.

## <a name="next-steps"></a>Następne kroki
Zobacz hello następującego łącza tooget korzystania z usługi aplikacji w systemie Linux. Pytania i uwagi można umieścić na [naszym forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Jak toouse Docker niestandardowego obrazu dla aplikacji sieci Web platformy Azure w systemie Linux](app-service-linux-using-custom-docker-image.md)
* [Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux](app-service-linux-using-nodejs-pm2.md)
* [W aplikacji sieci Web usługi aplikacji Azure w systemie Linux przy użyciu platformy .NET Core](app-service-linux-using-dotnetcore.md)
* [W aplikacji sieci Web usługi aplikacji Azure w systemie Linux przy użyciu Ruby](app-service-linux-ruby-get-started.md)
* [Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania](app-service-linux-faq.md)
* [Obsługa protokołu SSH dla aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-ssh-support.md)
* [Konfigurowanie środowisk w usłudze Azure App Service przejściowych](./web-sites-staged-publishing.md)
* [Centrum docker ciągłego wdrażania aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png