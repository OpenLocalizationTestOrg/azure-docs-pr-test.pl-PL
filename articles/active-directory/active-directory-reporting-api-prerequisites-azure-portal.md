---
title: "Wymagania wstępne dotyczące dostępu raportowania interfejsu API usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o wymaganiach wstępnych można uzyskać dostępu do raportowania interfejsu API usługi Azure AD"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/14/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f1f4d79b59d44bc1c151391290e79026051fe1df
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a>Wymagania wstępne dotyczące raportowania interfejsu API usługi Azure AD dostęp

[Raportowania interfejsów API usługi Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) umożliwiają programowy dostęp do danych za pomocą zestawu opartego na interfejsie REST API. Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.

Raportowania używa interfejsu API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) do autoryzacji dostępu do interfejsów API sieci web. 

Aby uzyskać dostęp do danych raportowania za pośrednictwem interfejsu API, należy mieć jeden z następujących ról przypisane:

- Czytnik zabezpieczeń
- Administrator zabezpieczeń
- Administrator globalny


Aby przygotować dostęp do interfejsu API raportowania, należy:

1. Rejestrowanie aplikacji 
2. Udzielanie uprawnień 
3. Zbierz ustawienia konfiguracji 

Pytania, problemy lub opinie, użyj funkcji [pliku biletu pomocy technicznej](https://docs.microsoft.com/azure/active-directory/active-directory-troubleshooting-support-howto).

## <a name="register-an-azure-active-directory-application"></a>Rejestrowanie aplikacji usługi Azure Active Directory

Należy zarejestrować aplikację, nawet jeśli uzyskują dostęp do interfejsu API raportowania przy użyciu skryptu. Zapewnia to **identyfikator aplikacji**, który jest wymagany przez wywołanie autoryzacji i umożliwia swój kod, aby odbierać tokeny.

Aby skonfigurować dostęp raportowania interfejsu API usługi Azure AD do katalogu, należy zalogować się do portalu Azure przy użyciu konta administratora platformy Azure, który jest również członkiem **administratora globalnego** roli katalogu w dzierżawie usługi Azure AD.

> [!IMPORTANT]
> Aplikacje uruchomione w ramach poświadczeń z uprawnieniami "Administrator", jak mogą być bardzo zaawansowane, więc Pamiętaj zapewnić bezpieczeństwo poświadczeń identyfikator/klucz tajny aplikacji.
> 


**Aby zarejestrować aplikację usługi Azure Active Directory:**

1. W [portalu Azure](https://portal.azure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory**.
   
    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Na **usługi Azure Active Directory** bloku, kliknij przycisk **rejestracji aplikacji**.

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. Na **rejestracji aplikacji** bloku na pasku narzędzi u góry, kliknij przycisk **nowej rejestracji aplikacji**.

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. Na **Utwórz** blok, wykonaj następujące czynności:

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    a. W **nazwa** pole tekstowe, typ `Reporting API application`.

    b. Jako **typu aplikacji**, wybierz pozycję **aplikacji sieci Web / interfejs API**.

    c. W **adres URL logowania** pole tekstowe, typ `https://localhost`.

    d. Kliknij przycisk **Utwórz**. 


## <a name="grant-permissions"></a>Udzielanie uprawnień 

Celem tego etapu jest udzielić aplikacji **odczytuj dane katalogu** uprawnień do **Windows Azure Active Directory** interfejsu API.

![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

**Aby udzielić zgody użytkownika aplikacji do użycia interfejsu API:**

1. Na **rejestracji aplikacji** bloku na liście aplikacji, kliknij przycisk **aplikacji interfejsu API raportowania**.

2. Na **aplikacji interfejsu API raportowania** bloku na pasku narzędzi u góry, kliknij przycisk **ustawienia**. 

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. Na **ustawienia** bloku, kliknij przycisk **wymagane uprawnienia**. 

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. Na **wymagane uprawnienia** bloku, w **interfejsu API** kliknij **Windows Azure Active Directory**. 

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. Na **Włącz dostęp** bloku, wybierz opcję **odczytuj dane katalogu**. 

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. Na pasku narzędzi u góry kliknij **zapisać**.

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

7. Kliknij przycisk **udzielanie uprawnień**, a następnie kliknij przycisk **tak**.

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/17.png)


## <a name="gather-configuration-settings"></a>Zbierz ustawienia konfiguracji 
W tej sekcji przedstawiono sposób uzyskać następujące ustawienia z katalogiem:

* Nazwa domeny
* Identyfikator klienta
* Klucz tajny klienta

Te wartości są wymagane podczas konfigurowania wywołania interfejsu API raportowania. 

### <a name="get-your-domain-name"></a>Pobierz nazwę domeny

**Aby uzyskać nazwy domeny:**

1. W [portalu Azure](https://portal.azure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory**.
   
    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Na **usługi Azure Active Directory** bloku, kliknij przycisk **niestandardowych nazw domen**.

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. Skopiuj nazwę domeny, z listy domen.


### <a name="get-your-applications-client-id"></a>Pobieranie Identyfikatora klienta aplikacji

**Aby uzyskać identyfikator klienta aplikacji:**

1. W [portalu Azure](https://portal.azure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory**.
   
    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Na **rejestracji aplikacji** bloku na liście aplikacji, kliknij przycisk **aplikacji interfejsu API raportowania**.

3. Na **aplikacji interfejsu API raportowania** bloku na **identyfikator aplikacji**, kliknij przycisk **kliknij, aby skopiować**.

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a>Pobierz klucz tajny klienta aplikacji
Aby uzyskać klucz tajny klienta aplikacji, musisz utworzyć nowy klucz i zapisać jego wartości podczas zapisywania nowego klucza, ponieważ nie jest możliwe później już pobierania tej wartości.

**Aby uzyskać klucz tajny klienta aplikacji:**

1. W [portalu Azure](https://portal.azure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory**.
   
    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Na **rejestracji aplikacji** bloku na liście aplikacji, kliknij przycisk **aplikacji interfejsu API raportowania**.


3. Na **aplikacji interfejsu API raportowania** bloku na pasku narzędzi u góry, kliknij przycisk **ustawienia**. 

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. Na **ustawienia** bloku, w **dostępu APIR** kliknij **klucze**. 

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. Na **klucze** blok, wykonaj następujące czynności:

    ![Zarejestruj aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    a. W **opis** pole tekstowe, typ `Reporting API`.

    b. Jako **Expires**, wybierz pozycję **w 2 lata**.

    c. Kliknij pozycję **Zapisz**.

    d. Skopiuj wartość klucza.


## <a name="next-steps"></a>Następne kroki
* Czy chcesz uzyskać dostęp do danych raportowania interfejsu API w sposób programowy usługi Azure AD? Zapoznaj się z [wprowadzenie do usługi Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).
* Jeśli chcesz dowiedzieć się więcej o usłudze Azure Active Directory, zobacz [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).  

