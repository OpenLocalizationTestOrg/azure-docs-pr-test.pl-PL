---
title: "interfejsu API raportowania usługi Azure AD hello tooaccess aaaPrerequisites | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o API raportowania hello wymagania wstępne tooaccess hello Azure AD"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>Wymagania wstępne tooaccess hello Azure AD raportowania interfejsu API

Witaj [raportowania interfejsów API usługi Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) umożliwiają dostęp programistyczny toohello danych za pomocą zestawu opartego na interfejsie REST API. Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.

Witaj reporting używa interfejsu API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize dostępu toohello interfejsów API sieci web. 

tooget uzyskiwać dostęp do interfejsu API hello toohello danych raportowania, należy toohave jedną powitania po przypisanych ról:

- Czytnik zabezpieczeń
- Administrator zabezpieczeń
- Administrator globalny


tooprepare z interfejsem API raportowania toohello dostępu, musi:

1. Rejestrowanie aplikacji 
2. Udzielanie uprawnień 
3. Zbierz ustawienia konfiguracji 

Pytania, problemy lub opinie, użyj funkcji [pliku biletu pomocy technicznej](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).

## <a name="register-an-azure-active-directory-application"></a>Rejestrowanie aplikacji usługi Azure Active Directory

Należy tooregister aplikacji, nawet jeśli uzyskują dostęp do hello raportowania interfejsu API za pomocą skryptu. Zapewnia to **identyfikator aplikacji**, który jest wymagany przez wywołanie autoryzacji i umożliwia tokenów tooreceive kodu.

tooconfigure katalogu tooaccess hello Azure AD raportowania interfejsu API, musisz zalogować się toohello portalu Azure przy użyciu konta administratora platformy Azure, który jest również członkiem hello **administratora globalnego** roli katalogu w dzierżawie usługi Azure AD .

> [!IMPORTANT]
> Aplikacje uruchomione w ramach poświadczeń z uprawnieniami "Administrator", jak mogą być bardzo zaawansowane, więc należy być bezpieczne czy tookeep hello identyfikator/klucz tajny poświadczenia aplikacji.
> 


**tooregister aplikację usługi Azure Active Directory:**

1. W hello [portalu Azure](https://portal.azure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Na powitania **usługi Azure Active Directory** bloku, kliknij przycisk **rejestracji aplikacji**.

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. Na powitania **rejestracji aplikacji** bloku na powitania narzędzi u góry hello kliknij **nowej rejestracji aplikacji**.

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. Na powitania **Utwórz** blok, wykonaj następujące kroki hello:

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    a. W hello **nazwa** pole tekstowe, typ `Reporting API application`.

    b. Jako **typu aplikacji**, wybierz pozycję **aplikacji sieci Web / interfejs API**.

    c. W hello **adres URL logowania** pole tekstowe, typ `https://localhost`.

    d. Kliknij przycisk **Utwórz**. 


## <a name="grant-permissions"></a>Udzielanie uprawnień 

Celem tego kroku Hello jest toogrant aplikacji **odczytuj dane katalogu** toohello uprawnienia **Windows Azure Active Directory** interfejsu API.

![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

**toogrant Twojego hello toouse uprawnienia aplikacji interfejsu API:**

1. Na powitania **rejestracji aplikacji** bloku, na liście aplikacji hello, kliknij przycisk **aplikacji interfejsu API raportowania**.

2. Na powitania **aplikacji interfejsu API raportowania** bloku na powitania narzędzi u góry hello kliknij **ustawienia**. 

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. Na powitania **ustawienia** bloku, kliknij przycisk **wymagane uprawnienia**. 

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. Na powitania **wymagane uprawnienia** bloku w hello **interfejsu API** kliknij **Windows Azure Active Directory**. 

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. Na powitania **Włącz dostęp** bloku, wybierz opcję **odczytuj dane katalogu**. 

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. Witaj pasku narzędzi u góry hello, kliknij przycisk **zapisać**.

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a>Zbierz ustawienia konfiguracji 
W tej sekcji opisano sposób hello tooget następujące ustawienia z katalogu:

* Nazwa domeny
* Identyfikator klienta
* Klucz tajny klienta

Należy korzystać z tych wartości podczas konfigurowania raportowania interfejsu API toohello wywołania. 

### <a name="get-your-domain-name"></a>Pobierz nazwę domeny

**tooget nazwy domeny:**

1. W hello [portalu Azure](https://portal.azure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Na powitania **usługi Azure Active Directory** bloku, kliknij przycisk **nazwy domen**.

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. Skopiuj nazwę domeny z hello listy domen.


### <a name="get-your-applications-client-id"></a>Pobieranie Identyfikatora klienta aplikacji

**tooget identyfikator klienta aplikacji:**

1. W hello [portalu Azure](https://portal.azure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Na powitania **rejestracji aplikacji** bloku, na liście aplikacji hello, kliknij przycisk **aplikacji interfejsu API raportowania**.

3. Na powitania **aplikacji interfejsu API raportowania** bloku na powitania **identyfikator aplikacji**, kliknij przycisk **kliknij toocopy**.

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a>Pobierz klucz tajny klienta aplikacji
tooget klienta aplikacji tajne, należy toocreate nowy klucz i zapisz jego wartości podczas zapisywania nowego klucza hello, ponieważ nie jest możliwe tooretrieve później już tej wartości.

**tooget klucz tajny klienta aplikacji:**

1. W hello [portalu Azure](https://portal.azure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Na powitania **rejestracji aplikacji** bloku, na liście aplikacji hello, kliknij przycisk **aplikacji interfejsu API raportowania**.


3. Na powitania **aplikacji interfejsu API raportowania** bloku na powitania narzędzi u góry hello kliknij **ustawienia**. 

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. Na powitania **ustawienia** bloku w hello **dostępu APIR** kliknij **klucze**. 

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. Na powitania **klucze** blok, wykonaj następujące kroki hello:

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    a. W hello **opis** pole tekstowe, typ `Reporting API`.

    b. Jako **Expires**, wybierz pozycję **w 2 lata**.

    c. Kliknij pozycję **Zapisz**.

    d. Skopiuj wartość klucza hello.


## <a name="next-steps"></a>Następne kroki
* Czy można tak, jak dane z usługi Azure AD hello hello tooaccess raportowania interfejsu API w sposób programowy Zapoznaj się z [wprowadzenie hello Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).
* Jeśli chcesz toofind się więcej o usłudze Azure Active Directory, zobacz hello [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).  

