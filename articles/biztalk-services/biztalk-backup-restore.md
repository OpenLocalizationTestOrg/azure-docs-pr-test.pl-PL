---
title: "aaaCreate i przywracania kopii zapasowej w usługach BizTalk | Dokumentacja firmy Microsoft"
description: "Usługi BizTalk Services zawiera kopii zapasowej i przywracania. Dowiedz się, jak toocreate i przywracania kopii zapasowej i określić kopiami zapasowymi. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a>BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Usługi BizTalk Azure obejmuje możliwości tworzenia kopii zapasowych i przywracania. W tym temacie opisano, jak toobackup i przywracania usługi BizTalk Services przy użyciu hello klasycznego portalu Azure.

Można również tworzyć kopie zapasowe usługi BizTalk Services przy użyciu hello [interfejsu API REST usługi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584). 

> [!NOTE]
> Połączenia hybrydowe nie kopii zapasowej, niezależnie od hello Edition. Należy ponownie utworzyć połączeń hybrydowych.


## <a name="before-you-begin"></a>Przed rozpoczęciem
* Kopii zapasowej i przywracania może nie być dostępne dla wszystkich wersji. Zobacz [usługi BizTalk Services: wersje wykresu](biztalk-editions-feature-chart.md).
* Przy użyciu hello klasycznego portalu Azure, możesz utworzyć kopię zapasową na żądanie lub utworzyć zaplanowaną kopię zapasową. 
* Wykonaj kopię zapasową zawartości może być przywrócona toohello tej samej usługi BizTalk lub tooa nową usługę BizTalk. toorestore hello usługi BizTalk przy użyciu powitalne nazwę istniejącej usługi BizTalk hello muszą zostać usunięte, a nazwa hello musi być dostępne. Po usunięciu usługi BizTalk, może potrwać dłużej, niż żądana dla hello takie same nazwy toobe dostępne. Jeśli nie może czekać na powitania sama nazwa toobe dostępne, a następnie przywrócić tooa nową usługę BizTalk.
* Usługi BizTalk Services może być przywrócona toohello tej samej wersji lub nowszą wersję. Przywracanie usługi BizTalk Services tooa niższej wersji z po hello tworzenia kopii zapasowej, nie jest obsługiwane.
  
    Na przykład kopii zapasowej przy użyciu hello podstawowych wydanie można przywrócić toohello Premium Edition. Kopii zapasowej przy użyciu hello Premium Edition nie może być przywrócona toohello Standard Edition.
* numery kontroli EDI Hello kopię zapasową toomaintain ciągłości hello numery kontroli. Wiadomości są przetwarzane po utworzeniu ostatniej kopii zapasowej hello, przywrócenia tej kopii zapasowej zawartości może spowodować numery zduplikowane kontroli.
* Partia ma aktywne wiadomości, proces partii hello **przed** wykonywania kopii zapasowej. Podczas tworzenia kopii zapasowej (jako wymagane lub zaplanowane), wiadomości w partiach nigdy nie są przechowywane. 
  
    **Jeśli wykonywana jest kopia zapasowa z active wiadomości w partii, te komunikaty nie kopii zapasowej i w związku z tym zostaną utracone.**
* Opcjonalnie: W hello Portal usługi BizTalk, Zatrzymaj wszystkie operacje zarządzania.

## <a name="create-a-backup"></a>Tworzenie kopii zapasowej
Kopię zapasową można wykonać w dowolnym momencie i całkowicie jest kontrolowany przez użytkownika. W tej sekcji przedstawiono hello kroki toocreate kopii zapasowych przy użyciu hello Azure classic portal, w tym:

[Na żądanie kopii zapasowej](#backupnow)

[Planowanie tworzenia kopii zapasowych](#backupschedule)

#### <a name="backupnow"></a>Na żądanie kopii zapasowej
1. Hello klasycznego portalu Azure, wybierz **usługi BizTalk Services**, a następnie wybierz hello ma toobackup usługi BizTalk.
2. W hello **pulpitu nawigacyjnego** wybierz opcję **kopię zapasową** u dołu hello hello strony.
3. Wprowadź nazwę kopii zapasowej. Na przykład wprowadź *myBizTalkService*BU*data*.
4. Wybierz konto magazynu obiektów blob i wybierz hello znacznikiem wyboru toostart hello w kopii zapasowej.

Po wykonaniu kopii zapasowej hello kontener z wprowadzona nazwa hello kopii zapasowej jest tworzony w hello konta magazynu. Ten kontener zawiera konfiguracji kopii zapasowej usługi BizTalk.

#### <a name="backupschedule"></a>Planowanie tworzenia kopii zapasowych
1. Hello klasycznego portalu Azure, wybierz **usługi BizTalk Services**, wybierz hello nazwa usługi BizTalk mają tooschedule hello tworzenia kopii zapasowej, a następnie wybierz hello **Konfiguruj** kartę.
2. Zestaw hello **stanu kopii zapasowej** za**automatyczne**. 
3. Wybierz hello **konta magazynu** toostore hello kopii zapasowej, należy wprowadzić hello **częstotliwość** toocreate Witaj i jak długo kopii zapasowych hello tookeep (**dni przechowywania**):
   
    ![][AutomaticBU]
   
    **Uwagi**     
   
   * W **dni przechowywania**, hello okres przechowywania musi być większa niż częstotliwość wykonywania kopii zapasowych hello.
   * Wybierz **zawsze Zachowuj co najmniej jedną kopię zapasową**nawet wtedy, gdy po upływie okresu przechowywania hello.
4. Wybierz pozycję **Zapisz**.

Po uruchomieniu zaplanowanego zadania tworzenia kopii zapasowej, tworzy kontener (toostore dane kopii zapasowej) na koncie magazynu hello wprowadzony. nosi nazwę kontenera hello Hello *usługi BizTalk Nazwa daty i godziny*. 

Jeśli wyświetlane hello pulpit nawigacyjny usługi BizTalk **** stanu:

![Stan ostatniej kopii zapasowej według harmonogramu][BackupStatus] 

Witaj łącze powoduje otwarcie hello dzienniki operacji usług zarządzania toohelp Rozwiązywanie problemów. Zobacz [usługi BizTalk Services: Rozwiązywanie problemów przy użyciu dzienników operacji](http://go.microsoft.com/fwlink/p/?LinkId=391211).

## <a name="restore"></a>Przywracanie
Można przywrócić kopii zapasowych z hello klasycznego portalu Azure lub hello [przywrócić usług BizTalk — wersja interfejsu API REST usługi](http://go.microsoft.com/fwlink/p/?LinkID=325582). Ta sekcja zawiera hello toorestore czynności przy użyciu klasycznego portalu hello.

#### <a name="before-restoring-a-backup"></a>Przed przywróceniem kopii zapasowej
* Nowe śledzenie, archiwizacji i monitorowania magazynów można wprowadzić podczas przywracania usługi BizTalk.
* Witaj, te same dane środowiska uruchomieniowego EDI jest przywracane. Kopia zapasowa środowiska uruchomieniowego EDI Hello przechowuje numery kontroli hello. numery kontroli Hello przywrócić są w kolejności od chwili hello hello tworzenia kopii zapasowej. Wiadomości są przetwarzane po utworzeniu ostatniej kopii zapasowej hello, przywrócenia tej kopii zapasowej zawartości może spowodować numery zduplikowane kontroli.

#### <a name="restore-a-backup"></a>Przywracanie kopii zapasowej
1. Hello klasycznego portalu Azure, wybierz **nowy** > **usługi aplikacji** > **usługi BizTalk** > **przywracania** :
   
    ![Przywracanie kopii zapasowej][Restore]
2. W **kopii zapasowej adresu URL**, wybierz ikonę folderu hello i rozwiń konto usługi Azure storage hello czy magazyny hello kopia zapasowa konfiguracji usługi BizTalk. Rozwiń kontener hello i w okienku po prawej stronie powitania, wybierz hello odpowiadającego Utwórz kopię zapasową pliku txt. 
   <br/><br/>
   Wybierz **Otwórz**.
3. Na powitania **usługi BizTalk przywracania** wprowadź **nazwa usługi BizTalk** i sprawdź hello **adresu URL domeny**, **wersji**i **Region** dla hello przywrócić usługi BizTalk. **Utwórz nowe wystąpienie bazy danych SQL** dla hello śledzenia bazy danych:
   
    ![][RestoreBizTalkService]
   
    Wybierz strzałkę dalej hello.
4. Sprawdź nazwę hello hello bazy danych SQL, wprowadź powitania serwera fizycznego, której zostanie utworzona hello bazy danych SQL i nazwę użytkownika/hasło dla tego serwera.

    Wersja bazy danych SQL hello tooconfigure, rozmiar i inne właściwości, wybierz opcję **skonfigurować zaawansowane ustawienia bazy danych**. 

    Wybierz strzałkę dalej hello.

1. Utwórz nowe konto magazynu, lub wprowadź istniejącego konta magazynu hello usługi BizTalk.
2. Wybierz hello znacznikiem wyboru toostart hello przywracania.

Po pomyślnym zakończeniu przywracania hello, nową usługę BizTalk znajduje się w stanie wstrzymania na stronie usługi BizTalk Services hello hello klasycznego portalu Azure.

### <a name="postrestore"></a>Po przywróceniu kopii zapasowej
Witaj usługi BizTalk jest zawsze przywracać w **zawieszone** stanu. W tym stanie można wprowadzać żadnych zmian konfiguracji przed hello nowe środowisko będzie działać, w tym:

* Jeśli utworzono usługę BizTalk aplikacji przy użyciu hello Azure SDK usługi BizTalk, może być konieczne tootooupdate hello kontroli dostępu (ACS) poświadczenia w tych toowork aplikacji ze środowiskiem hello przywrócona.
* Możesz przywrócić tooreplicate usługi BizTalk istniejącego środowiska usługi BizTalk. W takiej sytuacji jeśli są skonfigurowane w portalu usługi BizTalk Services z oryginalnego hello umowy, korzystających z folderu źródłowego FTP, może być konieczne tooupdate hello umów w nowo przywrócony hello środowiska toouse folderu FTP innego źródła. W przeciwnym razie może być tę samą wiadomość hello dwóch różnych umów w trakcie toopull.
* Jeśli toohave przywrócić wiele środowisk usługi BizTalk, upewnij się, że docelowa hello poprawne środowisko w aplikacji Visual Studio hello, poleceń cmdlet programu PowerShell, interfejsów API REST lub handlem partnera OM interfejsów API Management.
* Jest tooconfigure automatyczne kopie zapasowe dobrym rozwiązaniem w środowisku usługi BizTalk hello nowo przywrócony.

toostart hello usługi BizTalk w hello klasycznego portalu Azure, wybierz hello przywracane usługi BizTalk i wybierz **Wznów** hello paska zadań. 

## <a name="what-gets-backed-up"></a>Kopiami zapasowymi
Po utworzeniu kopii zapasowej hello następujące elementy są kopii zapasowej:

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH>Elementy kopii zapasowej</TH> 
</tr> 
<tr>
<td colspan="2">
 <strong>Portal usług Azure BizTalk</strong></td>
</tr> 
<tr>
<td>Konfiguracja i środowiska wykonawczego</td> 
<td>
<ul>
<li>Szczegóły partnera i profilu</li>
<li>Umowy z partnerami</li>
<li>Niestandardowe zestawy wdrożony</li>
<li>Mostków wdrożony</li>
<li>Certyfikaty</li>
<li>Transformacje wdrożony</li>
<li>Potoki</li>
<li>Szablony utworzony i zapisany w hello Portal usługi BizTalk</li>
<li>X12 mapowania ST01 i GS01</li>
<li>Numery kontroli (EDI)</li>
<li>Wartości AS2 komunikat Micznych</li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2">
 <strong>Usługi BizTalk Azure</strong></td>
</tr> 
<tr>
<td>Certyfikat SSL</td> 
<td>
<ul>
<li>Dane certyfikatu SSL</li>
<li>Hasło certyfikatu SSL</li>
</ul>
</td>
</tr> 
<tr>
<td>Ustawienia usługi BizTalk</td> 
<td>
<ul>
<li>Liczba jednostek skali</li>
<li>Wersja</li>
<li>Wersja produktu:</li>
<li>Region/centrum danych</li>
<li>Dostęp do usługi kontroli (ACS) w przestrzeni nazw i klucza</li>
<li>Parametry połączenia bazy danych śledzenia</li>
<li>Archiwizowanie parametry połączenia konta magazynu</li>
<li>Monitorowanie parametrów połączenia konta magazynu</li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2">
 <strong>Dodatkowe elementy</strong></td>
</tr> 
<tr>
<td>Śledzenie bazy danych</td> 
<td>Po utworzeniu hello usługi BizTalk hello śledzenia Szczegóły bazy danych są wprowadzane w tym powitania serwera bazy danych SQL Azure i hello śledzenia nazwy bazy danych. Witaj śledzenia bazy danych nie jest automatycznie kopii zapasowej.
<br/><br/>
<strong>Ważne</strong><br/>
Jeśli hello śledzenia bazy danych są usuwane i hello odzyskane potrzeb bazy danych, musi istnieć poprzedniej kopii zapasowej. Jeśli kopia zapasowa nie istnieje, hello śledzenia bazy danych i jego dane nie są możliwe do odzyskania. W takiej sytuacji należy utworzyć nową bazę danych śledzenia z hello samej nazwie bazy danych. Replikacja geograficzna jest zalecane.</td>
</tr> 
</table>

## <a name="next"></a>Następne kroki
usługi BizTalk Services Azure toocreate w hello Azure przejdź do portalu klasycznego zbyt[usługi BizTalk Services: klasycznego portalu Azure za pomocą udostępniania](http://go.microsoft.com/fwlink/p/?LinkID=302280). toostart tworzenia aplikacji, przejdź do zbyt[usług BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Zobacz też
* [Usługi BizTalk kopii zapasowej](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Przywracanie z kopii zapasowej usługi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [BizTalk Services: Provisioning Status Chart (Usługa BizTalk Services: aprowizowanie wykresu stanu)](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [BizTalk Services: Dashboard, Monitor and Scale tabs (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

