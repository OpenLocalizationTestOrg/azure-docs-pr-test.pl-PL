---
title: 'Samouczek: Integracji Azure Active Directory z SAP HANA Cloud Platform | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse SAP HANA Cloud Platform z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>Samouczek: integracja usługi Azure Active Directory z platformą w chmurze SAP HANA
Celem Hello tego samouczka jest tooshow integracji hello Azure i SAP HANA Cloud Platform.

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

* Ważnej subskrypcji platformy Azure
* Konta programu SAP HANA Cloud Platform

Ten samouczek hello użytkowników usługi Azure AD przypisano tooSAP HANA Cloud Platform będzie możliwe toosingle logowania do aplikacji hello przy użyciu hello [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

>[!IMPORTANT]
>Należy toodeploy własnej aplikacji lub subskrypcja tooan aplikacji na platformie chmury SAP HANA pojedynczego tootest konta logowania. W tym samouczku aplikacja jest wdrażana na koncie hello.
> 
> 

Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:

1. Włączanie integracji aplikacji hello SAP HANA chmury platformy
2. Konfigurowanie rejestracji jednokrotnej (SSO)
3. Przypisanie roli użytkownika tooa
4. Przypisywanie użytkowników

![Scenariusz](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "scenariusza")

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a>Włączanie integracji aplikacji hello SAP HANA chmury platformy
Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable platformy chmury SAP HANA.

**Integracja aplikacji hello tooenable platformy SAP HANA chmury, wykonaj hello następujące kroki:**

1. W hello portalu zarządzania Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.
   
    ![Usługi Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "usługi Active Directory")
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Aplikacje](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "aplikacji")
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Dodaj aplikację](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Dodaj aplikację")
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
    ![Dodawanie aplikacji z gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "dodać aplikację z gallerry")
6. W hello **pole wyszukiwania**, typ **SAP HANA Cloud Platform**.
   
    ![Galerii aplikacji](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "galerii aplikacji")
7. Wybierz w okienku wyników hello **SAP HANA Cloud Platform**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>Konfigurowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooSAP HANA Cloud Platform do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.

W ramach tej procedury jest wymagana tooupload dzierżawcy SAP HANA Cloud Platform tooyour base-64 zakodowanego certyfikatu.  

Jeśli nie masz doświadczenia z tej procedury, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure na powitania **SAP HANA Cloud Platform** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną**okna dialogowego.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "skonfigurować logowanie jednokrotne")
2. Na powitania **jak ma toosign użytkowników na tooSAP platformy w chmurze HANA** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "skonfigurować logowanie jednokrotne")
3. W oknie przeglądarki sieci web inną logowania toohello SAP HANA Cloud Platform w Panelu sterowania na https://account. \<hosta pozioma\>.ondemand.com/cockpit (np.: *https://account.hanatrial.ondemand.com/cockpit*).
4. Kliknij przycisk hello **zaufania** kartę.
   
    ![Zaufania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "zaufania")
5. W sekcji Zarządzanie zaufania należy wykonać hello następujące kroki:
   
    ![Pobranie metadanych](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "pobranie metadanych")
   
   1. Kliknij przycisk hello **lokalnego dostawcy usług** kartę.
   2. toodownload hello SAP HANA Cloud Platform pliku metadanych, kliknij przycisk **pobrać metadanych**.
6. W hello Azure Active klasycznego portalu na powitania **Konfigurowanie adresu URL aplikacji** , wykonaj następujące kroki hello, a następnie kliknij przycisk **dalej**.
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "skonfigurować adres URL aplikacji")
   
   1. W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używany przez Twoje toosign użytkowników w Twojej **SAP HANA Cloud Platform** aplikacji. To jest adres URL dotyczący konta hello zasobu chronionego w aplikacji platformy chmury SAP HANA. Witaj adres URL jest oparta na powitania następującego wzorca: *https://\<applicationName\>\<accountName\>.\< host pozioma\>.ondemand.com/\<ścieżki\_do\_chronione\_zasobów\>*  (np.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >To jest adres URL hello w aplikacji SAP HANA Cloud Platform, która wymaga hello tooauthenticate użytkownika.
     > 

   2. Otwórz plik metadanych platformy chmury SAP HANA hello pobrane, a następnie zlokalizuj hello **ns3:AssertionConsumerService** tagu.
   3. Skopiuj wartość hello hello **lokalizacji** atrybutu, a następnie wklej go do hello **SAP HANA Cloud Platform adres URL odpowiedzi służący** pola tekstowego.

7. Na powitania **skonfigurować logowanie jednokrotne w SAP HANA Cloud Platform** strony, toodownload metadanych programu kliknij **pobierania metadanych**, a następnie zapisz plik hello na tym komputerze.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "skonfigurować logowanie jednokrotne")
8. Na powitania SAP HANA Cloud Platform Panelu sterowania, w hello **lokalnego dostawcy usług** sekcji, wykonaj następujące kroki hello:
   
    ![Zaufania zarządzania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "zaufania zarządzania")
   
  1. Kliknij pozycję **Edytuj**.
  2. Jako **typu konfiguracji**, wybierz pozycję **niestandardowy**.
  3. Jako **lokalna nazwa dostawcy**, pozostaw wartość domyślną hello.
  4. toogenerate **klucza podpisywania** i **certyfikat podpisywania** parę kluczy, kliknij przycisk **generowanie pary klucz**.
  5. Jako **główna propagacji**, wybierz pozycję **wyłączone**.
  6. Jako **siły uwierzytelniania**, wybierz pozycję **wyłączone**.
  7. Kliknij pozycję **Zapisz**.

9. Kliknij przycisk hello **zaufany dostawca tożsamości** , a następnie kliknij pozycję **dodać zaufanego dostawcę tożsamości**.
   
    ![Zaufania zarządzania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "zaufania zarządzania")
   
    >[!NOTE]
    >toomanage hello listy zaufanych dostawców tożsamości, należy toohave wybrany hello niestandardowy typ konfiguracji w hello sekcji lokalnego dostawcy usług. Typ konfiguracji domyślnej masz toohello zaufania nie można edytować i niejawne SAP Identyfikatora usługi. Dla żadnego nie masz żadnych ustawień zaufania.
    > 
    > 

10. Kliknij przycisk hello **ogólne** , a następnie kliknij pozycję **Przeglądaj** tooupload hello pobrany plik metadanych.
    
    ![Zaufania zarządzania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "zaufania zarządzania")
    
    >[!NOTE]
    >Po przekazaniu pliku metadanych hello, wartości hello **URL rejestracji jednokrotnej**, **pojedynczego adresu URL wylogowania** i **certyfikat podpisywania** są wypełniane automatycznie.
    > 
    > 

11. Kliknij przycisk hello **atrybuty** kartę.
12. Na powitania **atrybuty** karcie, wykonaj powitania po kroku:
    
    ![Atrybuty](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "atrybutów") 
  * Kliknij przycisk **atrybutu Add Assertion-Based**, a następnie dodaj następujące atrybuty oparte na potwierdzenie hello:
       
    | Atrybut potwierdzenia | Atrybut podmiotu |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/givenName |Imię |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/surname |nazwisko |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/emailaddress |Adres e-mail 
   
     >[!NOTE]
     >Konfiguracja Hello atrybutów hello zależy od tego, jak aplikacji hello na HCP są tworzone, tj. atrybuty, które oczekiwanym hello odpowiedzi SAML i w których nazwa (atrybut podmiotu zabezpieczeń) będą uzyskiwać dostęp do tego atrybutu w kodzie hello.
     > 
     >  

    1.  Witaj **domyślny atrybut** w hello zrzut ekranu jest tylko do celów ilustracyjnych. Nie jest wymagane toomake hello scenariusz pracy.   
    2.  Witaj nazwy i wartości dla **atrybut podmiotu zabezpieczeń** pokazano hello zrzut ekranu zależą od tego, jak aplikacja hello został utworzony. Istnieje możliwość, że aplikacja wymaga innego mapowania.
     
13. W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w SAP HANA Cloud Platform** dialogu strony, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "skonfigurować logowanie jednokrotne")

###<a name="assertion-based-groups"></a>Grupy oparte na potwierdzenie
Ten opcjonalny krok można skonfigurować grupy oparte na potwierdzenie dla usługi Azure Active Directory dostawcy tożsamości.

Na platformie programu SAP HANA chmury przy użyciu grup umożliwia przypisanie toodynamically, jeden lub więcej użytkowników tooone lub więcej ról w aplikacjach platformy chmury SAP HANA określany przez wartości atrybutów w hello SAML 2.0 potwierdzenia. 

Na przykład jeśli hello potwierdzenia zawiera atrybut hello "*kontraktu = tymczasowego*", wszystkie grupy dodano toohello toobe użytkowników może być"*tymczasowego*". grupy Hello "*tymczasowego*" może zawierać co najmniej jedną rolę z co najmniej jednej aplikacji wdrożonych na koncie platformy chmury SAP HANA.
 
Grupy oparte na potwierdzenie należy użyć toosimultaneously przypisać wielu użytkowników tooone lub więcej ról aplikacji na koncie platformy chmury SAP HANA. Jeśli chcesz tooassign tylko jednego lub małej liczby użytkowników toospecific ról, zalecamy przypisywania do nich bezpośrednio w hello "**autoryzacje**" hello SAP HANA Cloud Platform w Panelu sterowania na karcie.

## <a name="assign-a-role-tooa-user"></a>Przypisywanie roli użytkownika tooa
W kolejności tooenable usługi Azure AD użytkownicy toolog do programu SAP HANA Cloud Platform należy przypisać role w hello toothem SAP HANA Cloud Platform.

**tooassign tooa roli użytkownika, wykonaj następujące kroki hello:**

1. Zaloguj się za tooyour **SAP HANA Cloud Platform** Panelu sterowania.
2. Wykonaj następujące hello:
   
   ![Autoryzacje](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "zezwolenia")
   
  1. Kliknij przycisk **autoryzacji**.
  2. Kliknij przycisk hello **użytkowników** kartę.
  3. W hello **użytkownika** pole tekstowe, typ hello adres e-mail użytkownika.
  4. Kliknij przycisk **przypisać** tooassign hello użytkownika tooa roli.
  5. Kliknij pozycję **Zapisz**.

## <a name="assign-users"></a>Przypisywanie użytkowników
tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.

**tooassign użytkowników tooSAP HANA platformy w chmurze, należy wykonać hello następujące kroki:**

1. W hello klasycznego portalu Azure Utwórz konto testu.
2. Na powitania **SAP HANA Cloud Platform** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.
   
   ![Przypisywanie użytkowników](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "przypisywanie użytkowników")
3. Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.
   
   ![Tak](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "tak")

Jeśli chcesz tootest ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

