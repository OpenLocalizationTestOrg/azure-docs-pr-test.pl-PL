---
title: 'Samouczek: Integracji Azure Active Directory z SAP HANA Cloud Platform | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak używać SAP HANA Cloud Platform z usługą Azure Active Directory w celu włączenia logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
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
ms.openlocfilehash: e03bc2410a8d57363c558f723b3bfd0e69b3f4c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>Samouczek: integracja usługi Azure Active Directory z platformą w chmurze SAP HANA
Celem tego samouczka jest pokazanie integracji Azure i SAP HANA Cloud Platform.

Scenariusz opisany w tym samouczku założono, że już następujące elementy:

* Ważnej subskrypcji platformy Azure
* Konta programu SAP HANA Cloud Platform

Ten samouczek użytkowników usługi Azure AD, zostały przypisane do SAP HANA Cloud Platform będzie można funkcji logowania jednokrotnego do aplikacji przy użyciu [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).

>[!IMPORTANT]
>Należy wdrożyć własną aplikację lub subskrybować aplikację na Twoim koncie SAP HANA Cloud Platform testowanie funkcji logowania jednokrotnego w. W tym samouczku aplikacja jest wdrażana w ramach konta.
> 
> 

Scenariusz opisany w tym samouczku składa się z następujących bloków konstrukcyjnych:

1. Włączanie integracji aplikacji dla programu SAP HANA Cloud Platform
2. Konfigurowanie rejestracji jednokrotnej (SSO)
3. Przypisywanie użytkownikowi roli
4. Przypisywanie użytkowników

![Scenariusz](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "scenariusza")

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a>Włączanie integracji aplikacji dla programu SAP HANA Cloud Platform
Celem tej sekcji jest przedstawiają sposób włączania integracji aplikacji dla platformy chmury SAP HANA.

**Aby włączyć integrację aplikacji dla programu SAP HANA Cloud Platform, wykonaj następujące czynności:**

1. W portalu zarządzania Azure, w okienku nawigacji po lewej stronie kliknij **usługi Active Directory**.
   
    ![Usługi Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "usługi Active Directory")
2. Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.
3. Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.
   
    ![Aplikacje](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "aplikacji")
4. Kliknij przycisk **Dodaj** w dolnej części strony.
   
    ![Dodaj aplikację](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Dodaj aplikację")
5. Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.
   
    ![Dodawanie aplikacji z gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "dodać aplikację z gallerry")
6. W **pole wyszukiwania**, typ **SAP HANA Cloud Platform**.
   
    ![Galerii aplikacji](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "galerii aplikacji")
7. W okienku wyników wybierz **SAP HANA Cloud Platform**, a następnie kliknij przycisk **Complete** można dodać aplikację.
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>Konfigurowanie rejestracji jednokrotnej

Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie platformy Chmurowej SAP HANA do swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.

W ramach tej procedury jest wymagane do przekazania zakodowanego certyfikatu base-64 w dzierżawie platformy chmury SAP HANA.  

Jeśli nie masz doświadczenia z tej procedury, zobacz [sposób konwertowania binarne certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)

**Aby skonfigurować rejestrację jednokrotną, wykonaj następujące czynności:**

1. W klasycznym portalu Azure na **SAP HANA Cloud Platform** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować rejestrację jednokrotną** okna dialogowego.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "skonfigurować logowanie jednokrotne")
2. Na **jak chcesz użytkownikom zalogować się do programu SAP HANA Cloud Platform** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "skonfigurować logowanie jednokrotne")
3. W oknie przeglądarki innej witryny sieci web Zaloguj się do panelu sterowania SAP HANA Cloud Platform w https://account. \<hosta pozioma\>.ondemand.com/cockpit (np.: *https://account.hanatrial.ondemand.com/cockpit*).
4. Kliknij przycisk **zaufania** kartę.
   
    ![Zaufania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "zaufania")
5. W sekcji Zarządzanie zaufania wykonaj następujące czynności:
   
    ![Pobranie metadanych](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "pobranie metadanych")
   
   1. Kliknij przycisk **lokalnego dostawcy usług** kartę.
   2. Aby pobrać pliku metadanych SAP HANA Cloud Platform, kliknij przycisk **pobrać metadanych**.
6. W portalu klasycznym Azure Active na **Konfigurowanie adresu URL aplikacji** , wykonaj następujące czynności, a następnie kliknij przycisk **dalej**.
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "skonfigurować adres URL aplikacji")
   
   1. W **na adres URL logowania** tekstowym, wpisz adres URL używany przez użytkowników do logowania się do sieci **SAP HANA Cloud Platform** aplikacji. To jest adres URL konta określonego zasobu chronionego w aplikacji platformy chmury SAP HANA. Adres URL jest oparta na następujący wzór: *https://\<applicationName\>\<accountName\>.\< host pozioma\>.ondemand.com/\<ścieżki\_do\_chronione\_zasobów\>*  (np.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >To jest adres URL w aplikacji SAP HANA Cloud Platform, która wymaga uwierzytelnienia użytkownika.
     > 

   2. Otwórz pobrany plik metadanych SAP HANA Cloud Platform, a następnie zlokalizuj **ns3:AssertionConsumerService** tagu.
   3. Skopiuj wartość **lokalizacji** atrybutu, a następnie wklej go do **SAP HANA Cloud Platform adres URL odpowiedzi służący** pola tekstowego.

7. Na **skonfigurować logowanie jednokrotne w SAP HANA Cloud Platform** , aby pobrać metadane, kliknij przycisk **pobierania metadanych**, a następnie zapisz plik na komputerze.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "skonfigurować logowanie jednokrotne")
8. Na SAP HANA Cloud Platform Panelu sterowania w **lokalnego dostawcy usług** sekcji, wykonaj następujące czynności:
   
    ![Zaufania zarządzania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "zaufania zarządzania")
   
  1. Kliknij pozycję **Edytuj**.
  2. Jako **typu konfiguracji**, wybierz pozycję **niestandardowy**.
  3. Jako **lokalna nazwa dostawcy**, pozostaw wartość domyślną.
  4. Aby wygenerować **klucza podpisywania** i **certyfikat podpisywania** parę kluczy, kliknij przycisk **generowanie pary klucz**.
  5. Jako **główna propagacji**, wybierz pozycję **wyłączone**.
  6. Jako **siły uwierzytelniania**, wybierz pozycję **wyłączone**.
  7. Kliknij pozycję **Zapisz**.

9. Kliknij przycisk **zaufany dostawca tożsamości** , a następnie kliknij pozycję **dodać zaufanego dostawcę tożsamości**.
   
    ![Zaufania zarządzania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "zaufania zarządzania")
   
    >[!NOTE]
    >Do zarządzania listą zaufanych dostawców tożsamości, musisz wybrany typ konfiguracji niestandardowej w sekcji lokalnego dostawcy usług. Typ konfiguracji domyślnej masz nieedytowalnego i niejawne zaufania z usługą identyfikator SAP. Dla żadnego nie masz żadnych ustawień zaufania.
    > 
    > 

10. Kliknij przycisk **ogólne** , a następnie kliknij pozycję **Przeglądaj** można przekazać pliku pobranego metadanych.
    
    ![Zaufania zarządzania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "zaufania zarządzania")
    
    >[!NOTE]
    >Po przekazaniu pliku metadanych wartości **URL rejestracji jednokrotnej**, **pojedynczego adresu URL wylogowania** i **certyfikat podpisywania** są wypełniane automatycznie.
    > 
    > 

11. Kliknij kartę **Atrybuty**.
12. Na **atrybuty** karcie, wykonaj następujące kroki:
    
    ![Atrybuty](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "atrybutów") 
  * Kliknij przycisk **atrybutu Add Assertion-Based**, a następnie dodaj następujące atrybuty oparte na potwierdzenia:
       
    | Atrybut potwierdzenia | Atrybut podmiotu |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/givenName |Imię |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/surname |nazwisko |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/emailaddress |Adres e-mail 
   
     >[!NOTE]
     >Konfiguracja atrybutów, zależy od tego, jak aplikacje na HCP są tworzone, tj. atrybuty, które oczekiwane w odpowiedzi SAML i w których nazwa (atrybut podmiotu zabezpieczeń) będą uzyskiwać dostęp do tego atrybutu w kodzie.
     > 
     >  

    1.  **Domyślny atrybut** na zrzucie ekranu jest tylko do celów ilustracyjnych. Nie jest wymagane dokonanie scenariuszu działać.   
    2.  Nazwy i wartości dla **atrybut podmiotu zabezpieczeń** na zrzucie ekranu pokazano zależą od sposobu zaprojektowano w aplikacji. Istnieje możliwość, że aplikacja wymaga innego mapowania.
     
13. W klasycznym portalu Azure na **skonfigurować logowanie jednokrotne w SAP HANA Cloud Platform** dialogu strony, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij **Complete**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "skonfigurować logowanie jednokrotne")

###<a name="assertion-based-groups"></a>Grupy oparte na potwierdzenie
Ten opcjonalny krok można skonfigurować grupy oparte na potwierdzenie dla usługi Azure Active Directory dostawcy tożsamości.

Na platformie programu SAP HANA chmury przy użyciu grup umożliwia dynamiczne przypisywanie co najmniej jednego użytkownika do co najmniej jedną rolę w aplikacjach platformy chmury SAP HANA określany przez wartości atrybutów w potwierdzenia SAML 2.0. 

Na przykład, jeśli potwierdzenie zawiera atrybut "*kontraktu = tymczasowego*", może być wszystkich użytkowników mają zostać dodane do grupy"*tymczasowego*". Grupa "*tymczasowego*" może zawierać co najmniej jedną rolę z co najmniej jednej aplikacji wdrożonych na koncie platformy chmury SAP HANA.
 
Grupy oparte na potwierdzenie należy użyć jednocześnie przypisać wielu użytkowników do co najmniej jedną rolę aplikacji na koncie platformy chmury SAP HANA. Jeśli chcesz przypisać tylko jednego lub mała liczba użytkowników do określonych ról, zalecane jest przypisywania do nich bezpośrednio w programie "**autoryzacje**" kartę SAP HANA Cloud Platform Panelu sterowania.

## <a name="assign-a-role-to-a-user"></a>Przypisywanie użytkownikowi roli
Aby włączyć użytkowników usługi Azure AD zalogować się do programu SAP HANA Cloud Platform, należy przypisać do nich ról na platformie programu SAP HANA chmury.

**Aby przypisać rolę do użytkownika, wykonaj następujące czynności:**

1. Zaloguj się do Twojego **SAP HANA Cloud Platform** Panelu sterowania.
2. Wykonaj następujące czynności:
   
   ![Autoryzacje](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "zezwolenia")
   
  1. Kliknij przycisk **autoryzacji**.
  2. Kliknij przycisk **użytkowników** kartę.
  3. W **użytkownika** tekstowym, wpisz adres e-mail użytkownika.
  4. Kliknij przycisk **przypisać** można przypisać do roli użytkownika.
  5. Kliknij pozycję **Zapisz**.

## <a name="assign-users"></a>Przypisywanie użytkowników
Aby przetestować konfigurację, musisz przyznać użytkowników usługi Azure AD, czy chcesz zezwolić, używając przypisywania do nich dostęp aplikacji do niego.

**Do przypisywania użytkowników do programu SAP HANA Cloud Platform, wykonaj następujące czynności:**

1. W klasycznym portalu Azure Utwórz konto testu.
2. Na **SAP HANA Cloud Platform** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.
   
   ![Przypisywanie użytkowników](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "przypisywanie użytkowników")
3. Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** o potwierdzenie przypisania.
   
   ![Tak](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "tak")

Jeśli chcesz przetestować ustawienia logowania jednokrotnego, otwórz Panel dostępu. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).

