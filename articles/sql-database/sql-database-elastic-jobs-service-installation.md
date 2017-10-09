---
title: zadania elastycznej bazy danych aaaInstalling | Dokumentacja firmy Microsoft
description: Przeprowadzenie instalacji hello elastycznej zadanie funkcji.
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a>Instalowanie omówienie zadania elastycznej bazy danych
[**Zadania elastyczne bazy danych** ](sql-database-elastic-jobs-overview.md) można zainstalować za pomocą programu PowerShell lub za pośrednictwem hello Portal.You klasycznego Azure mogą uzyskać dostęp do toocreate zadania i zarządzać nimi przy użyciu interfejsu API środowiska PowerShell hello tylko w przypadku instalowania pakietu programu PowerShell hello. Ponadto hello interfejsów API środowiska PowerShell Podaj znacznie więcej funkcji niż hello portal w tym momencie.

Jeśli użytkownik zainstalował już **zadania elastycznej bazy danych** za pośrednictwem hello portalu z istniejącego **puli elastycznej**, hello najnowsze programu Powershell w wersji zapoznawczej obejmuje skrypty tooupgrade istniejącej instalacji. Jest zdecydowanie zalecane tooupgrade Twojego toohello instalacji najnowszych **zadania elastycznej bazy danych** składników w kolejności tootake korzystać z nowych funkcji udostępnianych za pośrednictwem hello interfejsów API środowiska PowerShell.

## <a name="prerequisites"></a>Wymagania wstępne
* Subskrypcja platformy Azure. Bezpłatnej wersji próbnej, zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell. Zainstaluj najnowszą wersję hello przy użyciu hello [Instalatora platformy sieci Web](http://go.microsoft.com/fwlink/p/?linkid=320376). Aby uzyskać szczegółowe informacje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
* [Narzędzie wiersza polecenia NuGet](https://nuget.org/nuget.exe) jest pakietem zadania elastycznej bazy danych hello tooinstall używane. Aby uzyskać więcej informacji zobacz http://docs.nuget.org/docs/start-here/installing-nuget.

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a>Pobieranie i importowanie hello elastycznej bazy danych zadania programu PowerShell pakietu
1. Uruchom okno poleceń programu PowerShell usługi Microsoft Azure i przejdź do katalogu toohello, którego pobrano narzędzie wiersza polecenia NuGet (nuget.exe).
2. Pobieranie i importowanie **zadania elastycznej bazy danych** pakietu do bieżącego katalogu hello z hello następujące polecenie:
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    Witaj **zadania elastycznej bazy danych** pliki są umieszczane w katalogu lokalnego hello w folderze o nazwie **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** gdzie *x.x.xxxx.x* odzwierciedla hello numer wersji. polecenia cmdlet programu PowerShell Hello (w tym wymagany klient biblioteki) znajdują się w hello **tools\ElasticDatabaseJobs** podkatalogu i hello tooinstall skrypty programu PowerShell, uaktualniania i odinstalowywania również znajdują się w hello  **narzędzia** podkatalogu.
3. Przejdź toohello narzędzia podkatalogu w folderze Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello wpisując narzędzia dysku cd, na przykład:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. Wykonanie hello.\InstallElasticDatabaseJobsCmdlets.ps1 skryptu toocopy hello ElasticDatabaseJobs katalogu do $home\Documents\WindowsPowerShell\Modules. Spowoduje to również automatycznie zaimportowanie modułu hello do użycia, na przykład:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a>Zainstaluj składniki zadania elastycznej bazy danych hello przy użyciu programu PowerShell
1. Uruchom okno poleceń programu PowerShell usługi Microsoft Azure i przejdź toohello \tools podkatalogu w folderze Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello: wpisz \tools dysku cd
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. Uruchom skrypt programu PowerShell.\InstallElasticDatabaseJobs.ps1 hello i dostarczać wartości żądanej zmienne. Ten skrypt utworzy hello składników zawartych w [zadania elastycznej bazy danych, składników i cenach](sql-database-elastic-jobs-overview.md#components-and-pricing) oraz konfigurowanie hello usługi w chmurze Azure tooappropriately Użyj hello składników zależnych.

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

Po uruchomieniu tego polecenia okna otwiera pytania o **nazwy użytkownika** i **hasło**. Nie jest to Twoje poświadczenia platformy Azure, wprowadź hello nazwę użytkownika i hasło, które będą poświadczeniami administratora hello ma toocreate hello nowego serwera.

można zmodyfikować parametry Hello na to wywołanie próbki dla żądane ustawienia. Hello poniżej zamieszczono więcej informacji dotyczących zachowania hello każdego parametru:

<table style="width:100%">
  <tr>
    <th>Parametr</th>
    <th>Opis</th>
  </tr>

<tr>
    <td>Grupy zasobów o nazwie</td>
    <td>Zawiera nazwę grupy zasobów platformy Azure hello utworzoną hello toocontain nowo utworzone składniki platformy Azure. Tego parametru, domyślnie przyjmowana jest zbyt "__ElasticDatabaseJob". Nie jest zalecane toochange tej wartości.</td>
    </tr>

</tr>

    <tr>
    <td>ResourceGroupLocation</td>
    <td>Udostępnia hello toobe lokalizacji platformy Azure używana dla hello nowo utworzone składniki platformy Azure. Ten parametr domyślnie toohello USA centralnej lokalizacji.</td>
</tr>

<tr>
    <td>ServiceWorkerCount</td>
    <td>Zawiera liczbę hello tooinstall pracowników usługi. Ten parametr domyślnie too1. Większa liczba procesów roboczych może być używane tooscale limit hello usługi i tooprovide wysokiej dostępności. Zalecane jest toouse "2" dla wdrożenia, które wymagają wysokiej dostępności usługi hello.</td>
    </tr>

</tr>
    <tr>
    <td>ServiceVmSize</td>
    <td>Udostępnia hello rozmiar maszyny Wirtualnej do użycia w ramach hello usługi w chmurze. Ten parametr domyślnie tooA0. Wartości parametrów A0/A1/A2/a3 są akceptowane powodujących hello worker roli toouse rozmiar ExtraSmall/małych/średnich/duży odpowiednio. Zobacz więcej informacji na temat rozmiarów roli procesu roboczego, FO [zadania elastycznej bazy danych, składników i cenach](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerDatabaseSlo</td>
    <td>Zapewnia cel poziomu usługi hello Standard edition. Ten parametr domyślnie tooS0. Wartości parametrów S0/S1/S2/S3 są akceptowane, które powodują hello bazy danych SQL Azure toouse hello odpowiednich SLO. Aby uzyskać więcej informacji na cele slo bazy danych SQL, zobacz [zadania elastycznej bazy danych, składników i cenach](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorUserName</td>
    <td>Zawiera nazwę użytkownika administratora hello hello nowo utworzonego serwera bazy danych SQL Azure. Gdy nie jest określony, okno poświadczenia programu PowerShell zostanie otwarty tooprompt o poświadczenia hello.</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorPassword</td>
    <td>Zapewnia hasło administratora hello hello nowo utworzonego serwera bazy danych SQL Azure. Po nie podano okno poświadczenia programu PowerShell zostanie otwarty tooprompt hello poświadczeń.</td>
</tr>
</table>

Dla systemów przeznaczonych o dużej liczby zadań uruchamianych jednocześnie na dużej liczbie baz danych, zaleca się parametry toospecify takich jak: - ServiceWorkerCount 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a>Aktualizowanie instalacji składników istniejącego zadania elastycznej bazy danych przy użyciu programu PowerShell
**Zadania elastyczne bazy danych** może zostać zaktualizowana w ramach istniejącej instalacji zapewnienia skalowalności i wysokiej dostępności. Ten proces umożliwia w ramach przyszłych uaktualnień kodu usługi bez konieczności toodrop i ponowne utworzenie bazy danych kontroli hello. Ten proces można również w hello tej samej wersji toomodify hello usługi liczba maszyn wirtualnych rozmiaru lub powitania serwera worker.

rozmiar maszyny Wirtualnej hello tooupdate instalacji, hello wykonywania następującego skryptu z parametrami zaktualizować wartości toohello wybranych przez użytkownika.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th>Parametr</th>
  <th>Opis</th>
</tr>

  <tr>
    <td>Grupy zasobów o nazwie</td>
    <td>Określa nazwę grupy zasobów platformy Azure hello składników zadania elastycznej bazy danych hello początkowo zostały zainstalowane. Tego parametru, domyślnie przyjmowana jest zbyt "__ElasticDatabaseJob". Ponieważ nie jest zalecane toochange ta wartość nie powinna mieć toospecify tego parametru.</td>
    </tr>
</tr>

</tr>

  <tr>
    <td>ServiceWorkerCount</td>
    <td>Zawiera liczbę hello tooinstall pracowników usługi.  Ten parametr domyślnie too1.  Większa liczba procesów roboczych może być używane tooscale limit hello usługi i tooprovide wysokiej dostępności.  Zalecane jest toouse "2" dla wdrożenia, które wymagają wysokiej dostępności usługi hello.</td>
</tr>

</tr>

    <tr>
    <td>ServiceVmSize</td>
    <td>Udostępnia hello rozmiar maszyny Wirtualnej do użycia w ramach hello usługi w chmurze. Ten parametr domyślnie tooA0. Wartości parametrów A0/A1/A2/a3 są akceptowane powodujących hello worker roli toouse rozmiar ExtraSmall/małych/średnich/duży odpowiednio. Zobacz więcej informacji na temat rozmiarów roli procesu roboczego, FO [zadania elastycznej bazy danych, składników i cenach](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a>Zainstaluj składniki zadania elastycznej bazy danych hello przy użyciu hello portalu
Po utworzeniu [utworzyć puli elastycznej](sql-database-elastic-pool-manage-portal.md), można zainstalować **zadania elastycznej bazy danych** składniki tooenable wykonywania zadań administracyjnych dla każdej bazy danych w puli elastycznej hello. Inaczej niż w przypadku, gdy przy użyciu hello **zadania elastycznej bazy danych** interfejsów API środowiska PowerShell, interfejsu portalu hello jest obecnie ograniczone tooonly wykonywane istniejącej puli.

**Szacowany czas toocomplete:** 10 minut.

1. W widoku pulpitu nawigacyjnego hello hello puli elastycznej za pośrednictwem hello [Azure Portal](https://portal.azure.com/#) , kliknij przycisk **Utwórz zadanie**.
2. W przypadku tworzenia zadania dla powitania po raz pierwszy, musisz zainstalować **zadania elastycznej bazy danych** klikając **warunki dotyczące**.
3. Zaakceptować warunki hello klikając hello wyboru.
4. W widoku hello "instalacji usług" kliknij **POŚWIADCZENIA zadania**.
   
    ![Instalowanie usług hello][1]
5. Wpisz nazwę użytkownika i hasło administratora bazy danych. W ramach instalacji hello jest tworzony nowy serwer bazy danych SQL Azure. W ramach tego nowego serwera nowej bazy danych, znany jako bazy danych kontroli hello jest tworzony i używany toocontain hello meta danych dla zadania elastycznej bazy danych. Witaj, nazwę użytkownika i hasło utworzone w tym miejscu są używane hello w celu rejestrowania w bazie danych kontroli toohello. Oddzielne poświadczeń jest używany do wykonania skryptu hello w przypadku baz danych w puli hello.
   
    ![Utwórz nazwę użytkownika i hasło][2]
6. Kliknij przycisk OK hello. składniki Hello są tworzone automatycznie w ciągu kilku minut w nowym [grupy zasobów](../azure-resource-manager/resource-group-overview.md). nową grupę zasobów Hello jest przypięty toohello start tablicy, jak pokazano poniżej. Zadania po utworzeniu elastycznej bazy danych (usługi w chmurze, bazę danych SQL, magistrali usług i magazyn) są tworzone w grupie hello.
   
    ![grupy zasobów w tablicy start][3]
7. Jeśli próba toocreate lub zarządzać zadania podczas instalowania zadania elastycznej bazy danych podczas dostarczania **poświadczenia** zobaczą następującą wiadomości powitania.
   
    ![Wdrożenie w toku][4]

Jeśli wymagana jest dezinstalację, należy usunąć hello grupę zasobów. Zobacz [jak toouninstall hello elastycznej bazy danych zadania składniki](sql-database-elastic-jobs-uninstall.md).

## <a name="next-steps"></a>Następne kroki
Upewnij się, poświadczenie o hello odpowiednie prawa do wykonania skryptu jest utworzony w każdej bazie danych w grupie hello, aby uzyskać więcej informacji, zobacz [Zabezpieczanie bazy danych SQL](sql-database-manage-logins.md).
Zobacz [Tworzenie zadania i zarządzać nimi elastycznej bazy danych](sql-database-elastic-jobs-create-and-manage.md) tooget uruchomiona.

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
