---
title: aaaSubmit tooan zadania HPC Pack klastra na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooset się na lokalnym komputerze toosubmit zadań klastra HPC Pack tooan na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a>Przesyłanie zadań HPC z komputera lokalnego tooan klastra HPC Pack wdrożona na platformie Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Konfigurowanie lokalnego klienta komputera toosubmit zadania tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) klastra na platformie Azure. W tym artykule opisano, jak narzędzia zadania toosubmit tooset lokalnego komputera z klientem za pośrednictwem protokołu HTTPS toohello klastra na platformie Azure. W ten sposób kilku użytkowników klastra można przesłać zadania tooa oparte na chmurze HPC Pack klastra, ale bez połączyć się bezpośrednio węzła głównego toohello maszyny Wirtualnej lub uzyskiwania dostępu do subskrypcji platformy Azure.

![Przedstawia klastra tooa zadania na platformie Azure][jobsubmit]

## <a name="prerequisites"></a>Wymagania wstępne
* **Węzłem głównym HPC Pack wdrożony w maszynie Wirtualnej platformy Azure** -zalecane jest użycie automatycznych narzędzi takich jak [szablonie Szybki Start Azure](https://azure.microsoft.com/documentation/templates/) lub [skrypt programu PowerShell Azure](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) węzła głównego hello toodeploy i klaster. Należy nazwę DNS hello hello węzła głównego i hello poświadczenia administratora klastrów, aby wykonać kroki hello w tym artykule.
* **Komputer kliencki** -wymagają systemu Windows lub Windows Server komputera klienckiego, który można uruchomić narzędzia klienta HPC Pack (zobacz [wymagania systemowe](https://technet.microsoft.com/library/dn535781.aspx)). Jeśli chcesz tylko zadania toosubmit interfejsu API REST lub portalu internetowego HPC Pack hello toouse, można użyć dowolnego komputera klienckiego wybranych przez użytkownika.
* **Nośnik instalacyjny HPC Pack** -tooinstall hello HPC Pack narzędzi klienta, pakiet instalacyjny wolnego hello do najnowszej wersji HPC Pack (HPC Pack 2012 R2) jest niedostępna z [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Upewnij się, że pobierać hello tej samej wersji pakietu HPC, który jest zainstalowany w węźle głównym hello maszyny Wirtualnej.

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a>Krok 1: Instalowanie i konfigurowanie składników sieci web hello na powitania węzła głównego
tooenable klastra toohello zadania toosubmit interfejsu REST za pośrednictwem protokołu HTTPS, upewnij się, że składniki sieci web HPC Pack hello są skonfigurowane w węźle głównym HPC Pack hello. Jeśli nie są już zainstalowane, należy najpierw zainstalować składniki sieci web hello, uruchamiając plik instalacyjny HpcWebComponents.msi hello. Następnie należy skonfigurować składniki hello przez uruchomienie skryptu środowiska PowerShell klastra HPC hello **HPCWebComponents.ps1 zestawu**.

Aby uzyskać szczegółowe procedury, zobacz [zainstalować składniki sieci Web hello Microsoft HPC Pack](http://technet.microsoft.com/library/hh314627.aspx).

> [!TIP]
> Niektóre szablony szybkiego startu usługi Azure HPC Pack Instalowanie i konfigurowanie składników sieci web hello automatycznie. Jeśli używasz hello [skrypt wdrożenia HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello klastra, można opcjonalnie zainstalować i skonfigurować składniki sieci web hello jako część wdrożenia hello.
> 
> 

**składniki sieci web hello tooinstall**

1. Połącz z węzłem głównym toohello maszyny Wirtualnej, używając hello poświadczenia administratora klastra.
2. Z folderu instalacji pakietu HPC hello Uruchom HpcWebComponents.msi na powitania węzła głównego.
3. Wykonaj kroki hello w składnikach hello tooinstall hello kreatora w sieci web

**składniki sieci web hello tooconfigure**

1. W węźle głównym hello Uruchom program HPC PowerShell jako administrator.
2. Lokalizacja toohello katalogu toochange skryptu konfiguracji hello, hello wpisz następujące polecenie:
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. tooconfigure hello interfejsu REST i uruchomić hello HPC usługi sieci Web, hello wpisz następujące polecenie:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. Gdy zostanie wyświetlony monit o tooselect certyfikat, wybierz certyfikat hello, który odpowiada toohello publicznej nazwy DNS hello węzła głównego. Na przykład w przypadku wdrożenia hello węzła głównego maszyny Wirtualnej przy użyciu hello klasycznego modelu wdrażania, nazwa certyfikatu hello wygląda następująco: CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net. Jeśli używasz modelu wdrażania usługi Resource Manager hello, nazwa certyfikatu hello wygląda CN =&lt;*HeadNodeDnsName*&gt;.&lt; *region*&gt;. cloudapp.azure.com.
   
   > [!NOTE]
   > Należy wybrać ten certyfikat później podczas przesyłania zadań toohello węzła głównego z komputera lokalnego. Brak zaznaczenia lub skonfigurować certyfikat, który odpowiada nazwa komputera toohello hello węzła głównego w domenie usługi Active Directory hello (na przykład, CN =*MyHPCHeadNode.HpcAzure.local*).
   > 
   > 
5. portal sieci web hello tooconfigure składania zadania hello wpisz następujące polecenie:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. Po ukończeniu działania skryptu hello zatrzymać i ponownie uruchomić hello usługa harmonogramu zadań HPC, wpisując hello następujące polecenia:
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a>Krok 2: Zainstaluj narzędzia klienta HPC Pack hello na komputerze lokalnym
Jeśli chcesz tooinstall hello HPC Pack klienta narzędzia na komputerze, Pobierz pliki instalacji HPC Pack (Instalacja pełna) z hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Po rozpoczęciu instalacji hello, wybierz opcję instalacji hello hello **narzędzi klienta HPC Pack**.

klienckie HPC Pack hello toouse narzędzia toosubmit zadania toohello węzła głównego maszyny Wirtualnej, należy również tooexport certyfikat od węzła głównego hello i zainstaluj go na komputerze klienckim hello. Witaj, certyfikat musi mieć. CER format.

**certyfikat hello tooexport z węzłem głównym hello**

1. W węźle głównym hello Dodaj hello certyfikatów przystawki tooa konsoli Microsoft Management Console dla hello konta na komputerze lokalnym. Przystawka hello tooadd znajduje się [dodać tooan hello przystawki certyfikatów konsoli MMC](https://technet.microsoft.com/library/cc754431.aspx).
2. W drzewie konsoli hello rozwiń **certyfikaty — komputer lokalny** > **osobistych**, a następnie kliknij przycisk **certyfikaty**.
3. Zlokalizuj certyfikat hello skonfigurowane dla składników sieci web HPC Pack hello w [krok 1: Instalowanie i konfigurowanie składników sieci web hello na powitania węzła głównego](#step-1:-install-and-configure-the-web-components-on-the-head-node) (na przykład, CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).
4. Kliknij prawym przyciskiem myszy hello certyfikatu, a następnie kliknij przycisk **wszystkie zadania** > **wyeksportować**.
5. W Kreatorze eksportu certyfikatów hello, kliknij przycisk **dalej**i upewnij się, że **nie eksportuj klucza prywatnego hello** jest zaznaczone.
6. Certyfikat x.509 szyfrowany binarnie algorytmem hello wykonaj pozostałe kroki hello kreatora tooexport hello certyfikatu w DER (. Format CER).

**tooimport hello certyfikatów na komputerze klienckim hello**

1. Skopiuj wyeksportowany z hello węzła głównego tooa folderu na komputerze klienckim hello hello certyfikat.
2. Na komputerze klienckim hello Uruchom certmgr.msc.
3. Rozwiń węzeł w Menedżerze certyfikatów **Certyfikaty — bieżący użytkownik** > **zaufane główne urzędy certyfikacji**, kliknij prawym przyciskiem myszy **certyfikaty**, a następnie Kliknij przycisk **wszystkie zadania** > **importu**.
4. W hello Kreatora importu certyfikatów kliknij **dalej** i wykonaj hello kroki tooimport hello wyeksportowany certyfikat w magazynie zaufanych głównych urzędów certyfikacji toohello węzła głównego hello.

> [!TIP]
> Może pojawić się ostrzeżenie, ponieważ hello urzędu certyfikacji na powitania węzła głównego nie jest rozpoznawane przez komputer kliencki hello. Do celów testowych, możesz zignorować to ostrzeżenie i pełne importu certyfikatów hello.
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a>Krok 3: Uruchamianie testu zadań w klastrze hello
Spróbuj uruchomionych zadań na powitania konfiguracji klastra na platformie Azure z hello tooverify lokalnego komputera. Na przykład można użyć narzędzia HPC Pack graficznego interfejsu użytkownika lub polecenia toosubmit zadania toohello klastra. Umożliwia także zadania toosubmit portalu sieci web.

**toorun zadania przesyłania polecenia na komputerze klienckim hello**

1. Na komputerze klienckim, w którym są zainstalowane narzędzia klienta HPC Pack hello Uruchom wiersz polecenia.
2. Wpisz polecenie przykładowe. Na przykład toolist wszystkich zadań w klastrze hello, wpisz polecenie podobne tooone z powitania po, w zależności od hello pełną nazwą DNS hello węzła głównego:
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    lub
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > Użyj hello pełną nazwą DNS hello węzła głównego, nie adres IP hello w adresie URL harmonogramu hello. Jeśli określisz adresu IP hello pojawia się błąd podobny zbyt "hello, certyfikat serwera musi tooeither zawiera prawidłowy łańcuch zaufania lub toobe umieszczane w magazynie zaufanych certyfikatów głównych hello."
   > 
   > 
3. Po wyświetleniu monitu wpisz nazwę użytkownika hello (w postaci hello &lt;DomainName&gt;\\&lt;UserName&gt;) i hasło administratora klastra HPC hello lub innego użytkownika klastra skonfigurowanego. Możesz wybrać toostore poświadczenia hello lokalnie więcej operacji zadań.
   
    Zostanie wyświetlona lista zadań.

**toouse Menedżer zadań klastra HPC na komputerze klienckim hello**

1. Jeśli wcześniej nie przechowują poświadczeń domeny użytkownika, klastra, podczas przesyłania zadania, można dodać hello poświadczeń w Menedżerze poświadczeń.
   
    a. W Panelu sterowania na komputerze klienckim hello Uruchom Menedżera poświadczeń.
   
    b. Kliknij przycisk **poświadczeń systemu Windows** > **Dodaj poświadczenie ogólnego**.
   
    c. Określ adres internetowy hello (na przykład https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler lub https://&lt;HeadNodeDnsName&gt;.&lt; region&gt;.cloudapp.azure.com/HpcScheduler) i nazwą użytkownika hello (&lt;DomainName&gt;\\&lt;UserName&gt;) i hasło administratora klastra hello lub innego użytkownika klastra, który został skonfigurowany.
2. Na komputerze klienckim hello Uruchom Menedżer zadań klastra HPC.
3. W hello **wybierz węzeł Head** okno dialogowe, typ hello adresu URL toohello węzła głównego na platformie Azure (na przykład https://&lt;HeadNodeDnsName&gt;. cloudapp.net lub https://&lt;HeadNodeDnsName&gt;. &lt;region&gt;. cloudapp.azure.com).
   
    Menedżer zadań klastra HPC otwiera i jest wyświetlana lista zadań na powitania węzła głównego.

**portal sieci web hello toouse systemem hello węzła głównego**

1. Uruchom przeglądarkę sieci web na komputerze klienckim hello i wprowadź jedno z następujących adresów, w zależności od hello pełną nazwą DNS węzła głównego hello hello:
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    lub
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. Okno dialogowe zabezpieczeń hello, który pojawia się wpisz poświadczenia domeny hello administratora klastra HPC hello. (Można również dodać innych klastra użytkowników w różnych ról. Zobacz [Zarządzanie użytkownikami klastra](https://technet.microsoft.com/library/ff919335.aspx).)
   
    portal sieci web Hello otwiera widok listy toohello zadania.
3. Kliknij toosubmit przykładowe zadania, które zwraca ciąg hello "Hello World" z klastra hello **nowe zadanie** w nawigacji po lewej stronie powitania.
4. Na powitania **nowe zadanie** w obszarze **ze stron przesyłania**, kliknij przycisk **HelloWorld**. zostanie wyświetlona strona przesyłania zadania Hello.
5. Kliknij przycisk **przesłać**. Po wyświetleniu monitu podaj poświadczenia domeny hello administratora klastra HPC hello. zadanie Hello i hello identyfikator zadania jest wyświetlana na powitania **Moje zadania** strony.
6. wyniki hello tooview hello zadania, który zostanie przesłany, kliknij hello identyfikator zadania, a następnie kliknij **zadania widoku** danych wyjściowych polecenia hello tooview (w obszarze **dane wyjściowe**).

## <a name="next-steps"></a>Następne kroki
* Istnieje także możliwość przesyłania zadań toohello klastrze platformy Azure z hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).
* Toosubmit zadań klastra z klientów systemu Linux, zobacz hello Python przykładowa w hello [HPC Pack 2012 R2 SDK oraz przykładowy kod](https://www.microsoft.com/download/details.aspx?id=41633).

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
