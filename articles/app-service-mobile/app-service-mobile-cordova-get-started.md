---
title: "aaaCreate aplikacji platformy Cordova w usłudze Azure App Service Mobile Apps | Dokumentacja firmy Microsoft"
description: "Postępuj zgodnie z tego samouczka tooget wprowadzenie do zapleczy aplikacji mobilnych Azure przy użyciu oprogramowania Apache cordova."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: cordova,javascript,mobile,client
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a>Tworzenie aplikacji oprogramowania Apache Cordova
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak tooadd wewnętrznej bazy danych opartej na chmurze usługi aplikacji mobilnej oprogramowania Apache Cordova tooan przy użyciu zaplecza aplikacji mobilnej Azure.  Utworzysz nowe zaplecze aplikacji mobilnej oraz prostą aplikację oprogramowania Apache Cordova typu *Lista czynności do wykonania*, która przechowuje dane aplikacji na platformie Azure.

Wykonanie kroków tego samouczka jest wymaganiem wstępnym dla wszystkich innych samouczków Apache Cordova dotyczących używania funkcji Mobile Apps hello w usłudze Azure App Service.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy hello następujące wymagania wstępne:

* Komputer z programem [Visual Studio Community 2017] lub nowszym.
* [Visual Studio Tools for Apache Cordova].
* [Aktywne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

Można również pominąć program Visual Studio i używać bezpośrednio wiersza polecenia hello Apache Cordova.  Przy użyciu wiersza polecenia hello jest przydatne, gdy wykonanie kroków samouczka hello na komputerze Mac.  Kompilowanie aplikacji klienckich oprogramowania Apache Cordova za pomocą wiersza polecenia hello nie jest opisane w tym samouczku.

## <a name="create-an-azure-mobile-app-backend"></a>Tworzenie zaplecza aplikacji mobilnej Azure
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[Obejrzyj wideo przedstawiające podobne kroki](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a>Konfigurowanie projektu serwera hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a>Pobieranie i uruchamianie aplikacji oprogramowania Apache Cordova hello
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a>Następne kroki
Teraz, gdy ukończeniu tego samouczka szybkiego startu przejść tooone hello następujące samouczki:

* [Dodawanie danych w trybie Offline](app-service-mobile-cordova-get-started-offline-data.md) tooyour aplikacji oprogramowania Apache Cordova.
* [Dodawanie uwierzytelniania](app-service-mobile-cordova-get-started-users.md) tooyour aplikacji oprogramowania Apache Cordova.
* [Dodawanie powiadomień wypychanych](app-service-mobile-cordova-get-started-push.md) tooyour aplikacji oprogramowania Apache Cordova.

Dowiedz się więcej na temat najważniejszych pojęć związanych z usługą Azure App Service.

* [Dane w trybie offline]
* [Uwierzytelnianie]
* [Powiadomienia wypychane]

Dowiedz się, jak toouse hello zestawów SDK.

* [Zestaw Apache Cordova SDK]
* [Zestaw ASP.NET Server SDK]
* [Zestaw Node.js Server SDK]

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Dane w trybie offline]: app-service-mobile-offline-data-sync.md
[Uwierzytelnianie]: app-service-mobile-auth.md
[Powiadomienia wypychane]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Zestaw Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[Zestaw ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Zestaw Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
