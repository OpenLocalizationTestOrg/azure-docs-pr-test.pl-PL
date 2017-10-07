---
title: "aaaCreate aplikacji systemu Android w usłudze Azure App Service Mobile Apps | Dokumentacja firmy Microsoft"
description: "Postępuj zgodnie z tego samouczka tooget korzystanie z zapleczy zapleczy aplikacji mobilnych Azure dla systemu Android."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 0af85a3a4de9fc265976bbe3f34d73effc3807df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-android-app"></a>Tworzenie aplikacji systemu Android
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak tooadd wewnętrznej bazy danych opartej na chmurze usługi tooan aplikacji mobilnej systemu Android przy użyciu zaplecza aplikacji mobilnej Azure.  Będziesz tworzyć nowe zaplecze aplikacji mobilnej oraz prostą aplikację systemu Android typu *Lista czynności do wykonania*, która przechowuje dane aplikacji na platformie Azure.

Wykonanie kroków tego samouczka jest wymaganiem wstępnym dla wszystkich innych samouczków dla systemu Android dotyczących używania funkcji Mobile Apps hello w usłudze Azure App Service.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy hello następujące:

* [Narzędzia dla deweloperów systemu android](https://developer.android.com/sdk/index.html), w tym hello Android Studio zintegrowane środowisko programistyczne oraz najnowszej platformy Android hello.
* Azure Mobile Android SDK, która jest automatycznie używany jako część hello pobieranego projektu szybkiego startu możesz pobrać.
* [Aktywne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-new-azure-mobile-app-backend"></a>Tworzenie zaplecza nowej aplikacji mobilnej Azure
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Konfigurowanie projektu serwera hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a>Pobieranie i uruchamianie aplikacji systemu Android hello
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
