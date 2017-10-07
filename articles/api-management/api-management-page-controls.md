---
title: "Formanty strony Zarządzanie interfejsami API aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat formantów strony hello dostępne do użycia w szablonach portalu deweloperów w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a>Formanty strony Zarządzanie interfejsami API Azure
Zarządzanie interfejsami API Azure udostępnia powitania po formanty do użycia w szablonach portalu deweloperów hello.  
  
 toouse formantu, umieścić go w lokalizacji hello żądanego szablonu portalu deweloperów hello. Niektóre formanty, takie jak hello [akcje aplikacji](#app-actions) kontrolować, ma parametry, jak przedstawiono na powitania poniższy przykład.  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 Witaj wartości parametrów hello są przekazywane w jako część modelu danych hello hello szablonu. W większości przypadków, możesz po prostu wkleić hello podać przykład dla każdego formantu dla niego toowork poprawnie. Aby uzyskać więcej informacji na wartości parametrów hello widać hello sekcji modelu danych do każdego szablonu, w którym można użyć formantu.  
  
 Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
## <a name="developer-portal-template-page-controls"></a>Formantów strony szablonu portalu dla deweloperów  
  
-   [Akcje aplikacji](#app-actions)  
  
-   [Rejestrowanie Basic](#basic-signin)  
  
-   [Formant stronicowania](#paging-control)  
  
-   [dostawców](#providers)  
  
-   [formant wyszukiwania](#search-control)  
  
-   [rejestracji](#sign-up)  
  
-   [przycisk subskrypcji](#subscribe-button)  
  
-   [Anuluj subskrypcję](#subscription-cancel)  
  
##  <a name="app-actions"></a>Akcje aplikacji  
 Witaj `app-actions` kontroli udostępnia interfejs użytkownika do interakcji z aplikacjami na powitania strony profilu użytkownika w portalu dla deweloperów hello.  
  
 ![& #45 aplikacji; kontrolka akcje](./media/api-management-page-controls/APIM-app-actions-control.png "APIM kontroli akcje aplikacji")  
  
### <a name="usage"></a>Sposób użycia  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>Parametry  
  
|Parametr|Opis|  
|---------------|-----------------|  
|Identyfikator aplikacji|Identyfikator Hello aplikacji hello.|  
  
### <a name="developer-portal-templates"></a>Szablony portalu dla deweloperów  
 Witaj `app-actions` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.  
  
-   [Aplikacje](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a>Rejestrowanie Basic  
 Witaj `basic-signin` kontroli udostępnia kontrolkę do zbierania informacji w hello logowania użytkownika Zaloguj się na stronie w portalu dla deweloperów hello.  
  
 ![Basic &#45; kontrolka signin](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic Rejestrowanie formantu")  
  
### <a name="usage"></a>Sposób użycia  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>Parametry  
 Brak.  
  
### <a name="developer-portal-templates"></a>Szablony portalu dla deweloperów  
 Witaj `basic-signin` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.  
  
-   [Rejestrowanie](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a>Formant stronicowania  
 Witaj `paging-control` zawiera funkcje stronicowania po developer portal stron, które wyświetlania listy elementów.  
  
 ![stronicowanie kontroli](./media/api-management-page-controls/APIM-paging-control.png "APIM formant stronicowania")  
  
### <a name="usage"></a>Sposób użycia  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>Parametry  
 Brak.  
  
### <a name="developer-portal-templates"></a>Szablony portalu dla deweloperów  
 Witaj `paging-control` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.  
  
-   [Lista interfejsu API](api-management-api-templates.md#APIList)  
  
-   [Lista problemów](api-management-issue-templates.md#IssueList)  
  
-   [Lista produktów](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a>dostawców  
 Witaj `providers` kontroli udostępnia kontrolkę wyboru dostawcy uwierzytelniania w hello stronę w portalu dla deweloperów hello logowania.  
  
 ![Formant dostawców](./media/api-management-page-controls/APIM-providers-control.png "APIM dostawców kontroli")  
  
### <a name="usage"></a>Sposób użycia  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>Parametry  
 Brak.  
  
### <a name="developer-portal-templates"></a>Szablony portalu dla deweloperów  
 Witaj `providers` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.  
  
-   [Rejestrowanie](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a>formant wyszukiwania  
 Witaj `search-control` udostępnia funkcje wyszukiwania na deweloperów na stronach portalu zawierające listę elementów.  
  
 ![Wyszukaj kontroli](./media/api-management-page-controls/APIM-search-control.png "APIM formant wyszukiwania")  
  
### <a name="usage"></a>Sposób użycia  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>Parametry  
 Brak.  
  
### <a name="developer-portal-templates"></a>Szablony portalu dla deweloperów  
 Witaj `search-control` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.  
  
-   [Lista interfejsu API](api-management-api-templates.md#APIList)  
  
-   [Lista produktów](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a>rejestracji  
 Witaj `sign-up` kontroli udostępnia kontrolkę do zbierania informacji o profilu użytkownika w stronę w portalu dla deweloperów hello hello konta.  
  
 ![znak &#45; w górę kontrolki](./media/api-management-page-controls/APIM-sign-up-control.png "APIM zapisywania kontrolki")  
  
### <a name="usage"></a>Sposób użycia  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>Parametry  
 Brak.  
  
### <a name="developer-portal-templates"></a>Szablony portalu dla deweloperów  
 Witaj `sign-up` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.  
  
-   [Zarejestruj się](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a>przycisk subskrypcji  
 Witaj `subscribe-button` udostępnia kontrolkę do subskrypcji produktu tooa użytkownika.  
  
 ![Subskrypcja &#45; button — formant](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM formantu przycisku subskrypcji")  
  
### <a name="usage"></a>Sposób użycia  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>Parametry  
 Brak.  
  
### <a name="developer-portal-templates"></a>Szablony portalu dla deweloperów  
 Witaj `subscribe-button` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.  
  
-   [Produktu](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a>Anuluj subskrypcję  
 Witaj `subscription-cancel` kontroli udostępnia kontrolkę do anulowania subskrypcji produktu tooa hello strony profilu użytkownika w portalu dla deweloperów hello.  
  
 ![Subskrypcja &#45; Anuluj kontroli](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM kontroli Anuluj subskrypcję")  
  
### <a name="usage"></a>Sposób użycia  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>Parametry  
  
|Parametr|Opis|  
|---------------|-----------------|  
|subscriptionId|Identyfikator Hello hello toocancel subskrypcji.|  
|cancelUrl|Subskrypcja Hello anulować adresu URL.|  
  
### <a name="developer-portal-templates"></a>Szablony portalu dla deweloperów  
 Witaj `subscription-cancel` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.  
  
-   [Produktu](api-management-product-templates.md#Product)

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).
