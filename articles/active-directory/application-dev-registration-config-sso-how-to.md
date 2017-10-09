---
title: "tooconfigure aaaHow nowej aplikacji wielodostępnych | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure logowanie jednokrotne dla aplikacji niestandardowej opracowywania i rejestrowanie w usłudze Azure AD."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a>Jak tooconfigure nowej aplikacji wieloma dzierżawcami

Włączanie federacyjnych rejestracji jednokrotnej (SSO) w aplikacji jest automatycznie włączone podczas federowania za pośrednictwem usługi Azure AD dla OpenID Connect SAML 2.0 i WS-Fed. Jeśli użytkownicy końcowi toosign pomimo już o istniejącej sesji z usługą Azure AD, prawdopodobnie aplikacji może być niepoprawnie skonfigurowany.

* Jeśli korzystasz z biblioteki ADAL/MSAL, upewnij się, masz **PromptBehavior** ustawić także**automatycznie** zamiast **zawsze**.

* Jeśli tworzysz aplikację mobilną, może być konieczne dodatkowe konfiguracje tooenable obsługiwanych przez brokera lub z systemem innym niż nieobsługiwana przez brokera logowania jednokrotnego.

Dla systemu Android, zobacz [włączanie dla wielu aplikacji rejestracji Jednokrotnej w systemie Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).<br>

Dla systemu iOS, zobacz [włączanie dla wielu aplikacji rejestracji Jednokrotnej w systemie iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).

## <a name="next-steps"></a>Następne kroki

[Azure AD logowania jednokrotnego.](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[Włączanie Cross logowania jednokrotnego aplikacji w systemie Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[Włączanie dla wielu aplikacji rejestracji Jednokrotnej w systemie iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[Integrowanie aplikacji tooAzureAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[Permissioning dla AzureAD w wersji 2.0 i zgody zbieżność aplikacji](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[AzureAD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
