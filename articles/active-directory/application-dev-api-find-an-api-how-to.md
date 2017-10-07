---
title: toofind aaaHow interfejsu API wymagane dla aplikacji utworzonych niestandardowych | Dokumentacja firmy Microsoft
description: "Jak należy tooaccess określony interfejs API w niestandardowe uprawnienia hello tooconfigure opracowała aplikację usługi Azure AD"
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a>Jak toofind określonego interfejsu API wymagane dla aplikacji utworzonych niestandardowych

TooAPIs dostępu wymagają konfiguracji, zakresów dostępu i ról. Jeśli chcesz tooexpose zasobów aplikacji sieci web API tooclient aplikacji, należy tooconfigure zakresów dostępu i role dla hello interfejsu API. Jeśli chcesz tooaccess aplikacji klienta interfejsu API sieci web, należy tooconfigure uprawnienia tooaccess hello API w rejestracji aplikacji hello.

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Konfigurowanie zasobów aplikacji tooexpose interfejsów API sieci web

Gdy uwidacznia interfejs API, sieci web hello interfejsu API można wyświetlić w hello **wybierz interfejs API** listy podczas dodawania rejestracji aplikacji tooan uprawnienia. zakresy dostępu tooadd, wykonaj kroki hello opisane w temacie [Dodawanie dostępu zakresów aplikacji zasobów tooyour](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).

## <a name="configuring-a-client-application-tooaccess-web-apis"></a>Konfigurowanie klienta aplikacji tooaccess interfejsów API sieci web

Po dodaniu rejestracji aplikacji tooyour uprawnienia można **dodać dostępu do interfejsu API** tooexposed interfejsów API sieci web. tooaccess interfejsów API sieci web, wykonaj czynności hello opisane w temacie [dodać interfejsów API sieci web tooaccess poświadczeń lub uprawnienia](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).

## <a name="next-steps"></a>Następne kroki

-   [Integrating applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications) (Integrowanie aplikacji za pomocą usługi Azure Active Directory)

-   [Opis manifestu aplikacji hello Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


