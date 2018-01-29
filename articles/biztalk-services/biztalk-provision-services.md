---
title: "Tworzenie usługi Azure BizTalk Services w witrynie Azure Portal | Microsoft Docs"
description: "Informacje o inicjowaniu obsługi lub tworzeniu usługi Azure BizTalk Services w portalu Azure; MABS, WABS"
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
ms.openlocfilehash: 61776b19ba0ee273b78e3b0a6f610e5701251dd0
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="create-biztalk-services-using-the-azure-portal"></a>Tworzenie usługi BizTalk Services przy użyciu portalu Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

> [!INCLUDE [Use APIs to manage MABS](../../includes/biztalk-services-retirement-azure-classic-portal.md)]

> [!TIP]
> Do zalogowania się do portalu Azure potrzebne jest konto Azure i subskrypcja platformy Azure. Jeśli nie masz konta, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Zobacz [Bezpłatna wersja próbna platformy Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).


## <a name="CreateService"></a>Tworzenie usługi BizTalk

> [!INCLUDE [Use APIs to manage MABS](../../includes/biztalk-services-retirement-azure-classic-portal.md)]

W zależności od stanu usługi BizTalk niektórych operacji nie można ukończyć. Aby uzyskać listę tych operacji, przejdź do artykułu [BizTalk Services State Chart](biztalk-service-state-chart.md) (Wykres stanu usługi BizTalk Services).

## <a name="post-provisioning-steps"></a>Kroki po zainicjowaniu obsługi
* [Instalacja certyfikatu na komputerze lokalnym](#InstallCert)
* [Dodanie certyfikatu gotowego do produkcji](#AddCert)
* [Uzyskanie przestrzeni nazw kontroli dostępu](#ACS)

#### <a name="InstallCert"></a>Instalacja certyfikatu na komputerze lokalnym

> [!INCLUDE [Use APIs to manage MABS](../../includes/biztalk-services-retirement-azure-classic-portal.md)]

#### <a name="AddCert"></a>Dodanie certyfikatu gotowego do produkcji

> [!INCLUDE [Use APIs to manage MABS](../../includes/biztalk-services-retirement-azure-classic-portal.md)]

#### <a name="ACS"></a>Uzyskanie przestrzeni nazw usługi Access Control

> [!INCLUDE [Use APIs to manage MABS](../../includes/biztalk-services-retirement-azure-classic-portal.md)]

Podczas wdrażania projektu usługi BizTalk w programie Visual Studio należy wprowadzić obszar nazw kontroli dostępu. Przestrzeń nazw kontroli dostępu dla usługi BizTalk jest tworzona automatycznie.

Wartości kontroli dostępu można używać z dowolną aplikacją. Podczas tworzenia usługi Azure BizTalk Services ta przestrzeń nazw kontroli dostępu kontroluje uwierzytelnianie za pomocą wdrożenia usługi BizTalk. Jeśli chcesz zmienić subskrypcję lub zarządzać przestrzenią nazw, wybierz opcję **ACTIVE DIRECTORY** w lewym okienku nawigacji, a następnie wybierz przestrzeń nazw. Pasek zadań zawiera opcje.

Kliknięcie przycisku **Zarządzaj** powoduje otwarcie portalu zarządzania kontroli dostępu. W portalu zarządzania kontroli dostępu usługa BizTalk korzysta z **tożsamości usługi**:  
![Tożsamości usługi ACS w portalu zarządzania usługi Access Control][ACSServiceIdentities]

Tożsamość usługi kontroli dostępu jest zestawem poświadczeń, który pozwala aplikacjom lub klientom uwierzytelniać się bezpośrednio za pomocą kontroli dostępu i odebrać token.

> [!IMPORTANT]
> Usługa BizTalk używa opcji **Właściciel** dla domyślnej tożsamości usługi oraz wartości **Hasło**. Jeśli używasz wartości Klucz symetryczny zamiast wartości Hasło, może wystąpić następujący błąd.<br/><br/>*Nie można nawiązać połączenia z kontem usługi zarządzania Access Control za pomocą podanych poświadczeń*
> 
> 

Niektóre wskazówki i zalecenia znajdują się w artykule [Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) (Zarządzanie obszarem nazw ACS).

## <a name="requirements-explained"></a>Wyjaśniono wymagania
Wymagania te nie dotyczą wersji bezpłatnej.

<table border="1">
<tr bgcolor="FAF9F9">
        <td><strong>Co jest potrzebne</strong></td>
        <td><strong>Do czego służy</strong></td>
</tr>
<tr>
<td>Subskrypcja platformy Azure</td>
<td>Subskrypcja określa, kto może logować się do platformy Azure. Właściciel konta tworzy subskrypcję w witrynie <a HREF="https://account.windowsazure.com/Subscriptions">Subskrypcje Azure</a>.
<br/><br/>
Konto platformy Azure może mieć wiele subskrypcji i może być zarządzane przez dowolną osobę, która ma odpowiednie uprawnienia. Na przykład właściciel konta Azure tworzy subskrypcję o nazwie <em>BizTalkServiceSubscription</em> i nadaje administratorom usługi BizTalk w firmie (na przykład ContosoBTSAdmins@live.com) prawo dostępu do niej. W tym scenariuszu administratorzy usługi BizTalk logują się do platformy Azure i mają pełne prawa administratora do wszystkich hostowanych usług w ramach subskrypcji, łącznie z usługą Azure BizTalk Services. Administratorzy usługi BizTalk nie są właścicielami konta Azure i dlatego nie mają dostępu do żadnych informacji dotyczących rozliczeń.
<br/><br/>Więcej informacji znajduje się w artykule 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Zarządzanie subskrypcjami i kontami usługi Storage na platformie Azure</a>.
</td>
</tr>
<tr>
<td>Usługa Azure SQL Database</td>
<td>Przechowuje tabele, widoki i procedury składowane używane przez usługę BizTalk, w tym dane śledzenia.
<br/><br/>
Podczas tworzenia usługi BizTalk można użyć istniejącego serwera Azure SQL Server, bazy danych SQL Azure lub automatycznie utworzyć nowy serwer bądź nową bazę danych.
<br/><br/>
Skala bazy danych SQL zostaje automatycznie skonfigurowana. Zwykle dla usługi BizTalk domyślna skala jest wystarczająca. Zmiana skali ma wpływ na cenę. Zobacz artykuł <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
 (Konta i rozliczenia w bazie danych SQL Azure)<br/><br/>
<strong>Uwagi</strong>
<br/>
<ul>
<li> Po utworzeniu nowego serwera Azure SQL Server i bazy danych usługi Azure zostaną automatycznie włączone. Usługa BizTalk wymaga, by usługi Azure zostały włączone.</li>
<li>W przypadku tworzenia nowej bazy danych SQL Azure na istniejącym serwerze Azure SQL Server reguły zapory serwera nie zostają zmienione. W związku z tym jest możliwe, że inne usługi Azure nie mają prawa dostępu do bazy danych serwera.</li>
</ul>
</td>
</tr>
<tr>
<td>Przestrzeń nazw kontroli dostępu Azure</td>
<td>Uwierzytelnia za pomocą usługi Azure BizTalk Services. Podczas wdrażania projektu usługi BizTalk w programie Visual Studio należy wprowadzić obszar nazw kontroli dostępu. Podczas tworzenia usługi BizTalk zostaje automatycznie utworzona przestrzeń nazw kontroli dostępu.</td>
</tr>

<tr>
<td>Konto usługi Azure Storage</td>
<td>Zapewnia dostęp do tabel, obiektów blob i kolejek używanych przez usługę BizTalk do zapisania:

<ul>
<li>Plików dziennika, które monitorują usługę BizTalk. </li>
<li>Podczas tworzenia umowy X12 lub AS2 między partnerami możesz włączyć funkcję archiwizacji, aby przechować właściwości komunikatów. Te dane są zapisywane na koncie usługi Storage.</li>
</ul>
<br/>
Podczas tworzenia usługi BizTalk można użyć istniejącego konta usługi Storage lub automatycznie utworzyć nowe.
<br/><br/>
Domyślne ustawienia usługi Storage są wystarczające dla usługi BizTalk.
<br/><br/>
Podczas tworzenia konta usługi Storage następuje automatyczne utworzenie klucza podstawowego i klucza pomocniczego. Klucze te kontrolują dostęp do konta usługi Storage. Usługa BizTalk automatycznie używa klucza podstawowego.
<br/><br/>
Więcej informacji znajduje się w artykule <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a>.
</td>
</tr>

<tr>
<td>Prywatny certyfikat SSL</td>
<td>
Po utworzeniu usługi Azure BizTalk Services zostaje również utworzony adres URL HTTPS zawierający nazwę usługi BizTalk. Ten adres URL zostaje automatycznie skonfigurowany do używania certyfikatu z podpisem własnym tylko do programowania. Do produkcji potrzebny jest prywatny certyfikat SSL.
<br/><br/>
<strong>Ważne informacje dotyczące certyfikatów SSL</strong>

<ul>
<li>Certyfikat musi wygasać nie później niż po 5 latach.</li>
<li>Wszystkie certyfikaty prywatne wymagają hasła. Zapamiętaj to hasło i udostępnij je swoim administratorom.</li>
<li>Certyfikaty z podpisem własnym są używane w środowisku testowania/programowania. W przypadku korzystania z certyfikatów z podpisem własnym zaimportuj certyfikat do osobistego magazynu certyfikatów oraz magazynu certyfikatów zaufanych głównych urzędów certyfikacji.</li>
</ul>
<br/>Podczas wysyłania żądania certyfikatu produkcji do urzędu certyfikacji należy podać następujące właściwości certyfikatu:
<br/>

<ul>
<li><strong>Ulepszone użycie klucza</strong>: usługa Azure BizTalk Services wymaga przynajmniej uwierzytelniania przez serwer.</li>
<li><strong>Nazwa pospolita</strong>: wprowadź w pełni kwalifikowaną nazwę domeny (FQDN) adresu URL usługi Azure BizTalk Services. Zobacz temat <a HREF="#CreateService">Create a BizTalk Service</a> (Tworzenie usługi BizTalk) w tym artykule.</li>
</ul>
<br/>
Po utworzeniu usługi BizTalk można dodać nowy lub inny certyfikat.
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting to any location.--->



## <a name="hybrid-connections"></a>Połączenia hybrydowe
Podczas tworzenia usługi Azure BizTalk Services dostępna jest karta **Połączenia hybrydowe**:

![Karta Połączenia hybrydowe][HybridConnectionTab]

Połączenia hybrydowe są używane do łączenia witryny sieci Web Azure lub usługi mobilnej Azure z dowolnym zasobem lokalnym, który używa statycznego portu TCP, takim jak serwer SQL Server, MySQL, interfejsy API HTTP Web, Mobile Services i większość niestandardowych usług sieci Web.  Połączenia hybrydowe i usługa adaptera BizTalk różnią się od siebie. Usługa adaptera BizTalk służy do łączenia usługi Azure BizTalk Services z lokalnym systemem Line of Business (LOB).

 Więcej informacji, m.in. na temat tworzenia połączeń hybrydowych i zarządzania nimi, znajduje się w artykule [Hybrid Connections](integration-hybrid-connection-overview.md) (Połączenia hybrydowe).

## <a name="next-steps"></a>Następne kroki
Po utworzeniu usługi BizTalk zapoznaj się z różnymi [usługami BizTalk Services: kartami Pulpit nawigacyjny, Monitor i Skala](biztalk-dashboard-monitor-scale-tabs.md). Usługa BizTalk jest gotowa dla aplikacji. Aby rozpocząć tworzenie aplikacji, przejdź do artykułu [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197) (Usługa Azure BizTalk Services).

## <a name="see-also"></a>Zobacz też
* [BizTalk Services: Editions Chart (Usługa BizTalk Services: zestawienie wersji)](biztalk-editions-feature-chart.md)<br/>
* [BizTalk Services: State Chart (Usługa BizTalk Services: tabela stanów)](biztalk-service-state-chart.md)<br/>
* [BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)](biztalk-backup-restore.md)<br/>
* [BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)](biztalk-throttling-thresholds.md)<br/>
* [BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)](biztalk-issuer-name-issuer-key.md)<br/>
* [Jak rozpocząć pracę z zestawem SDK usługi Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Połączenia hybrydowe](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
