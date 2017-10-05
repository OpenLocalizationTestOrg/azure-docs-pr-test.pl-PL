---
title: Wprowadzenie do aplikacji sieci Web platformy Azure w systemie Linux | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 0870f811845ec7c705da13f08abdfa762d25b209
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-web-app-on-linux"></a>Wprowadzenie do aplikacji sieci Web platformy Azure w systemie Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Omówienie
Klienci mogą użyć aplikacji sieci Web w systemie Linux do aplikacji sieci web hosta natywnie w systemie Linux dla stosy obsługiwanej aplikacji. W poniższej sekcji przedstawiono stosy aplikacji, które są obecnie obsługiwane. 

## <a name="features"></a>Funkcje
Aplikacji w systemie Linux sieci Web obsługuje obecnie następujących stosy aplikacji:

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

* Klientów można skalować aplikacji sieci web górę i w dół, zmieniając warstwę ich planu usługi aplikacji
* Klienci mogą skalowanie aplikacji i uruchamiać wiele wystąpień aplikacji w obrębie ich jednostki SKU

Dla Kudu, niektóre podstawowe funkcje:

* Środowisk
* Wdrożenia
* Podstawowe konsoli
* SSH

Dla opracowywania oprogramowania:

* Środowiska przejściowe
* ACR i DockerHub CI/CD

## <a name="limitations"></a>Ograniczenia
Azure portal zawiera tylko funkcje, które obecnie działają dla aplikacji sieci Web w systemie Linux i ukrywa pozostałe. Jak możemy włączyć funkcje dodatkowe, będą one widoczne w portalu.

Niektóre funkcje, takie jak integracji sieci wirtualnej, Azure Active Directory/uwierzytelniania innej firmy lub Kudu rozszerzenia lokacji, nie są jeszcze dostępne. Gdy te funkcje są dostępne, aktualizujemy nasze dokumentację i blog o zmianach.

Ta publicznej wersji zapoznawczej jest obecnie dostępna tylko w następujących regionach:

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

Web Apps w systemie Linux jest obsługiwana tylko w planie usługi aplikacji dedykowanej i nie ma warstwy bezpłatna lub udostępnione. Ponadto planów usługi App Service dla zwykłych oraz aplikacje sieci web systemu Linux wzajemnie się wykluczają, więc nie można utworzyć aplikacji sieci web systemu Linux w planie usługi aplikacji z systemem innym niż Linux.

Web Apps w systemie Linux należy utworzyć w grupie zasobów, która nie zawiera aplikacji sieci web z systemem innym niż Linux, w tym samym regionie.

## <a name="troubleshooting"></a>Rozwiązywanie problemów ##

Aplikacji nie powiedzie się lub chcesz sprawdzić rejestrowania z aplikacji, sprawdź dzienniki w katalogu LogFiles Docker. Za pomocą witryny SCM, lub za pośrednictwem protokołu FTP można uzyskać dostępu do tego katalogu.
W dzienniku `stdout` i `stderr` z Twojej kontenera, musisz włączyć **rejestrowania kontenera Docker** w obszarze **dzienników diagnostycznych**.

![Włączanie rejestrowania][2]

![Aby wyświetlić dzienniki Docker przy użyciu Kudu][1]

Można uzyskać dostępu do lokacji SCM z **zaawansowane narzędzia** w **narzędzi programistycznych** menu.

## <a name="next-steps"></a>Następne kroki
Zobacz poniższe łącza, aby rozpocząć korzystanie z usługi aplikacji w systemie Linux. Pytania i uwagi można umieścić na [naszym forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Sposób użycia niestandardowego obrazu Docker dla aplikacji sieci Web platformy Azure w systemie Linux](app-service-linux-using-custom-docker-image.md)
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