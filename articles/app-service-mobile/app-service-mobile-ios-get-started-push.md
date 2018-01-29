---
title: "Dodawanie powiadomień wypychanych do aplikacji za pomocą usługi Azure Mobile Apps systemu iOS"
description: "Dowiedz się, jak używać usługi Azure Mobile Apps do wysyłania powiadomień wypychanych do aplikacji systemu iOS."
services: app-service\mobile
documentationcenter: ios
manager: crdun
editor: 
author: conceptdev
ms.assetid: fa503833-d23e-4925-8d93-341bb3fbab7d
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/10/2016
ms.author: crdun
ms.openlocfilehash: 063926a5a98aeab62e191d372831a00c29b9f6d7
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2018
---
# <a name="add-push-notifications-to-your-ios-app"></a>Dodawanie powiadomień wypychanych do aplikacji dla systemu iOS
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Przegląd
W tym samouczku, dodawanie powiadomień wypychanych do [iOS szybki start] projektu, aby powiadomienia wypychane są wysyłane do urządzenia, za każdym razem, gdy wstawieniu rekordu.

Jeśli nie używasz Projekt serwera pobrany szybki start, konieczne będzie pakiet rozszerzenia powiadomień wypychanych. Zobacz [pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) Aby uzyskać więcej informacji.

[Symulatora systemu iOS nie obsługuje powiadomień wypychanych](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html). Potrzebujesz urządzenia fizyczne z systemem iOS i [członkostwo w programie dla deweloperów firmy Apple](https://developer.apple.com/programs/ios/).

## <a name="configure-hub"></a>Konfigurowanie Centrum powiadomień
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Rejestrowanie aplikacji dla powiadomień wypychanych
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a>Konfigurowanie usługi Azure do wysyłania powiadomień wypychanych
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a id="update-server"></a>Zaktualizuj wewnętrznej bazy danych do wysyłania powiadomień wypychanych
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <a id="add-push"></a>Dodawanie powiadomień wypychanych do aplikacji
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <a id="test"></a>Powiadomienia wypychane testu
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <a id="more"></a>Więcej
* Szablony zapewniają elastyczność i możliwość wysyłania wypchnięć i platform i wypchnięć zlokalizowanego. [Sposób użycia iOS biblioteki klienta usługi Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) pokazuje, jak zarejestrować szablonów.

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS szybki start]: app-service-mobile-ios-get-started.md
