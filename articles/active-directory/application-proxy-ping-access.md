---
title: "uwierzytelnianie oparte na aaaHeader z PingAccess dla serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Publikowania aplikacji za pomocą PingAccess i serwera Proxy aplikacji toosupport nagłówek uwierzytelniania."
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
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a>Nagłówek uwierzytelniania dla logowania jednokrotnego z serwera Proxy aplikacji i PingAccess

Azure Active Directory serwera Proxy aplikacji i PingAccess ma współpracę ze sobą tooprovide usługi Azure Active Directory klientom dostępu tooeven więcej aplikacji. PingAccess rozszerza hello [istniejący serwer Proxy aplikacji ofert](active-directory-application-proxy-get-started.md) tooinclude tooapplications dostępu rejestracji jednokrotnej, który nagłówków jest używany do uwierzytelniania.

## <a name="what-is-pingaccess-for-azure-ad"></a>Co to jest PingAccess dla usługi Azure AD?

PingAccess dla usługi Azure Active Directory jest oferowany PingAccess umożliwiającą toogive użytkowników dostęp i pojedynczego logowania jednokrotnego tooapplications który nagłówków jest używany do uwierzytelniania. Serwer Proxy aplikacji traktuje te aplikacje, takie jak każdy inny przy użyciu usługi Azure AD tooauthenticate dostępu, a następnie przekazywanie ruchu za pośrednictwem usługi łącznika hello. PingAccess znajduje się na początku aplikacji hello i tłumaczy hello token dostępu z usługi Azure AD na nagłówka, dzięki czemu aplikacja hello odbiera hello uwierzytelniania w formacie hello, który można odczytać.

Użytkownicy nie będą Zwróć uwagę, inne po zalogowaniu toouse aplikacji firmowych. Wciąż pracować z dowolnego miejsca na dowolnym urządzeniu. 

Ponieważ łączniki serwera Proxy aplikacji hello skierować ruch zdalnego tooall aplikacji niezależnie od ich typ uwierzytelniania, będziesz nadal saldo tooload automatycznie, jak również.

## <a name="how-do-i-get-access"></a>Jak uzyskać dostęp?

Ponieważ ten scenariusz jest dostępna za pośrednictwem usługi Azure Active Directory i PingAccess, potrzebnych licencji dla obu usług. Jednak subskrypcje usługi Azure Active Directory Premium obejmują podstawowe licencji PingAccess, która obejmuje zapasowe too20 aplikacji. Jeśli potrzebujesz toopublish więcej niż 20 aplikacji nagłówka, można nabyć od PingAccess dodatkowych licencji. 

Aby uzyskać więcej informacji, zobacz [Wersje usługi Azure Active Directory](active-directory-editions.md).

## <a name="publish-your-application-in-azure"></a>Publikowanie aplikacji na platformie Azure

Ten artykuł jest przeznaczony dla osób, które są publikowania aplikacji za pomocą tego scenariusza powitania po raz pierwszy. Go przedstawiono sposób tooget uruchamiania z aplikacji i PingAccess, oprócz toohello kroki publikowania. Jeśli skonfigurowano już obie usługi, ale odświeżacz na powitania publikowania kroki, możesz pominąć hello instalacja łącznika i przenieść na zbyt[dodać tooAzure Twojej aplikacji usługi Active Directory z serwera Proxy aplikacji](#add-your-app-to-Azure-AD-with-Application-Proxy).

>[!NOTE]
>Ponieważ ten scenariusz jest powiązanie między usługą Azure AD i PingAccess, niektóre instrukcje hello istnieją na powitania Ping tożsamości witryny.

### <a name="install-an-application-proxy-connector"></a>Instalowanie łącznika serwera Proxy aplikacji

Jeśli już ma włączony serwer Proxy aplikacji, a ma zainstalowany łącznik, możesz pominąć tę sekcję i przenieść na zbyt[dodać tooAzure Twojej aplikacji usługi Active Directory z serwera Proxy aplikacji](#add-your-app-to-azure-ad-with-application-proxy).

Łącznik serwera Proxy aplikacji Hello jest Windows Server usługi, który kieruje ruch hello z tooyour Twojego pracowników zdalnych opublikowane aplikacje. Aby uzyskać szczegółowe instrukcje dotyczące instalacji, zobacz [Włączanie serwera Proxy aplikacji w portalu Azure hello](active-directory-application-proxy-enable.md).

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator globalny.
2. Wybierz **usługi Azure Active Directory** > **serwera proxy aplikacji**.
3. Wybierz **Pobierz łącznik** pobieranie łącznika serwera Proxy aplikacji hello toostart. Wykonaj instrukcje dotyczące instalacji hello.

   ![Włącz serwer Proxy aplikacji i Pobierz łącznik hello](./media/application-proxy-ping-access/install-connector.png)

4. Pobieranie łącznika hello automatycznie należy włączyć serwer Proxy aplikacji dla katalogu, ale jeśli nie możesz wybrać **Włączanie serwera Proxy aplikacji**.


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a>Dodaj użytkownika tooAzure aplikacji usługi Active Directory z serwera Proxy aplikacji

Istnieją dwie akcje muszą tootake w hello portalu Azure. Najpierw należy toopublish aplikacji przy użyciu serwera Proxy aplikacji. Następnie należy toocollect niektóre informacje na temat aplikacji hello, używanego podczas hello PingAccess czynności.

Wykonaj te kroki toopublish aplikacji. Bardziej szczegółowe wskazówki kroki 1 – 8, zobacz [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](application-proxy-publish-azure-portal.md).

1. Jeśli nie w ostatniej sekcji hello, zaloguj się w toohello [portalu Azure](https://portal.azure.com) jako administrator globalny.
2. Wybierz **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw**.
3. Wybierz **Dodaj** u góry bloku hello hello.
4. Wybierz **lokalnej aplikacji**.
5. Wypełnij pola hello wymagane informacje o nowej aplikacji. Użyj hello następujące wskazówki dotyczące ustawień hello:
   - **Wewnętrzny adres URL**: zwykle Podaj adres URL hello przejście toohello aplikacji zaloguj się na stronie podczas pracy w sieci firmowej hello. W tym scenariuszu hello łącznika musi tootreat hello PingAccess proxy jako pierwsza strona hello aplikacji hello. Użyj tego formatu: `https://<host name of your PA server>:<port>`. Hello port jest 3000 domyślnie, ale można go skonfigurować w PingAccess.
   - **Metoda wstępnego uwierzytelnienia**: Azure Active Directory
   - **Tłumaczenie adresów URL w nagłówkach**: nie

   >[!NOTE]
   >Jeśli jest to swoją pierwszą aplikację, użyj port 3000 toostart i wróć tooupdate to ustawienie w przypadku zmiany konfiguracji PingAccess. Jeśli jest to drugi lub nowszym aplikacji, to należy toomatch hello skonfigurowaniu PingAccess odbiornika. Dowiedz się więcej o [odbiorników w PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).

6. Wybierz **Dodaj** u dołu hello hello bloku. Aplikacja zostanie dodany, a następnie otwiera hello szybki start menu.
7. Witaj szybki start menu wybierz **przypisać użytkownika do testowania**i Dodaj przynajmniej jednego użytkownika toohello aplikacji. Upewnij się, że to konto testu ma dostęp toohello lokalnej aplikacji.
8. Wybierz **przypisać** przypisanie użytkownika testu hello toosave.
9. W bloku zarządzania aplikacji hello, wybierz **logowanie jednokrotne**.
10. Wybierz **na podstawie nagłówka logowania jednokrotnego** z menu rozwijanego hello. Wybierz pozycję **Zapisz**.

   >[!TIP]
   >Jeśli jest to pierwsza przy użyciu opartych na nagłówkach logowanie jednokrotne, należy tooinstall PingAccess. toomake się, że subskrypcji platformy Azure jest automatycznie kojarzony z instalacją PingAccess, użyj łącza hello na tym toodownload strony rejestracji jednokrotnej PingAccess. Można teraz otworzyć hello pobierania witryny lub powracanie toothis strony. 

   ![Wybierz na podstawie nagłówka logowania jednokrotnego](./media/application-proxy-ping-access/sso-header.PNG)

11. Zamknij blok aplikacje przedsiębiorstwa hello lub przewiń wszystkich hello sposób toohello tooreturn po lewej stronie toohello usługi Azure Active Directory menu.
12. Wybierz **rejestracji aplikacji**.

   ![Wybierz rejestracji aplikacji](./media/application-proxy-ping-access/app-registrations.png)

13. Aplikacja hello wybierz dodaną, następnie **adresy URL odpowiedzi**.

   ![Wybierz adresy URL odpowiedzi](./media/application-proxy-ping-access/reply-urls.png)

14. Określ, czy toosee hello zewnętrznego adresu URL, zostanie przypisany tooyour aplikacja w kroku 5 się na liście adresów URL odpowiedzi hello. Jeśli nie, dodaj go.
15. W bloku ustawień aplikacji hello wybierz **wymagane uprawnienia**.

  ![Wybierz wymagane uprawnienia](./media/application-proxy-ping-access/required-permissions.png)

16. Wybierz pozycję **Dodaj**. Hello interfejsu API, można wybrać **Windows Azure Active Directory**, następnie **wybierz**. Uprawnienia hello, wybierz **odczytu i zapisu wszystkie aplikacje** i **Zaloguj się i odczytuj profil użytkownika**, następnie **wybierz** i **gotowe**.  

  ![Wybierz uprawnienia](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a>Zbieranie informacji o krokach PingAccess hello

1. W bloku ustawień aplikacji, wybierz **właściwości**. 

  ![Wybierz polecenie Właściwości](./media/application-proxy-ping-access/properties.png)

2. Zapisz hello **identyfikator aplikacji** wartość. Służy to dla Identyfikatora klienta powitania po skonfigurowaniu PingAccess.
3. W bloku ustawień aplikacji hello wybierz **klucze**.

  ![Wybierz klucze](./media/application-proxy-ping-access/Keys.png)

4. Utwórz klucz, wprowadzając opis klucza i wybierając z menu rozwijanego hello datę wygaśnięcia.
5. Wybierz pozycję **Zapisz**. Identyfikator GUID jest wyświetlana w hello **wartość** pola.

  Zapisz tę wartość teraz, ponieważ nie będzie możliwe toosee ją ponownie po zamknąć to okno.

  ![Utwórz nowy klucz](./media/application-proxy-ping-access/create-keys.png)

6. Zamknij bloku rejestracji aplikacji hello lub przewiń wszystkich hello sposób toohello tooreturn po lewej stronie toohello usługi Azure Active Directory menu.
7. Wybierz **właściwości**.
8. Zapisz hello **identyfikator katalogu** identyfikatora GUID.

### <a name="optional---update-graphapi-toosend-custom-fields"></a>Opcjonalne - pola niestandardowe toosend GraphAPI aktualizacji

Aby uzyskać listę tokeny zabezpieczające, które wysyła usługi Azure AD do uwierzytelniania, zobacz [odwołania do tokenu usługi Azure AD](./develop/active-directory-token-and-claims.md). Niestandardowe oświadczenie, które wysyła innych tokenów, należy użyć pola aplikacji hello tooset GraphAPI *acceptMappedClaims* za**True**. Azure AD Graph Explorer lub MS Graph toomake można użyć tej konfiguracji. 

W tym przykładzie użyto wykres Explorer:

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a>Pobierz PingAccess i konfigurowanie aplikacji

Teraz, gdy zakończyła się wszystkie kroki konfiguracji usługi Azure Active Directory hello, można przenieść na tooconfiguring PingAccess. 

Hello szczegółowe informacje na temat hello PingAccess częścią tego scenariusza kontynuowania hello dokumentacji tożsamości Ping [PingAccess konfigurowanie dla usługi Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).

Tych krokach objaśniono proces hello pierwsze konto PingAccess, jeśli nie masz już konto, instalowanie hello PingAccess serwera i tworzenie połączenia dostawcy usługi Azure AD OIDC z hello identyfikator katalogu, który został skopiowany z portalu Azure hello. Następnie należy użyć hello aplikacji identyfikator i klucz wartości toocreate sesji sieci Web na PingAccess. Po wykonaniu tej można Konfigurowanie mapowania tożsamości i tworzenia hostów wirtualnych, witryn i aplikacji.

### <a name="test-your-app"></a>Testowanie aplikacji

Po zakończeniu wszystkich tych kroków aplikacji powinna być uruchomiona. tootest, otwórz przeglądarkę i przejdź toohello zewnętrzny adres URL, utworzony po opublikowaniu aplikacji hello na platformie Azure. Zaloguj się przy użyciu konta testowego hello tego przypisanej toohello aplikacji.

## <a name="next-steps"></a>Następne kroki

- [Skonfiguruj PingAccess dla usługi Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [W jaki sposób serwera Proxy aplikacji usługi Azure AD zapewnia rejestrację jednokrotną](application-proxy-sso-overview.md)
- [Rozwiązywanie problemów z serwera Proxy aplikacji](active-directory-application-proxy-troubleshoot.md)
