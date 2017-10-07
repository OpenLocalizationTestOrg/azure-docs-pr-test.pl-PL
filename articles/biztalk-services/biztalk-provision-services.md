---
title: "aaaCreate usług BizTalk Azure w portalu Azure hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprovision lub Utwórz usług BizTalk Azure w hello portal Azure. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a>Tworzenie przy użyciu portalu Azure hello usługi BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> toosign w toohello portalu Azure, należy konto platformy Azure i subskrypcji platformy Azure. Jeśli nie masz konta, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Zobacz [Bezpłatna wersja próbna platformy Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).


## <a name="CreateService"></a>Tworzenie usługi BizTalk
W zależności od hello wybór wersji nie wszystkie ustawienia usługi BizTalk mogą być dostępne.

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Witaj dolnym okienku nawigacji, wybierz **nowy**:  
   ![Wybierz przycisk Nowy hello][NEWButton]
3. Wybierz kolejno opcje **USŁUGI APLIKACJI** > **USŁUGA BIZTALK** > **TWORZENIE NIESTANDARDOWE**:  
   ![Wybieranie kolejno opcji Usługa BizTalk i Tworzenie niestandardowe][NewBizTalkService]
4. Wprowadź ustawienia usługi BizTalk hello:
   
    <table border="1">
    <tr>
    <td><strong>Nazwa usługi BizTalk</strong></td>
    <td>Można wprowadzić dowolną nazwę, ale musi ona być dokładna. Oto niektóre przykłady:<br/><br/>
    <em>mojafirma</em>.biztalk.windows.net<br/>
    <em>mojafirmamojaaplikacja</em>.biztalk.windows.net<br/>
    <em>mojaaplikacja</em>.biztalk.windows.net<br/><br/>". biztalk.windows.net" jest nazwą automatycznie dodawanych toohello możesz wprowadzić. Spowoduje to utworzenie adresu URL, który jest używany tooaccess Twojego BizTalk usługi tak samo, jak <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>.
    </td>
    </tr>
    <tr>
    <td><strong>Wersja</strong></td>
    <td>Jeśli w fazie testowania programowanie hello, wybierz polecenie <strong>Developer</strong>. Na etapie produkcji hello, za pomocą hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">usługi BizTalk Services: wykres wersje</a> toodetermine Jeśli <strong>Premium</strong>, <strong>standardowe</strong>, lub <strong>Basic</strong>jest poprawny wybór powitania dla danego scenariusza biznesowego.
    </td>
    </tr>
    <tr>
    <td><strong>Region</strong></td>
    <td>Wybierz usługę BizTalk hello toohost regionu geograficznego.</td>
    </tr>
    <tr>
    <td><strong>Adres URL domeny</strong></td>
    <td><strong>Opcjonalnie</strong>. Domyślnie adres URL domeny hello jest <em>YourBizTalkServiceName</em>. biztalk.windows.net. Można również wprowadzić niestandardową nazwę domeny.  Na przykład jeśli domeną jest <em>contoso</em>, możesz wprowadzić: <br/><br/>
    <em>MojaFirma</em>.contoso.com<br/>
    <em>MojaFirmaMojaAplikacja</em>.contoso.com<br/>
    <em>MojaAplikacja</em>.contoso.com<br/>
    <em>NazwaUsługiBizTalk</em>.contoso.com<br/>
    </td>
    </tr>
    </table>
Wybierz strzałkę dalej hello.
5. Wprowadź hello magazynu i ustawienia bazy danych:  <table border="1">
    <tr>
    <td><strong>Konto monitorowania/archiwizowania magazynu</strong></td>
    <td>Wybierz istniejące konto magazynu lub utwórz nowe. <br/><br/>Jeśli utworzysz nowe konto magazynu, wprowadź hello <strong>nazwy konta magazynu</strong>.</td>
    </tr>
    <tr>
    <td><strong>Baza danych śledzenia</strong></td>
    <td>Jeśli używasz istniejącej bazy danych SQL Azure, nie można jej użyć w innej usłudze BizTalk. Należy hello nazwy logowania i hasła podanego podczas tworzenia tego serwera bazy danych SQL Azure.<br/><br/><strong>Porada</strong> Utwórz hello śledzenia bazę danych i konto magazynu monitorowania/archiwizacja w hello tego samego regionu hello usługi BizTalk.</td>
    </tr>
    </table>
Wybierz strzałkę dalej hello.
6. Wprowadź ustawienia bazy danych hello:  <table border="1">
    <tr>
    <td><strong>Nazwa</strong></td>
    <td>Dostępna, gdy <strong>utworzenia nowego wystąpienia bazy danych SQL</strong> wybrano hello poprzedniego ekranu.
    <br/><br/>
Wprowadź toobe Nazwa bazy danych SQL, używane przez usługi BizTalk.</td>
    </tr>
    <tr>
    <td><strong>Serwer</strong></td>
    <td>Dostępna, gdy <strong>utworzenia nowego wystąpienia bazy danych SQL</strong> wybrano hello poprzedniego ekranu.
    <br/><br/>
Wybierz istniejący serwer bazy danych SQL lub utwórz nowy.</td>
    </tr>
    <tr>
    <td><strong>Nazwa logowania do serwera</strong></td>
    <td>Wprowadź nazwę użytkownika logowania hello.</td>
    </tr>
    <tr>
    <td><strong>Hasło logowania do serwera</strong></td>
    <td>Wprowadź hasło logowania hello.</td>
    </tr>
    <tr>
    <td><strong>Region</strong></td>
    <td>Ustawienie dostępne, jeśli wybrano opcję <strong>Utwórz nowe wystąpienie bazy danych SQL</strong>. Wybierz toohost regionu geograficznego hello bazy danych SQL.</td>
    </tr>
    </table>

Wybierz hello znacznik wyboru toocomplete hello kreatora. pojawi się ikona postępu Hello:  
![Ikona postępu zostanie wyświetlona po ukończeniu][ProgressComplete]

Po zakończeniu hello Azure usługi BizTalk został utworzony i gotowa do aplikacji. Witaj domyślne ustawienia są wystarczające. Ustawienia domyślne hello toochange, wybierz opcję **usługi BIZTALK SERVICES** w lewym okienku nawigacji hello, a następnie wybierz usługi BizTalk. Dodatkowe ustawienia są wyświetlane na powitania [karty Pulpit nawigacyjny, Monitor i skali](biztalk-dashboard-monitor-scale-tabs.md) u góry hello.

W zależności od stanu hello hello usługi BizTalk ma niektórych operacji, które nie może zostać zakończona. Lista te operacje, przejść za[wykresu stanu usługi BizTalk](biztalk-service-state-chart.md).

## <a name="post-provisioning-steps"></a>Kroki po zainicjowaniu obsługi
* [Zainstaluj certyfikat hello na komputerze lokalnym](#InstallCert)
* [Dodanie certyfikatu gotowego do produkcji](#AddCert)
* [Pobierz hello kontroli dostępu w przestrzeni nazw](#ACS)

#### <a name="InstallCert"></a>Zainstaluj certyfikat hello na komputerze lokalnym
W ramach inicjowania obsługi usługi BizTalk zostaje utworzony certyfikat z podpisem własnym, skojarzony z subskrypcją usługi BizTalk. Należy pobrać tego certyfikatu i zainstalować na komputerach, z których możesz wdrażania aplikacji usługi BizTalk lub wysyłać wiadomości tooa punktu końcowego usługi BizTalk.

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Wybierz **usługi BIZTALK SERVICES** w lewym okienku nawigacji hello, a następnie wybierz subskrypcję usługi BizTalk.
3. Wybierz hello **pulpitu nawigacyjnego** kartę.
4. Wybierz opcję **Pobierz certyfikat SSL**:  
   ![Modyfikowanie certyfikatu SSL][QuickGlance]
5. Kliknij dwukrotnie certyfikat hello i uruchom za pośrednictwem hello kreatora tooinstall hello certyfikatu. Upewnij się, że konieczne jest zainstalowanie certyfikatu hello w obszarze hello **zaufane główne urzędy certyfikacji** przechowywania.

#### <a name="AddCert"></a>Dodanie certyfikatu gotowego do produkcji
Witaj certyfikatu z podpisem własnym, który jest tworzony automatycznie podczas tworzenia usługi BizTalk Services jest przeznaczony do użytku w środowiskach programistycznych tylko. Na potrzeby scenariuszy produkcyjnych zastąp go certyfikatem gotowym do produkcji.

1. Na powitania **pulpitu nawigacyjnego** wybierz opcję **certyfikat SSL aktualizacji**.
2. Przeglądaj tooyour prywatny certyfikatu SSL (*CertificateName*pfx) zawierającą nazwę usługi BizTalk, wprowadź hasło hello, a następnie kliknij znacznik wyboru hello.

#### <a name="ACS"></a>Pobierz hello kontroli dostępu w przestrzeni nazw
1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Wybierz **usługi BIZTALK SERVICES** w lewym okienku nawigacji hello, a następnie wybierz usługi BizTalk.
3. Na pasku zadań hello, wybierz **informacje o połączeniu**:  
   ![Wybieranie opcji Informacje o połączeniu][ACSConnectInfo]
4. Skopiuj hello wartości kontroli dostępu.

Podczas wdrażania projektu usługi BizTalk w programie Visual Studio należy wprowadzić obszar nazw kontroli dostępu. Witaj kontroli dostępu w przestrzeni nazw jest tworzony automatycznie dla usługi BizTalk.

można używać wartości kontroli dostępu Hello z dowolnej aplikacji. Po utworzeniu usługi BizTalk Azure tej przestrzeni nazw kontroli dostępu określa hello uwierzytelniania z wdrożeniem usługi BizTalk. Wybierz toochange hello subskrypcji lub zarządzania hello przestrzeni nazw, **usługi ACTIVE DIRECTORY** w hello w lewym okienku nawigacji, a następnie wybierz obszar nazw. pasek zadań Hello listą dostępnych opcji.

Kliknięcie przycisku **Zarządzaj** otwiera hello portalu zarządzania kontroli dostępu. W portalu zarządzania kontroli dostępu hello, hello używa usługi BizTalk **tożsamości usługi**:  
![Tożsamości usługi ACS w hello portalu zarządzania kontroli dostępu][ACSServiceIdentities]

Witaj tożsamość usługi kontroli dostępu jest zestaw poświadczeń, które umożliwia aplikacji lub tooauthenticate klientów bezpośrednio z kontroli dostępu i otrzymujących token.

> [!IMPORTANT]
> Witaj usługi BizTalk używa **właściciela** hello domyślnej usługi tożsamości i hello **hasło** wartość. Jeśli używasz wartość klucza symetrycznego hello zamiast hello wartość hasła hello następujący błąd może wystąpić.<br/><br/>*Nie można połączyć konto usługi zarządzania kontroli dostępu toohello z hello określone poświadczenia*
> 
> 

Niektóre wskazówki i zalecenia znajdują się w artykule [Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) (Zarządzanie obszarem nazw ACS).

## <a name="requirements-explained"></a>Wyjaśniono wymagania
Te wymagania nie dotyczą toohello bezpłatna wersja.

<table border="1">
<tr bgcolor="FAF9F9">
        <td><strong>Co jest potrzebne</strong></td>
        <td><strong>Do czego służy</strong></td>
</tr>
<tr>
<td>Subskrypcja platformy Azure</td>
<td>Subskrypcja Hello Określa, kto Zaloguj toohello portalu Azure. Właściciel konta Hello tworzy subskrypcję hello w <a HREF="https://account.windowsazure.com/Subscriptions"> subskrypcji platformy Azure</a>.
<br/><br/>
Witaj konto platformy Azure może mieć wiele subskrypcji i mogą być zarządzane przez każdy, kto jest dozwolone. Na przykład z właścicielem konta Azure tworzy subskrypcję o nazwie <em>BizTalkServiceSubscription</em> i zapewnia hello Administratorzy BizTalk w obrębie firmy (na przykład ContosoBTSAdmins@live.com) dostęp toothis subskrypcji. W tym scenariuszu Administratorzy BizTalk hello Zaloguj toohello portalu Azure i ma pełny Administrator prawa tooall hello hostowanej usługi w subskrypcji hello, w tym usług BizTalk Azure. Administratorzy BizTalk Hello nie są hello posiadaczy konto platformy Azure i w związku z tym nie ma informacji dotyczących rozliczeń tooany dostępu.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Zarządzanie subskrypcjami i kont magazynu w hello portalu Azure</a> zawiera więcej informacji.
</td>
</tr>
<tr>
<td>Usługa Azure SQL Database</td>
<td>Przechowuje hello tabel, widoków i procedur składowanych używane przez usługi BizTalk, w tym dane śledzenia hello hello.
<br/><br/>
Podczas tworzenia usługi BizTalk można użyć istniejącego serwera Azure SQL Server, bazy danych SQL Azure lub automatycznie utworzyć nowy serwer bądź nową bazę danych.
<br/><br/>
automatycznie skonfigurowano Hello skalowania bazy danych SQL. Zazwyczaj Skala domyślna hello jest wystarczająca dla usługi BizTalk. Zmiana skali hello ma wpływ na cennik. Zobacz artykuł <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
 (Konta i rozliczenia w bazie danych SQL Azure)<br/><br/>
<strong>Uwagi</strong>
<br/>
<ul>
<li> Po utworzeniu nowego serwera Azure SQL Server i bazy danych usługi Azure zostaną automatycznie włączone. Usługi BizTalk Hello wymaga usług Azure można włączyć.</li>
<li>Jeśli tworzysz nową bazę danych SQL Azure na istniejącym serwerze SQL Azure hello reguły zapory powitania serwera nie są zmieniane. W związku z tym jest możliwe, innych usług Azure nie są dozwolone baz danych serwera toohello dostępu.</li>
</ul>
</td>
</tr>
<tr>
<td>Przestrzeń nazw kontroli dostępu Azure</td>
<td>Uwierzytelnia za pomocą usługi Azure BizTalk Services. Podczas wdrażania projektu usługi BizTalk w programie Visual Studio należy wprowadzić obszar nazw kontroli dostępu. Witaj kontroli dostępu w przestrzeni nazw jest tworzony automatycznie podczas tworzenia usługi BizTalk.</td>
</tr>

<tr>
<td>Konto usługi Azure Storage</td>
<td>Zapewnia dostęp do tootables, obiekty BLOB i kolejki używane przez użytkownika usługi BizTalk toosave powitania po:

<ul>
<li>Ten monitor hello usługi BizTalk plików dziennika. monitorowanie danych wyjściowych Hello jest wyświetlany na powitania **monitorowanie** kartę w hello portalu Azure.</li>
<li>Podczas tworzenia X12 lub AS2 umowę pomiędzy partnerami, można włączyć właściwości wiadomości powitania Archiwizacja funkcji toostore. Te dane są zapisywane w hello konta magazynu.</li>
</ul>
<br/>
Podczas tworzenia usługi BizTalk można użyć istniejącego konta usługi Storage lub automatycznie utworzyć nowe.
<br/><br/>
Witaj domyślne ustawienia przechowywania są wystarczające dla usługi BizTalk.
<br/><br/>
Podczas tworzenia konta usługi Storage następuje automatyczne utworzenie klucza podstawowego i klucza pomocniczego. Te klucze kontroli dostępu tooyour konta magazynu. Usługi BizTalk Hello automatycznie używa hello klucza podstawowego.
<br/><br/>
Więcej informacji znajduje się w artykule <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a>.
</td>
</tr>

<tr>
<td>Prywatny certyfikat SSL</td>
<td>
Po utworzeniu usługi Azure BizTalk Services zostaje również utworzony adres URL HTTPS zawierający nazwę usługi BizTalk. Ten adres URL jest automatycznie skonfigurowana toouse tylko do tworzenia certyfikatu z podpisem własnym. Do produkcji potrzebny jest prywatny certyfikat SSL.
<br/><br/>
<strong>Ważne informacje dotyczące certyfikatów SSL</strong>

<ul>
<li>Data wygaśnięcia certyfikatu Hello musi być mniejsza niż 5 lat.</li>
<li>Wszystkie certyfikaty prywatne wymagają hasła. Zapamiętaj to hasło i udostępnij je swoim administratorom.</li>
<li>Certyfikaty z podpisem własnym są używane w środowisku testowania/programowania. Podczas korzystania z certyfikatów z podpisem własnym, zaimportuj hello certyfikatu tooyour osobistym magazynie certyfikatów i hello magazynu certyfikatów zaufanych głównych urzędów certyfikacji.</li>
</ul>
<br/>Podczas wysyłania urzędu certyfikacji tooyour żądania certyfikatu hello produkcji, należy podać hello następujące właściwości certyfikatu:
<br/>

<ul>
<li><strong>Ulepszone użycie klucza</strong>: usługa Azure BizTalk Services wymaga przynajmniej uwierzytelniania przez serwer.</li>
<li><strong>Nazwa pospolita</strong>: Wprowadź hello pełną nazwę domeny (FQDN) adres URL usługi BizTalk Azure. Zobacz temat <a HREF="#CreateService">Create a BizTalk Service</a> (Tworzenie usługi BizTalk) w tym artykule.</li>
</ul>
<br/>
Po utworzeniu hello usługi BizTalk można dodać nowe lub inny certyfikat.
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a>Połączenia hybrydowe
Podczas tworzenia usługi BizTalk Azure hello **połączeń hybrydowych** karta jest dostępna:

![Karta Połączenia hybrydowe][HybridConnectionTab]

Połączenia hybrydowe są używane tooconnect Azure witryny sieci Web lub usługą Azure mobile Services tooany lokalnych zasobów, która używa portu TCP statycznego, takich jak SQL Server, MySQL, interfejsy API protokołu HTTP sieci Web, usług Mobile Services i większość niestandardowych usług sieci Web.  Połączenia hybrydowe i hello usługę BizTalk karty są różne. Hello Usługa karty BizTalk jest używane tooconnect usług BizTalk Azure tooan lokalnego Linia biznesowych (LOB) systemu.

 Zobacz [połączeń hybrydowych](integration-hybrid-connection-overview.md) toolearn więcej, w tym tworzenie i zarządzanie nimi połączeń hybrydowych było możliwe.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy jest tworzony usługi BizTalk, zapoznaj się z różnych hello [usługi BizTalk Services: karty Pulpit nawigacyjny, Monitor i skali](biztalk-dashboard-monitor-scale-tabs.md). Usługa BizTalk jest gotowa dla aplikacji. toostart tworzenia aplikacji, przejdź do zbyt[usług BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Zobacz też
* [BizTalk Services: Editions Chart (Usługa BizTalk Services: zestawienie wersji)](biztalk-editions-feature-chart.md)<br/>
* [BizTalk Services: State Chart (Usługa BizTalk Services: tabela stanów)](biztalk-service-state-chart.md)<br/>
* [BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)](biztalk-backup-restore.md)<br/>
* [BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)](biztalk-throttling-thresholds.md)<br/>
* [BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)](biztalk-issuer-name-issuer-key.md)<br/>
* [Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Połączenia hybrydowe](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
