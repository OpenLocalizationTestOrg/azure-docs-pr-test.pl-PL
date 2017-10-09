---
title: aaaAzure AD v2 Windows Desktop wprowadzenie - Config | Dokumentacja firmy Microsoft
description: "Jak aplikacji .NET pulpitu systemu Windows (XAML) można uzyskać tokenu dostępu i wywołania funkcji API chronione przez punkt końcowy w wersji 2 usługi Azure Active Directory. | Microsoft Azure | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Tworzenie aplikacji (Express)
Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:
1. Zarejestrować aplikację za pośrednictwem hello [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)
2.  Wprowadź nazwę aplikacji i poczty e-mail
3.  Upewnij się, że jest zaznaczona opcja hello z przewodnikiem instalacji
4.  Wykonaj identyfikator aplikacji hello hello instrukcje tooobtain i wklej go w kodzie

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Dodawanie rozwiązania tooyour informacji o rejestracji aplikacji (zaawansowane)
Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:
1. Przejdź toohello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister aplikacji
2. Wprowadź nazwę aplikacji i poczty e-mail 
3. Upewnij się, że jest zaznaczona opcja hello instrukcje konfiguracji
4. Kliknij przycisk `Add Platform`, a następnie wybierz pozycję `Native Application` i kliknij przycisk Zapisz
5. Skopiuj identyfikator aplikacji hello identyfikator GUID, przejdź wstecz tooVisual Studio, otwórz `App.xaml.cs` i Zastąp `your_client_id_here` z hello został zarejestrowany identyfikator aplikacji:

```csharp
private static string ClientId = "your_application_id_here";
```
