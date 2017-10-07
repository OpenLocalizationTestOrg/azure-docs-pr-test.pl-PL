---
title: "aaaHPC pakiet klastra w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toointegrate HPC Pack 2016 klaster na platformie Azure za pomocą usługi Azure Active Directory"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a>Zarządzanie klastra HPC Pack platformie Azure przy użyciu usługi Azure Active Directory
[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) obsługuje integrację z [usługi Azure Active Directory](../../active-directory/index.md) (Azure AD) dla administratorów, którzy wdrożenie klastra HPC Pack na platformie Azure.



Wykonaj kroki hello w tym artykule hello następujące zadania wysokiego poziomu: 
* Ręcznie integracji klastra HPC Pack z dzierżawy usługi Azure AD
* Zarządzanie i planowanie zadań w klastrze HPC Pack na platformie Azure 

Inne aplikacje i usługi toointegrate standardowe kroki integracji z usługą Azure AD rozwiązanie klastra HPC Pack jest zgodna. W tym artykule przyjęto założenie, że czytelnik zna podstawowe użytkownika zarządzania w usłudze Azure AD. Aby uzyskać więcej informacji i tło, zobacz hello [dokumentacji usługi Azure Active Directory](../../active-directory/index.md) i hello następujących sekcji.

## <a name="benefits-of-integration"></a>Korzyści wynikające z integracji


Azure Active Directory (Azure AD) to wielodostępne oparte na chmurze katalogami i tożsamościami zarządzania usługa, która zapewnia dostęp do rejestracji jednokrotnej (SSO) toocloud rozwiązania.

Integracja z usługą Azure AD klastra HPC Pack można osiągnąć następujące cele hello:

* Usuń hello tradycyjnych kontrolera domeny usługi Active Directory z klastra HPC Pack hello. To może pomóc zmniejszyć koszty utrzymania hello klastra, jeśli nie jest to niezbędne do firmy oraz proces wdrażania hello przyspieszyć hello.
* Wykorzystanie hello następujące korzyści, które zostały podane przy użyciu usługi Azure AD:
    *   Logowanie jednokrotne 
    *   Dla klastra HPC Pack hello na platformie Azure przy użyciu lokalnej tożsamości usługi AD 

    ![Środowiska usługi Active Directory platformy Azure](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a>Wymagania wstępne
* **Klaster HPC Pack 2016 wdrożonymi na maszynach wirtualnych Azure** — Aby uzyskać instrukcje, zobacz [wdrożenie klastra HPC Pack 2016 na platformie Azure](hpcpack-2016-cluster.md). Należy nazwę DNS hello hello węzła głównego i hello poświadczenia administratora klastrów, aby wykonać kroki hello w tym artykule.

  > [!NOTE]
  > Integracja z usługą Azure Active Directory nie jest obsługiwany w wersjach pakietu HPC przed HPC Pack 2016.



* **Komputer kliencki** — należy Windows lub Windows Server klienta zbyt Uruchom HPC Pack klienta narzędzia komputera. Jeśli chcesz tylko zadania toosubmit interfejsu API REST lub portalu internetowego HPC Pack hello toouse, można użyć dowolnego komputera klienckiego wybranych przez użytkownika.

* **HPC Pack narzędzi klienta** -Zainstaluj narzędzia klienta HPC Pack hello na komputerze klienckim hello przy użyciu pakietu instalacyjnego wolnego hello dostępnej w sklepie hello Microsoft Download Center.


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a>Krok 1: Zarejestruj serwera klastra HPC hello dzierżawy usługi Azure AD
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Kliknij przycisk **usługi Active Directory** w hello menu po lewej stronie, a następnie kliknij przycisk hello żądanego katalogu w ramach subskrypcji. Musi mieć uprawnienie tooaccess zasobów w katalogu hello.
3. Kliknij przycisk **użytkowników**i upewnij się, że istnieją już konta użytkowników utworzone lub skonfigurowane.
4. Kliknij przycisk **aplikacji** > **Dodaj**, a następnie kliknij przycisk **Dodaj aplikację moją organizację**. Wprowadź następujące informacje w Kreatorze hello hello:
    * **Nazwa** -HPCPackClusterServer
    * **Typ** — wybierz tę opcję **aplikacji i/lub sieci Web interfejs API sieci Web**
    * **Adres URL logowania na**— Witaj bazowy adres URL dla próbki hello jest domyślnie`https://hpcserver`
    * **Identyfikator URI aplikacji** - `https://<Directory_name>/<application_name>`. Zastąp `<Directory_name`> z hello Pełna nazwa dzierżawy usługi Azure AD, na przykład `hpclocal.onmicrosoft.com`i Zastąp `<application_name>` o nazwie hello wybrano wcześniej.

5. Po dodaniu aplikacji hello, kliknij przycisk **Konfiguruj**. Skonfiguruj hello następujące właściwości:
    * Wybierz **tak** dla **aplikacji jest wieloma dzierżawcami**
    * Wybierz **tak** dla **aplikacji wymagane tooaccess przypisanie użytkownika**.

6. Kliknij pozycję **Zapisz**. Po zakończeniu zapisywania, kliknij przycisk **Zarządzanie manifestu**. Ta akcja spowoduje pobranie aplikacji manifestu JavaScript object notation (JSON) pliku. Edytuj hello pobrane manifeście dzięki umieszczeniu hello `appRoles` Ustawianie i dodawanie hello następującej roli aplikacji:
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. Zapisz plik hello. Następnie kliknij w portalu hello **Zarządzanie manifestu** > **przekazać manifestu**. Następnie możesz przekazać hello edytowanych manifestu.
8. Kliknij przycisk **użytkowników**, wybierz użytkownika, a następnie kliknij przycisk **przypisać**. Przypisać jeden hello dostępnych ról (HpcUsers lub HpcAdminMirror) toohello użytkownika. Powtórz ten krok z dodatkowym użytkownikom w katalogu hello. Aby uzyskać ogólne informacje o użytkownikach z klastra, zobacz [Zarządzanie użytkownikami klastra](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).

   > [!NOTE] 
   > Użytkownicy toomanage, zaleca się używanie bloku w wersji zapoznawczej usługi Azure Active Directory hello w hello [portalu Azure](https://portal.azure.com).
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a>Krok 2: Zarejestruj klienta klastra HPC hello dzierżawy usługi Azure AD

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Kliknij przycisk **usługi Active Directory** w hello menu po lewej stronie, a następnie kliknij przycisk hello żądanego katalogu w ramach subskrypcji. Musi mieć uprawnienie tooaccess zasobów w katalogu hello.
3. Kliknij przycisk **aplikacji** > **Dodaj**, a następnie kliknij przycisk **Dodaj aplikację moją organizację**. Wprowadź następujące informacje w Kreatorze hello hello:

    * **Nazwa** -HPCPackClusterClient
    * **Typ** — wybierz tę opcję **aplikację Native Client**
    * **Identyfikator URI przekierowania** - `http://hpcclient`

4. Po dodaniu aplikacji hello, kliknij przycisk **Konfiguruj**. Kopiuj hello **identyfikator klienta** wartość i zapisz go. Należy to później podczas konfigurowania aplikacji.

5. W **uprawnienia aplikacji tooother**, kliknij przycisk **Dodawanie aplikacji**. Wyszukiwanie i dodaj aplikację HpcPackClusterServer hello (utworzonego w kroku 1).

6. W hello **delegowane uprawnienia** listy rozwijanej wybierz **HpcClusterServer dostępu**. Następnie kliknij przycisk **Save** (Zapisz).


## <a name="step-3-configure-hello-hpc-cluster"></a>Krok 3: Konfigurowanie klastra HPC hello

1. Połącz toohello HPC Pack 2016 węzła głównego na platformie Azure.

2. Uruchom program HPC PowerShell.

3. Uruchom następujące polecenie hello:

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    gdzie

    * `AADTenant`Określa nazwę dzierżawy usługi Azure AD hello, takich jak`hpclocal.onmicrosoft.com`
    * `AADClientAppId`Określa identyfikator klienta hello aplikacji hello utworzony w kroku 2.

4. Uruchom ponownie usługę HpcSchedulerStateful hello.

    W klastrze z wieloma węzłami head można uruchomić następujące polecenia programu PowerShell na powitania węzła głównego tooswitch hello repliki podstawowej dla usługi HpcSchedulerStateful hello hello:

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a>Krok 4: Zarządzania i przesyłania zadań z powitania klienta

narzędzi tooinstall hello HPC Pack klienta na komputerze, pobrać pliki instalacyjne HPC Pack 2016 (Instalacja pełna) z hello Microsoft Download Center. Po rozpoczęciu instalacji hello, wybierz opcję instalacji hello hello **narzędzi klienta HPC Pack**.

komputer kliencki hello tooprepare, zainstaluj certyfikat hello używane podczas [Konfiguracja klastra HPC](hpcpack-2016-cluster.md) na komputerze klienckim hello. Użyj standardowych systemu Windows certyfikatu zarządzania procedury tooinstall hello certyfikatu publicznego toohello **Certyfikaty — bieżący użytkownik** > **zaufane główne urzędy certyfikacji** przechowywania. 

Można teraz Uruchom polecenia HPC Pack hello lub użyj toosubmit hello graficznego interfejsu użytkownika Menedżera HPC Pack zadania i zarządzać zadaniami klastra przy użyciu konta hello Azure AD. Dla opcji przesyłania zadań, zobacz [klastra HPC przesyłania zadań tooan HPC Pack na platformie Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).

> [!NOTE]
> Podczas próby tooconnect klastra HPC Pack toohello na platformie Azure na powitania po raz pierwszy, zostanie wyświetlony okna podręczne. Wprowadź toolog poświadczeń użytkownika usługi Azure AD w. Hello token następnie są buforowane. Nowsze klastra toohello połączeń w hello Azure Użyj buforowane token, o ile nie jest brany pod uwagę zmiany lub hello w pamięci podręcznej.
>
  
Na przykład po wykonaniu poprzednich kroków hello, musisz mogą wykonywać kwerendę o zadań z klienta lokalnego w następujący sposób:

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a>Przydatne polecenia cmdlet umożliwiające przesyłanie zadań o integracji z usługą Azure AD 

### <a name="manage-hello-local-token-cache"></a>Zarządzanie pamięci podręcznej tokenu lokalne powitania

HPC Pack 2016 zawiera dwa nowe polecenia cmdlet środowiska PowerShell klastra HPC toomanage hello lokalnej pamięci podręcznej tokenu. Te polecenia cmdlet są przydatne do przesyłania zadań nieinteraktywnie. Zobacz poniższy przykład hello:

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a>Ustaw poświadczenia hello przesyłania zadań przy użyciu konta hello Azure AD 

Czasami może być toorun hello zadania w obszarze użytkownika klastra HPC hello (dla klastra HPC przyłączonych do domeny, Uruchom jako jedną domenę użytkownika; dla klastra HPC przyłączone do domeny, Uruchom jako jeden użytkownik lokalny na powitania węzła głównego).

1. Użyj hello następujące polecenia tooset hello poświadczeń:

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. Następnie przesłać zadania hello w następujący sposób. Hello zadanie działa w obszarze $localUser na powitania węzłów obliczeniowych.

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   Jeśli `–Credential` nie zostanie określony z `Submit-HpcJob`, hello lub zadania uruchamiana zamapowanych użytkownika lokalnego jako hello konto usługi Azure AD. (klaster HPC hello tworzy użytkownika lokalnego z hello takie same nazwy jako hello zadań hello toorun konta usługi Azure AD).
    
3. Ustaw datę rozszerzonej dla hello konto usługi Azure AD. Jest to przydatne podczas uruchamiania zadań MPI w węzłach systemu Linux przy użyciu konta hello Azure AD.

   * Ustaw datę rozszerzonej dla hello samo konto usługi Azure AD

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * Ustaw zwiększoną ilość danych, a następnie uruchom jako użytkownika klastra HPC
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

