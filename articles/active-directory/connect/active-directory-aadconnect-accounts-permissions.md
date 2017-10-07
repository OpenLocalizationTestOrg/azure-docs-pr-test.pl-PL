---
title: 'Azure AD Connect: Konta i uprawnienia | Dokumentacja firmy Microsoft'
description: "W tym temacie opisano hello konta używane i utworzyć i wymagane uprawnienia."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.reviewer: cychua
ms.assetid: b93e595b-354a-479d-85ec-a95553dd9cc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 70a7013e0353d74714ec8a3ff54b3e811789a0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-accounts-and-permissions"></a>Azure AD Connect: Konta i uprawnienia
Kreator instalacji Hello Azure AD Connect oferuje dwa różne ścieżki:

* W ustawieniach Express Kreator hello wymaga wyższego poziomu uprawnień.  Jest tak, aby go skonfigurować konfigurację łatwe, bez konieczności toocreate użytkowników lub skonfigurować uprawnienia.
* W niestandardowych ustawień kreatora hello oferuje więcej opcji i opcje. Istnieją jednak niektórych sytuacjach, w których należy tooensure możesz mieć hello odpowiednie uprawnienia.

## <a name="related-documentation"></a>Dokumentacja pokrewna
Jeśli nie odczytał dokumentacji hello na [integrowanie tożsamości lokalnych z usługą Azure Active Directory](../active-directory-aadconnect.md), hello Poniższa tabela zawiera linki toorelated tematów.

|Temat |Link|  
| --- | --- |
|Pobieranie programu Azure AD Connect | [Pobieranie programu Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Instalowanie przy użyciu ustawień ekspresowych | [Ekspresowa instalacja programu Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Instalowanie przy użyciu ustawień dostosowanych | [Niestandardowa instalacja programu Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Uaktualnianie przy użyciu narzędzia DirSync | [Uaktualnianie z narzędzia Azure AD Sync (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Po instalacji | [Zweryfikuj instalację hello i przypisywanie licencji](active-directory-aadconnect-whats-next.md)|

## <a name="express-settings-installation"></a>Ustawienia instalacji ekspresowej
W ustawieniach Express hello instalacji kreator poprosi o poświadczenia administratora przedsiębiorstwa usługi AD DS.  Jest to tak lokalnej usługi Active Directory można skonfigurować za pomocą wymaganych uprawnień do usługi Azure AD Connect. Jeśli uaktualniasz z narzędzia DirSync, hello AD DS, Administratorzy przedsiębiorstwa poświadczenia są tooreset używane hello hasło dla konta hello używane przez narzędzie DirSync. Należy również poświadczenia administratora globalnego usługi Azure AD.

| Strona kreatora | Poświadczenia zbierane | Wymagane uprawnienia | Używany do |
| --- | --- | --- | --- |
| Nie dotyczy |Kreator instalacji hello uruchomionych użytkownika |Administrator lokalny serwer hello |<li>Tworzy hello konta lokalnego, który jest używany jako hello [konta usługi aparatu synchronizacji](#azure-ad-connect-sync-service-account). |
| Połącz tooAzure AD |Poświadczenia katalogu usługi Azure AD |Rola administratora globalnego w usłudze Azure AD |<li>Włączanie synchronizacji w katalogu usługi Azure AD hello.</li>  <li>Tworzenie hello [konto usługi Azure AD](#azure-ad-service-account) używanego do operacji w toku synchronizacji w usłudze Azure AD.</li> |
| Połącz tooAD DS |Lokalnych poświadczeń usługi Active Directory |Członek grupy Administratorzy przedsiębiorstwa (EA) hello w usłudze Active Directory |<li>Tworzy [konta](#active-directory-account) w usłudze Active Directory i przyznaje uprawnienia tooit. Utworzone konto jest używane tooread i Zapisz informacje katalogu podczas synchronizacji.</li> |

### <a name="enterprise-admin-credentials"></a>Poświadczenia administratora przedsiębiorstwa
Te poświadczenia są używane tylko podczas instalacji hello i nie są używane po ukończeniu instalacji hello. Upewnij się, że hello uprawnień usługi Active Directory można ustawić we wszystkich domenach Hello administratora przedsiębiorstwa, hello administratora domeny.

### <a name="global-admin-credentials"></a>Poświadczenia administratora globalnego
Te poświadczenia są używane tylko podczas instalacji hello i nie są używane po ukończeniu instalacji hello. Jest używana toocreate hello [konto usługi Azure AD](#azure-ad-service-account) używane do synchronizowania zmian tooAzure AD. Witaj konta umożliwia także synchronizacji jako funkcję w usłudze Azure AD.

### <a name="permissions-for-hello-created-ad-ds-account-for-express-settings"></a>Uprawnienia dla hello utworzone konto usług AD DS dla ustawień ekspresowych
Witaj [konta](#active-directory-account) utworzone do odczytywania i zapisywania tooAD DS ma następujących uprawnień podczas tworzenia ustawienia ekspresowe hello:

| Uprawnienie | Używany do |
| --- | --- |
| <li>Replikować zmiany katalogu</li><li>Replikowanie katalogu zmienia wszystkie |Synchronizacja haseł |
| Odczyt/zapis wszystkich właściwości użytkownika |Hybrydowe Import i Exchange |
| Odczyt/zapis wszystkich właściwości iNetOrgPerson |Hybrydowe Import i Exchange |
| Grupa wszystkich właściwości odczytu/zapisu |Hybrydowe Import i Exchange |
| Skontaktuj się z wszystkich właściwości odczytu/zapisu |Hybrydowe Import i Exchange |
| Resetowanie hasła |Przygotowanie do włączania funkcji zapisywania zwrotnego haseł |

## <a name="custom-settings-installation"></a>Niestandardowe ustawienia instalacji
Azure AD Connect wersji 1.1.524.0 i później ma hello opcja toolet hello Azure AD Connect kreatora Utwórz hello konto używane tooconnect tooActive katalogu.  Wcześniejszych wersji wymaga utworzenia konta hello przed rozpoczęciem powitalne instalacji. należy przyznawać temu kontu uprawnienia Hello znajdują się w [Tworzenie konta usług AD DS hello](#create-the-ad-ds-account). 

| Strona kreatora | Poświadczenia zbierane | Wymagane uprawnienia | Używany do |
| --- | --- | --- | --- |
| Nie dotyczy |Kreator instalacji hello uruchomionych użytkownika |<li>Administrator lokalny serwer hello</li><li>Jeśli przy użyciu pełnego serwera SQL, hello użytkownik musi być administratora systemu (SA) w programie SQL</li> |Domyślnie tworzy hello konta lokalnego, który jest używany jako hello [konta usługi aparatu synchronizacji](#azure-ad-connect-sync-service-account). Konto Hello jest tworzony tylko, gdy Witaj, Administratorze nie określa określonego konta. |
| Zainstaluj usługi synchronizacji i opcji konta usługi |Usługi AD lub poświadczenia konta użytkownika lokalnego |Użytkownik, uprawnienia są udzielane przez Kreatora instalacji hello |Jeśli Witaj, Administratorze Określa konto, to konto jest używane jako konto usługi hello hello synchronizacji usługi. |
| Połącz tooAzure AD |Poświadczenia katalogu usługi Azure AD |Rola administratora globalnego w usłudze Azure AD |<li>Włączanie synchronizacji w katalogu usługi Azure AD hello.</li>  <li>Tworzenie hello [konto usługi Azure AD](#azure-ad-service-account) używanego do operacji w toku synchronizacji w usłudze Azure AD.</li> |
| Podłączanie katalogów |Lokalnych poświadczeń usługi Active Directory dla każdego lasu, który jest połączony tooAzure AD |uprawnienia Hello zależą od funkcji, które można włączyć i znajdują się w [Tworzenie konta hello usług AD DS](#create-the-ad-ds-account) |To konto jest używane tooread i Zapisz informacje katalogu podczas synchronizacji. |
| Serwery usług AD FS |Dla każdego serwera na liście hello hello Kreator zbiera poświadczeń podczas hello poświadczenia logowania użytkownika hello kreatora hello są niewystarczające tooconnect |Administrator domeny |Instalowanie i konfigurowanie roli serwera hello AD FS. |
| Serwery proxy aplikacji sieci Web |Dla każdego serwera na liście hello hello Kreator zbiera poświadczeń podczas hello poświadczenia logowania użytkownika hello kreatora hello są niewystarczające tooconnect |Administratora lokalnego na komputerze docelowym hello |Instalowanie i konfigurowanie roli serwera proxy. |
| Poświadczenia zaufania serwera proxy |Poświadczenia zaufania usługi federacyjnej (hello poświadczenia hello proxy używa tooenroll certyfikatu relacji zaufania z hello FS |Konta domeny, które ma uprawnienia administratora lokalnego serwera hello AD FS |Wstępnej rejestracji certyfikatu zaufania FS WAP. |
| Strona usług AD FS konta usługi, "Użyć opcji konta użytkownika domeny" |Poświadczenia konta użytkownika AD |Użytkownik domeny |Hello AD konto użytkownika, którego poświadczenia są udostępniane jest używane jako konto logowania hello usługi hello usług AD FS. |

### <a name="create-hello-ad-ds-account"></a>Tworzenie konta hello usług AD DS
Witaj konta użytkownika na powitania **Podłączanie katalogów** strony musi być obecny w poprzednich tooinstallation usługi Active Directory.  Musi mieć również hello wymagane uprawnienia. Kreator instalacji Hello nie Sprawdź, czy uprawnienia hello i problemy mogą znajdować się tylko podczas synchronizacji.

Uprawnienia wymagane jest zależny od funkcji opcjonalnych hello zostanie włączona. Jeśli masz wiele domen dla wszystkich domen w lesie hello muszą być przyznane uprawnienia hello. Jeśli nie włączysz dowolnej z tych funkcji, hello domyślne **użytkownika domeny** uprawnienia są wystarczające.

| Funkcja | Uprawnienia |
| --- | --- |
| Funkcja msDS-ConsistencyGuid |Uprawnienia do zapisu atrybutu msDS-ConsistencyGuid toohello udokumentowane w [zagadnienia dotyczące projektowania — przy użyciu msDS-ConsistencyGuid jako sourceAnchor](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). | 
| Synchronizacja haseł |<li>Replikować zmiany katalogu</li>  <li>Replikowanie katalogu zmienia wszystkie |
| Wdrożenia hybrydowego programu Exchange |Zapis atrybutów toohello uprawnienia udokumentowane w [zapisywania zwrotnego hybrydowego programu Exchange](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) dla użytkowników, grup i kontakty. |
| Folder publiczny poczty programu Exchange |Atrybuty toohello uprawnienia odczytu udokumentowane w [folderu publicznego poczty programu Exchange](active-directory-aadconnectsync-attributes-synchronized.md#exchange-mail-public-folder) dla folderów publicznych. | 
| Zapisywanie zwrotne haseł |Zapis atrybutów toohello uprawnienia udokumentowane w [wprowadzenie do zarządzania hasłami](../active-directory-passwords-writeback.md) dla użytkowników. |
| Zapisywanie zwrotne urządzeń |Uprawnienia przyznane przy użyciu skryptu programu PowerShell, zgodnie z opisem w [zapisu zwrotnego urządzeń](active-directory-aadconnect-feature-device-writeback.md). |
| Zapisywanie zwrotne grup |Przeczytaj, tworzenia, aktualizowania lub usuwania grupy obiektów dla synchronizacji **grup usługi Office 365**.  Aby uzyskać więcej informacji, zobacz [zapisu zwrotnego grup](active-directory-aadconnect-feature-preview.md#group-writeback).|

## <a name="upgrade"></a>Uaktualnienie
Podczas uaktualniania z jednej wersji programu Azure AD Connect tooa nowej wersji należy hello następujących uprawnień:

| Główna | Wymagane uprawnienia | Używany do |
| --- | --- | --- |
| Kreator instalacji hello uruchomionych użytkownika |Administrator lokalny serwer hello |Aktualizowanie plików binarnych. |
| Kreator instalacji hello uruchomionych użytkownika |Element członkowski ADSyncAdmins |Wprowadzanie zmian reguły tooSync i innych konfiguracji. |
| Kreator instalacji hello uruchomionych użytkownika |Jeśli używasz pełnego serwera SQL: DBO (lub podobny) bazy danych aparatu synchronizacji hello |Wprowadź zmiany poziomu bazy danych, takich jak aktualizowanie tabel z nowymi kolumnami. |

## <a name="more-about-hello-created-accounts"></a>Więcej informacji na temat tworzenia kont hello
### <a name="active-directory-account"></a>Konto usługi Active Directory
Jeśli używasz ustawień ekspresowych, konto jest tworzone w usłudze Active Directory, które jest używane do synchronizacji. Hello utworzone konto znajduje się w domenie głównej lasu hello w kontenerze Użytkownicy hello i ma jego nazwa jest prefiksem **MSOL_**. Utworzono konto Hello z długo złożone hasło, które nie wygaśnie. Jeśli masz zasady haseł w domenie, upewnij się, że długie i złożone hasła będzie dozwolone dla tego konta.

![Konto usługi AD](./media/active-directory-aadconnect-accounts-permissions/adsyncserviceaccount.png)

Jeśli używasz ustawienia niestandardowe, następnie jest odpowiedzialny za tworzenie konta hello przed rozpoczęciem powitalne instalacji.

### <a name="azure-ad-connect-sync-service-account"></a>Konto usługi synchronizacji programu Azure AD Connect
Usługa synchronizacji Hello może działać w ramach różnych kont. Mogą działać w ramach **wirtualnego konta usługi** (VSA), **konta usługi zarządzanego przez grupę** (gMSA/autonomiczne) lub konta zwykłych użytkowników. Witaj obsługiwane opcje zostały zmienione z hello wersji kwietnia 2017 Connect po wykonaniu pierwszą instalację. W przypadku uaktualniania z wcześniejszych wersji programu Azure AD Connect nie są dostępne te opcje dodatkowe.

| Typ konta | Opcja instalacji | Opis |
| --- | --- | --- |
| [Konta usług wirtualnych](#virtual-service-account) | 2017 Express i niestandardowych, kwietnia i nowsze | Jest to opcja hello używane dla wszystkich instalacji ekspresowej, z wyjątkiem instalacji na kontrolerze domeny. Niestandardowe jest opcja domyślna hello chyba że używana jest inną opcją. |
| [Konto usługi zarządzane przez grupę](#group-managed-service-account) | Niestandardowe, 2017 kwietnia i nowsze | Jeśli używasz zdalnego serwera SQL, a następnie zalecamy toouse grupy zarządzane konto usługi. |
| [Konto użytkownika](#user-account) | 2017 Express i niestandardowych, kwietnia i nowsze | Konto użytkownika z prefiksem AAD_ jest tworzony tylko podczas instalacji zainstalowany w systemie Windows Server 2008 i zainstalować na kontrolerze domeny. |
| [Konto użytkownika](#user-account) | 2017 Express i niestandardowych, marca i starszych wersji | Konto lokalne, i jest poprzedzony prefiksem AAD_ został utworzony podczas instalacji. Podczas korzystania z niestandardowej instalacji, można określić inne konto. |

Jeśli używasz Połącz z kompilacją z marca 2017 lub starszy, nie należy resetować hasła hello na koncie usługi hello od systemu Windows, a następnie niszczy klucze szyfrowania hello ze względów bezpieczeństwa. Inne konto hello tooany konta nie można zmienić bez ponownego instalowania Azure AD Connect. Jeśli uaktualnienia tooa kompilacji z 2017 kwietnia lub później, to jest obsługiwane toochange hello hasło konta usługi hello, ale nie można zmienić konto hello używane.

> [!Important]
> Konto usługi hello można ustawić tylko w pierwszej instalacji. Nie jest obsługiwane konta usługi hello toochange po ukończeniu instalacji hello.

Jest to tabela wartości domyślnych hello, zaleca się, i opcje są obsługiwane dla hello synchronizacji konta usługi.

Legenda:

- **Bold** wskazuje hello opcji domyślnej i w większości przypadków hello zalecana opcja.
- *Kursywa* wskazuje hello opcja zalecana, gdy nie jest to opcja domyślna hello.
- 2008 — opcja domyślna w systemie Windows Server 2008
- Inne niż — bold — opcja obsługiwana
- Konto lokalne - użytkownika lokalnego konta na powitania serwera
- Konto domeny — konta użytkownika domeny
- Autonomiczne - [autonomiczny konto usługi zarządzane](https://technet.microsoft.com/library/dd548356.aspx)
- gMSA - [grupy konto usługi zarządzane](https://technet.microsoft.com/library/hh831782.aspx)

| | LocalDB</br>Express | LocalDB/LocalSQL</br>Niestandardowy | Zdalny program SQL</br>Niestandardowy |
| --- | --- | --- | --- |
| **komputer autonomicznego/Grupa robocza** | Nieobsługiwane | **VSA**</br>Konto lokalne (2008)</br>Konto lokalne |  Nieobsługiwane |
| **komputerze przyłączonym do domeny** | **VSA**</br>Konto lokalne (2008) | **VSA**</br>Konto lokalne (2008)</br>Konto lokalne</br>Konto domeny</br>Autonomiczne, gMSA | **gMSA**</br>Konto domeny |
| **Kontroler domeny** | **Konto domeny** | *gMSA*</br>**Konto domeny**</br>Autonomiczne| *gMSA*</br>**Konto domeny**|

#### <a name="virtual-service-account"></a>Konta usług wirtualnych
Konto usługi wirtualnego jest specjalnym rodzajem konto nie ma hasła, który jest zarządzany przez system Windows.

![VSA](./media/active-directory-aadconnect-accounts-permissions/aadsyncvsa.png)

Witaj VSA jest zamierzone toobe używana w scenariuszach, w którym hello aparatu synchronizacji i SQL znajdują się na powitania tym samym serwerze. Jeśli używasz zdalnego programu SQL, a następnie zalecamy toouse [konta usługi zarządzanego przez grupę](#managed-service-account) zamiast tego.

Ta funkcja wymaga systemu Windows Server 2008 R2 lub nowszym. Jeśli Azure AD Connect można zainstalować w systemie Windows Server 2008, a następnie instalacji hello powraca toousing [konta użytkownika](#user-account) zamiast tego.

#### <a name="group-managed-service-account"></a>Konto usługi zarządzane przez grupę
Jeśli używasz zdalnego serwera SQL, a następnie zalecamy toousing **konto usługi zarządzane przez grupę**. Aby uzyskać więcej informacji na temat Zobacz usługi Active Directory dla kont usług zarządzanych grupy tooprepare [omówienie kont usług zarządzanych grupy](https://technet.microsoft.com/library/hh831782.aspx).

tę opcję na powitania toouse [zainstalowanie wymaganych składników](active-directory-aadconnect-get-started-custom.md#install-required-components) wybierz pozycję **Użyj istniejącego konta usługi**i wybierz **konto usługi zarządzane przez**.  
![VSA](./media/active-directory-aadconnect-accounts-permissions/serviceaccount.png)  
Możliwe jest również obsługiwany toouse [autonomiczne zarządzane konto usługi](https://technet.microsoft.com/library/dd548356.aspx). Jednak te można używać tylko na komputerze lokalnym hello i nie istnieje żadne toouse korzyści ich za pośrednictwem hello domyślnego konta usługi wirtualnego.

Ta funkcja wymaga systemu Windows Server 2012 lub nowszym. Jeśli toouse starszy system operacyjny a za pomocą zdalnego programu SQL, a następnie należy użyć [konta użytkownika](#user-account).

#### <a name="user-account"></a>Konto użytkownika
Konto Usługa lokalna jest tworzony przez Kreatora instalacji hello (chyba że toouse konta hello jest podana w ustawieniach niestandardowych). Konto Hello jest prefiksem **AAD_** i używane do toorun usługi synchronizacji rzeczywiste hello jako. Jeśli program Azure AD Connect na kontrolerze domeny, konto hello jest tworzony w domenie hello. Witaj **AAD_** konto usługi musi znajdować się w domenie hello, jeśli:
   - w przypadku używania serwera zdalnego programem SQL server
   - Użyj serwera proxy, który wymaga uwierzytelniania

![Konto usługi synchronizacji](./media/active-directory-aadconnect-accounts-permissions/syncserviceaccount.png)

Utworzono konto Hello z długo złożone hasło, które nie wygaśnie.

To konto jest używane toostore hello hasła dla hello inne konta w bezpieczny sposób. Te hasła konta są przechowywany jako zaszyfrowany hello bazy danych. Hello klucze prywatne dla kluczy szyfrowania hello są chronione przy użyciu szyfrowania klucza tajnego usługi kryptograficzne hello przy użyciu interfejsu API ochrony danych systemu Windows (DPAPI).

Jeśli używasz pełnego serwera SQL, hello konto usługi jest hello DBO bazy danych aparatu synchronizacji hello hello utworzony. Usługa Hello nie będzie działać zgodnie z założeniami z innymi uprawnieniami. Tworzona jest również identyfikator logowania SQL.

Konto Hello ma również przyznane uprawnienia toofiles, kluczy rejestru i innych toohello powiązane obiekty aparatu synchronizacji.

### <a name="azure-ad-service-account"></a>Konto usługi Azure AD
Konto w usłudze Azure AD jest tworzone do użycia usługi synchronizacji hello. To konto może zostać zidentyfikowane na podstawie nazwy wyświetlanej.

![Konto usługi AD](./media/active-directory-aadconnect-accounts-permissions/aadsyncserviceaccount.png)

używana jest nazwa konta powitania serwera hello Hello na mogą zostać zidentyfikowane hello drugiej części hello nazwy użytkownika. Na rysunku hello hello nazwa serwera jest FABRIKAMCON. Jeśli masz przemieszczania serwerów, każdy serwer ma własnego konta.

Konto usługi Hello jest tworzony z długo złożone hasło, które nie wygaśnie. Ma przyznane uprawnienia roli specjalne **konta synchronizacji katalogu** która ma tylko uprawnienia tooperform katalogu zadania synchronizacji. Nie można udzielić tej roli wbudowanych specjalne poza hello Kreator Azure AD Connect. Witaj portalu Azure zawiera tego konta z rolą hello **użytkownika**.

Istnieje limit 20 kont usługi synchronizacji w usłudze Azure AD. Lista hello tooget istniejącego konta usługi Azure AD usługi w usługi Azure AD, uruchom następujące polecenia cmdlet programu PowerShell usługi Azure AD hello:`Get-AzureADDirectoryRole | where {$_.DisplayName -eq "Directory Synchronization Accounts"} | Get-AzureADDirectoryRoleMember`

tooremove nieużywanych konta usługi Azure AD, uruchom następujące polecenia cmdlet programu PowerShell usługi Azure AD hello:`Remove-AzureADUser -ObjectId <ObjectId-of-the-account-you-wish-to-remove>`

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](../active-directory-aadconnect.md).
