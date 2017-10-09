---
title: 'Synchronizacja programu Azure AD Connect: zagadnienia i zadania operacyjne | Dokumentacja firmy Microsoft'
description: "W tym temacie opisano zadania operacyjne synchronizacji usługi Azure AD Connect i w jaki sposób tooprepare pracy tego składnika."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a>Synchronizacja programu Azure AD Connect: brany pod uwagę i zadania operacyjne
Celem Hello tego tematu jest toodescribe zadań operacyjnych synchronizacji usługi Azure AD Connect.

## <a name="staging-mode"></a>Tryb przejściowy
Tryb przejściowy może służyć do kilka scenariuszy, w tym:

* Wysoka dostępność.
* Testowania i wdrażania nowych zmian konfiguracji.
* Wprowadzenie nowego serwera i zlikwidować stary hello.

Z serwerem w trybie przejściowym można zmieniać toohello zmian konfiguracji i Podgląd hello przed wprowadzeniem powitania serwera active. Można też toorun pełny import i pełną synchronizację tooverify oczekuje wszystkie zmiany przed wprowadzeniem tych zmian w środowisku produkcyjnym.

Podczas instalacji można wybrać powitania serwera toobe w **Tryb przejściowy**. Ta akcja powoduje powitania serwera active importowania i synchronizacji, ale nie działa on żadnych eksportów. Serwer w trybie przejściowym nie jest uruchomiona, synchronizacja haseł lub zapisywania zwrotnego haseł, nawet jeśli te funkcje są wybrane podczas instalacji. Po wyłączeniu trybu przejściowego powitania serwera rozpoczyna eksportowanie umożliwia synchronizację haseł i włącza funkcję zapisywania zwrotnego haseł.

Nadal można wymusić eksportu przy użyciu Menedżera usługi synchronizacji hello.

Serwer w trybie przejściowym nadal tooreceive zmiany z usługi Active Directory i Azure AD. Zawsze ma kopię hello najnowsze zmiany i podejmij bardzo szybko mogą za pośrednictwem obowiązki hello innego serwera. Jeśli serwer podstawowy tooyour zmian konfiguracji, jest toomake Twojego odpowiedzialność hello tego samego serwera toohello zmiany w trybie przejściowym.

Dla osób, które znajomości starszych technologii synchronizacji hello Tryb przejściowy różni się od hello serwer ma własną bazę danych SQL. Taka architektura umożliwia hello przemieszczania tryb serwera toobe znajdujących się w różnych centrach danych.

### <a name="verify-hello-configuration-of-a-server"></a>Sprawdź konfigurację powitania serwera
tooapply tej metody, wykonaj następujące kroki:

1. [Przygotowanie](#prepare)
2. [Konfiguracja](#configuration)
3. [Importuje i synchronizuje](#import-and-synchronize)
4. [Sprawdź](#verify)
5. [Serwer active przełącznika](#switch-active-server)

#### <a name="prepare"></a>Przygotowanie
1. Zainstalować program Azure AD Connect, wybierz **Tryb przejściowy**i usuń zaznaczenie pozycji **rozpoczęcia synchronizacji** na ostatniej stronie powitania w Kreatorze instalacji hello. W tym trybie można aparatu synchronizacji hello toorun ręcznie.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)
2. Znak poza/logowania i z hello start menu wybierz opcję **usługi synchronizacji**.

#### <a name="configuration"></a>Konfiguracja
Jeśli wprowadzono zmiany niestandardowe toohello podstawowego serwera i chcesz toocompare hello konfiguracji z hello przemieszczania serwera, użyj [Dokumentatora konfiguracji usługi Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).

#### <a name="import-and-synchronize"></a>Importuje i synchronizuje
1. Wybierz **łączniki**, i wybierz hello pierwszego łącznika z typem hello **usług domenowych w usłudze Active Directory**. Kliknij przycisk **Uruchom**, wybierz pozycję **pełny import**, i **OK**. Wykonaj te kroki dla wszystkich łączników tego typu.
2. Wybierz hello łącznika z typem **usługi Azure Active Directory (Microsoft)**. Kliknij przycisk **Uruchom**, wybierz pozycję **pełny import**, i **OK**.
3. Upewnij się, że karta hello łączniki nadal jest zaznaczone. Dla poszczególnych łączników o typie **usług domenowych w usłudze Active Directory**, kliknij przycisk **Uruchom**, wybierz pozycję **synchronizacja przyrostowa**, i **OK**.
4. Wybierz hello łącznika z typem **usługi Azure Active Directory (Microsoft)**. Kliknij przycisk **Uruchom**, wybierz pozycję **synchronizacja przyrostowa**, i **OK**.

Masz teraz przemieszczanego eksportu zmiany tooAzure AD i lokalnej usłudze AD (Jeśli używasz wdrożenia hybrydowego programu Exchange). Następne kroki Hello pozwalają tooinspect nowości dotyczących toochange przed rozpoczęciem faktycznie hello eksportu toohello katalogów.

#### <a name="verify"></a>Weryfikuj
1. Uruchom wiersz polecenia i przejdź zbyt`%ProgramFiles%\Microsoft Azure AD Sync\bin`
2. Instalacja: `csexport "Name of Connector" %temp%\export.xml /f:x` nazwę hello hello łącznika można znaleźć w usługi synchronizacji. Ma ona nazwę too"contoso.com podobne — AAD" dla usługi Azure AD.
3. Skopiuj skrypt programu PowerShell hello z sekcji hello [CSAnalyzer](#appendix-csanalyzer) tooa plik o nazwie `csanalyzer.ps1`.
4. Otwórz okno programu PowerShell i Przeglądaj toohello folder, w którym utworzono hello skrypt programu PowerShell.
5. Instalacja: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.
6. Istnieje już plik o nazwie **processedusers1.csv** które można zbadać w programie Microsoft Excel. Wszystkie zmiany przemieszczane tooAzure toobe wyeksportowane AD znajdują się w tym pliku.
7. Wprowadź niezbędne zmiany danych toohello lub konfiguracji i uruchom następujące kroki ponownie (importowania i synchronizowania i sprawdź, czy) do momentu hello zmiany, które są o toobe wyeksportowane.

#### <a name="switch-active-server"></a>Serwer active przełącznika
1. Na powitania aktualnie aktywnego serwera wyłącz powitania serwera (DirSync/FIM/usługi Azure AD Sync), więc nie jest eksportowany tooAzure AD lub ustaw go w trybie (Azure AD Connect) przejściowym.
2. Uruchom Kreatora instalacji hello na powitania serwera w **Tryb przejściowy** i Wyłącz **Tryb przejściowy**.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)

## <a name="disaster-recovery"></a>Odzyskiwanie po awarii
Część projektu implementacji hello jest tooplan, dla jakiego toodo w przypadku braku awarii, w którym utratę powitania serwera synchronizacji. Istnieją różne modele toouse i które jeden toouse zależy od wielu czynników, takich jak:

* Co to jest ustawiona tolerancja, nie będą mogli upewnij zmian tooobjects w programie Azure AD podczas hello Przestój?
* Jeśli używasz synchronizacji haseł, czy użytkownicy hello zaakceptować mają toouse hello stare hasło w usłudze Azure AD w przypadku ich zmiany lokalne?
* Czy użytkownik ma zależności w czasie rzeczywistym operacje, takie jak zapisywanie zwrotne haseł?

W zależności od toothese hello odpowiedzi na pytania i zasady organizacji można zaimplementować jedną z następujących strategii hello:

* Ponownie w razie potrzeby.
* Zapasowe serwer zapasowy nie powinien, znany jako **Tryb przejściowy**.
* Użyj maszyn wirtualnych.

Jeśli nie używasz hello wbudowanych baza danych SQL Express, a następnie należy także przejrzeć hello [wysokiej dostępności SQL](#sql-high-availability) sekcji.

### <a name="rebuild-when-needed"></a>Skompiluj ponownie w razie potrzeby
Strategia działało jest tooplan do odbudowywania serwera, w razie potrzeby. Zazwyczaj instalowanie hello aparatu synchronizacji i hello początkowej importowania i synchronizacji można wykonać w kilka godzin. Jeśli serwer zapasowe jest niedostępna, jest możliwe tootemporarily Użyj aparatu synchronizacji hello toohost kontrolera domeny.

Serwer aparatu synchronizacji Hello nie przechowuje jakikolwiek stan informacje o obiektach hello tak hello bazy danych może zostać ponownie skompilowany od hello danych w usłudze Active Directory i Azure AD. Witaj **sourceAnchor** atrybutów jest używane toojoin hello obiektów z lokalnymi i hello chmury. Po odbudowaniu lokalne powitania serwera z istniejących obiektów i hello chmury, a następnie hello synchronizacji dopasowań aparat tych obiektów jednocześnie ponownie na ponowną instalację. Witaj należy toodocument i Zapisz kwestie hello zmian konfiguracji serwera toohello, takie jak reguły filtrowania i synchronizacji. Przed rozpoczęciem tej synchronizacji, należy ponownie zastosować te konfiguracje niestandardowe.

### <a name="have-a-spare-standby-server---staging-mode"></a>Zapasowe serwer zapasowy nie powinien — Tryb przejściowy
Jeśli masz środowisku bardziej złożonym, następnie o jeden lub więcej serwerów rezerwy jest zalecane. Podczas instalacji, możesz włączyć toobe serwera, w **Tryb przejściowy**.

Aby uzyskać więcej informacji, zobacz [Tryb przejściowy](#staging-mode).

### <a name="use-virtual-machines"></a>Użyj maszyn wirtualnych
Typowe i obsługiwane metody to aparat synchronizacji hello toorun na maszynie wirtualnej. W przypadku, gdy hello host ma problemu, obraz hello z serwerem aparatu synchronizacji hello może być tooanother migrowanego serwera.

### <a name="sql-high-availability"></a>SQL wysokiej dostępności
Jeśli nie używasz programu SQL Server Express dostarczonego z programem Azure AD Connect hello, następnie wysoką dostępność dla programu SQL Server należy również rozważyć. rozwiązania wysokiej dostępności Hello obsługiwane obejmują klastrowania SQL i AOA (zawsze włączone grupy dostępności). Nieobsługiwany rozwiązania obejmują dublowania.

Dodano obsługę dla SQL AOA tooAzure AD Connect w wersji 1.1.524.0. Przed zainstalowaniem usługi Azure AD Connect, należy włączyć SQL AOA. Podczas instalacji Azure AD Connect wykrywa, czy podane wystąpienie programu SQL hello jest włączone dla SQL AOA. Po włączeniu SQL AOA Azure dalsze AD Connect danych liczbowych czy SQL AOA jest skonfigurowany toouse synchronicznego lub asynchronicznego replikacji. Podczas konfigurowania hello odbiornika grupy dostępności, zaleca się ustawienie hello RegisterAllProvidersIP właściwości too0. Jest to spowodowane Azure AD Connect aktualnie używa programu SQL Native Client tooconnect tooSQL i SQL Native Client nie obsługuje użycia hello właściwości MultiSubNetFailover.

## <a name="appendix-csanalyzer"></a>Dodatek CSAnalyzer
Zobacz sekcję hello [Sprawdź](#verify) na temat toouse ten skrypt.

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a>Następne kroki
**Tematy poglądowe**  

* [Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji](active-directory-aadconnectsync-whatis.md)  
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)  
