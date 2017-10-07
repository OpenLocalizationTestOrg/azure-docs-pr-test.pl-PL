---
title: aaaHow toogrant uprawnienia tooa opracowany niestandardowych aplikacji | Dokumentacja firmy Microsoft
description: "Jak toogrant tooyour uprawnienia niestandardowe rozwiniętych hello aplikacji przy użyciu portalu usługi Azure AD lub parametr adresu URL"
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a>Jak toogrant tooa uprawnienia niestandardowe opracowanych aplikacji

Zgody toogrant preemptively w aplikacji lub wystąpił błąd działają, że nie wyrażono zgodę tooan aplikacji, spróbuj te czynności.

## <a name="how-tooperform-admin-consent-for-your-application"></a>Jak tooperform zgody administratora aplikacji

To ustawienie działa hello udzielania zgody toohello aplikacji dla wszystkich użytkowników w organizacji.

1. Przejdź toohello **rejestracji aplikacji** bloku jako **administratora globalnego**, a następnie wybierz pozycję aplikacji hello.

2. Wybierz **wymagane uprawnienia**, a na koniec trafienie hello **udzielanie uprawnień** u góry hello hello bloku.

Alternatywnie można konstruować żądanie zbyt*login.microsoftonline.com* z configs Twojej aplikacji i Dołącz na *& Monituj = admin\_zgody*. Po zarejestrowaniu się przy użyciu poświadczeń administratora, aplikacja hello udzielono zgody dla wszystkich użytkowników.

## <a name="how-tooforce-user-consent-for-your-application"></a>Jak tooforce zgody użytkownika dla aplikacji

* Dołącz do uwierzytelniania żądań *& Monituj = zgody* który żądania tooconsent użytkowników końcowych za każdym razem uwierzytelniania.

## <a name="next-steps"></a>Następne kroki

[Integrowanie aplikacji i zgody tooAzureAD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[Permissioning dla AzureAD w wersji 2.0 i zgody zbieżność aplikacji](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[AzureAD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
