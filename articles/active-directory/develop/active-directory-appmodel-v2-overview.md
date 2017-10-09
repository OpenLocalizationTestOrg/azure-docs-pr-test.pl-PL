---
title: "punktu końcowego v2.0 usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toobuilding aplikacje z logowaniem zarówno Account firmy Microsoft, jak i usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a>Logowanie użytkowników usługi Azure AD w jednej aplikacji & Account firmy Microsoft
W hello poza Deweloper aplikacji, którzy chcieli toosupport oba osobistego konta Microsoft i konta pracy z usługą Azure Active Directory była wymagana toointegrate w dwóch osobnych systemach.  Witaj **punktu końcowego v2.0 usługi Azure AD** wprowadziła nową wersję interfejsu API uwierzytelniania, umożliwiający toosign w obu typów kont przy użyciu jednego prostą integrację.  Aplikacji korzystających z punktu końcowego v2.0 hello można również używać interfejsów API REST z hello [Microsoft Graph](https://graph.microsoft.io) za pomocą dowolnego typu konta.

## <a name="getting-started"></a>Wprowadzenie
Wybierz preferowaną platformę z powitania po toobuild listę aplikacji za pomocą naszych biblioteki typu open source & struktury.  Alternatywnie możesz użyć naszych OAuth 2.0 & OpenID Connect toosend dokumentacji protokołu i odbierać komunikaty protokołu bezpośrednio, bez przy użyciu biblioteki uwierzytelniania.

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a>Co nowego
tutaj informacje Hello będzie przydatna zrozumieć, co to jest & co nie jest możliwe z punktem końcowym v2.0 hello.

* Dowiedz się więcej o hello [typy aplikacji, można tworzyć za pomocą punktu końcowego v2.0 hello](active-directory-v2-flows.md).
* Zrozumienie hello [ograniczenia, ograniczenia i ograniczenia](active-directory-v2-limitations.md) z punktem końcowym v2.0 hello.
* Wyewidencjonuj ten przegląd wideo dla punktu końcowego v2.0 hello:

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a>Dokumentacja
Te linki przydadzą się do eksplorowania hello platform szczegółowo:

* [Dokumentacja protokołu v2.0](active-directory-v2-protocols.md)
* [Odwołania do tokenu w wersji 2.0](active-directory-v2-tokens.md)
* [Odwołanie do biblioteki w wersji 2.0](active-directory-v2-libraries.md)
* [Zakresy i zgody w hello punktu końcowego v2.0](active-directory-v2-scopes.md)
* [Witaj Microsoft Graph](https://graph.microsoft.io)

## <a name="help--support"></a>Pomoc i obsługa techniczna
Są to hello najlepsze miejsca tooget pomoc dotyczącą tworzenia w usłudze Azure Active Directory.

* [Tagi `azure-active-directory` i `adal` w witrynie Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [Opinia o usłudze Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> Jeśli wymagane jest tylko toosign kont służbowych z usługą Azure Active Directory, należy zacząć z naszych [przewodnik dewelopera usługi Azure AD](active-directory-developers-guide.md).  punktu końcowego v2.0 Hello jest przeznaczony do użycia przez deweloperów, którzy muszą jawnie toosign osobistego konta Microsoft.

