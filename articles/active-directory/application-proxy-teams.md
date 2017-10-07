---
title: "aplikacje serwera Proxy aplikacji usługi Azure AD w zespołach aaaAccess | Dokumentacja firmy Microsoft"
description: "Za pomocą serwera Proxy aplikacji usługi Azure AD tooaccess aplikacji lokalnej za pośrednictwem Teams firmy Microsoft."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a>Dostęp do aplikacji lokalnych poprzez Teams firmy Microsoft

Azure Active Directory serwera Proxy aplikacji daje pojedynczy znak tooon lokalnych aplikacji niezależnie od tego, gdzie się znajdujesz i Teams firmy Microsoft upraszcza współpracy wysiłków w jednym miejscu. Integrowanie hello dwa razem oznacza, że użytkownicy mogą produktywność z ich członków zespołu w każdej sytuacji. 

Użytkownicy mogą dodawać chmury aplikacji tootheir zespołów kanałów [przy użyciu karty](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), ale co się stanie, jeśli jest w tej witrynie programu SharePoint lub narzędzie do planowania wszyscy korzystają z obsługiwanego lokalnie? Serwer Proxy aplikacji jest hello rozwiązania. Można dodać aplikacji opublikowanych przy użyciu serwera Proxy aplikacji tootheir kanałów przy użyciu hello tego samego zewnętrzne adresy URL zawsze korzystają z tooaccess swoje aplikacje zdalnie. I ponieważ uwierzytelnia serwer Proxy aplikacji za pomocą usługi Azure Active Directory, hello tego samego posiada środowisko rejestracji jednokrotnej za pośrednictwem.


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a>Instalowanie łącznika serwera Proxy aplikacji hello i publikowanie aplikacji

Jeśli nie jest jeszcze, [skonfigurować serwer Proxy aplikacji dzierżawy i zainstalować łącznik hello](active-directory-application-proxy-enable.md). Następnie [opublikować aplikację lokalną](application-proxy-publish-azure-portal.md) dostępu zdalnego. W przypadku publikowania aplikacji hello, zwróć uwagę na powitania zewnętrznego adresu URL, ponieważ użytkownicy końcowi muszą tych informacji podczas dodawania tooTeams aplikacji hello.

Jeśli już masz aplikacje opublikowane, ale nie zapamiętuj ich zewnętrzne adresy URL, wyszukaj je hello [portalu Azure](https://portal.azure.com). Zaloguj się, a następnie przejdź zbyt**usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje** > Wybierz aplikacji > **Serwera proxy aplikacji**.

## <a name="add-your-app-tooteams"></a>Dodaj tooTeams Twojej aplikacji

Po opublikowaniu aplikacji hello za pośrednictwem serwera Proxy aplikacji, należy poinformować użytkowników, że ich go dodać na karcie bezpośrednio w ich kanały zespołów. Niech wykonaj następujące trzy kroki:

1. Przejdź toohello zespołów kanału miejscu tooadd tej aplikacji i wybierz  **+**  tooadd karty.

   ![Wybierz opcję Dodaj kartę](./media/application-proxy-teams/add-tab.png)

2. Wybierz **witryny sieci Web** hello kartę Opcje.

   ![Dodaj witrynę sieci Web](./media/application-proxy-teams/website.png)

3. Nadaj nazwę hello kartę i ustawić hello adresu URL toohello serwera Proxy aplikacji zewnętrznego adresu URL. 

   ![Skonfiguruj kartę nazwy i adresu URL](./media/application-proxy-teams/tab-name-url.png)

Po jednego członka do zespołu dodaje kartę hello, jest wyświetlane dla wszystkich użytkowników w kanale hello. Wszyscy użytkownicy, którzy mają dostęp do aplikacji toohello korzystać pojedynczego logowania jednokrotnego przy użyciu poświadczeń hello, używanego dla Teams firmy Microsoft. Wszyscy użytkownicy, którzy nie mają dostępu do aplikacji toohello zostanie wyświetlony na karcie hello w zespołach, ale dopóki przysługujące im uprawnienia toohello lokalnej aplikacji i hello Azure portalu opublikowanej wersji aplikacji hello są blokowane. 

## <a name="next-steps"></a>Następne kroki

- Dowiedz się, jak za[publikowanie witryn programu SharePoint lokalnymi](application-proxy-enable-remote-access-sharepoint.md) z serwerem Proxy aplikacji.
- Skonfiguruj toouse Twoje aplikacje [domen niestandardowych](active-directory-application-proxy-custom-domains.md) dla ich zewnętrznego adresu URL. 
