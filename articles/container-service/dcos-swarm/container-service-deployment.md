---
title: klaster aaaDeploy kontenera Docker na platformie Azure | Dokumentacja firmy Microsoft
description: "Wdrażanie rozwiązania Kubernetes, DC/OS lub Docker Swarm usługi kontenera platformy Azure przy użyciu portalu Azure hello lub szablonu usługi Resource Manager."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure, dcos, swarm, kubernetes, azure container service, acs
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a>Wdrażanie rozwiązania przy użyciu portalu Azure hello hostingu kontener Docker



Usługa kontenera platformy Azure zapewnia szybkie wdrażanie popularnych rozwiązań typu open source służących do aranżowania i klastrowania kontenerów. Ten dokument zawiera opis kroków wdrażania klastra usługi kontenera platformy Azure przy użyciu hello portalu Azure lub szablon szybkiego startu usługi Azure Resource Manager. 

Można także wdrożyć klaster usługi kontenera platformy Azure przy użyciu hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) lub hello interfejsów API usługi kontenera platformy Azure.

Aby uzyskać ogólne informacje, zobacz [Wprowadzenie do usługi Azure Container Service](../container-service-intro.md).


## <a name="prerequisites"></a>Wymagania wstępne

* **Subskrypcja platformy Azure**: jeśli jej nie masz, możesz utworzyć konto [bezpłatnej wersji próbnej](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935). W przypadku większego klastra warto rozważyć subskrypcję opartą na płatności zgodnie z rzeczywistym użyciem lub inne opcje zakupu.

    > [!NOTE]
    > Użycie subskrypcji platformy Azure i [przydziałami zasobów](../../azure-subscription-service-limits.md), takie jak limity przydziału rdzeni, można ograniczyć hello rozmiar klastra hello wdrażania. toorequest zwiększenia limitu przydziału, otwórz [żądania obsługi online klienta](../../azure-supportability/how-to-create-azure-support-request.md) bez dodatkowych opłat.
    >

* **Klucz publiczny SSH RSA**: w przypadku wdrażania, za pośrednictwem portalu hello lub jednego z szablonów Szybki Start Azure hello, wymaga klucza publicznego hello tooprovide do uwierzytelniania względem usługi kontenera platformy Azure, maszyny wirtualne. toocreate kluczy RSA Secure Shell (SSH), zobacz hello [OS X i Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) lub [Windows](../../virtual-machines/linux/ssh-from-windows.md) wskazówki. 

* **Identyfikator podmiotu zabezpieczeń klienta i klucz tajny usługi Service** (tylko Kubernetes): Aby uzyskać więcej informacji i wskazówek toocreate nazwy głównej usługi Azure Active Directory, zobacz [o hello nazwy głównej usługi dla klastra Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).



## <a name="create-a-cluster-by-using-hello-azure-portal"></a>Tworzenie klastra przy użyciu hello portalu Azure
1. Wybierz zalogować się w portalu Azure, toohello **nowy**i wyszukiwania hello Azure Marketplace w celu **usługi kontenera platformy Azure**.

    ![Usługa Azure Container Service w portalu Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. Kliknij pozycję **Azure Container Service**, a następnie kliknij przycisk **Utwórz**.

3. Na powitania **podstawy** bloku, wprowadź hello następujących informacji:

    * **Orchestrator**: Wybierz jedno z toodeploy orchestrators kontenera hello na powitania klastra.
        * **DC/OS**: wdraża klaster DC/OS.
        * **Swarm**: wdraża klaster Docker Swarm.
        * **Kubernetes**: wdraża klaster Kubernetes.
    * **Subskrypcja**: wybierz subskrypcję platformy Azure.
    * **Grupa zasobów**: Wprowadź nazwę nowej grupy zasobów hello hello wdrożenia.
    * **Lokalizacja**: Wybierz region platformy Azure dla hello wdrożenia usługi kontenera platformy Azure. Aby uzyskać informacje o dostępności, zobacz [Dostępność produktów według regionów](https://azure.microsoft.com/regions/services/).
    
    ![Ustawienia podstawowe](./media/container-service-deployment/acs-portal3.png)  <br />
    
    Kliknij przycisk **OK** gdy wszystko będzie gotowe tooproceed.

4. Na powitania **wzorca konfiguracji** bloku, wprowadź hello następujące ustawienia dla węzła głównego Linux hello lub w węzłach klastra hello (niektóre ustawienia są określone tooeach orchestrator):

    * **Nazwa DNS wzorca**: hello prefiks toocreate unikatową w pełni kwalifikowana nazwa domeny (FQDN) głównego hello. Hello wzorca nazwy FQDN ma formę hello *prefiks*dotyczących zarządzania*lokalizacji*. cloudapp.azure.com.
    * **Nazwa użytkownika**: hello nazwę użytkownika dla konta na poszczególnych maszyn wirtualnych systemu Linux hello hello klastra.
    * **Klucz publiczny SSH RSA**: Dodaj hello publicznego toobe klucza używany do uwierzytelniania względem maszyn wirtualnych systemu Linux hello. Ważne jest, aby klucz ten nie zawierał podziałów wierszy i zawiera hello `ssh-rsa` prefiks. Witaj `username@domain` przyrostek jest opcjonalna. Witaj klucz powinien wyglądać jak poniżej hello: **AAAAB3Nz ssh-rsa... <>...... UcyupgH azureuser@linuxvm** . 
    * **Nazwy głównej usługi**: w przypadku wybrania hello Kubernetes orchestrator Azure Active Directory wprowadź **usługi identyfikator podmiotu zabezpieczeń klienta** (nazywanych również hello appId) i **klucz tajny klienta główna usługi** (hasło). Aby uzyskać więcej informacji, zobacz [o hello nazwy głównej usługi dla klastra Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).
    * **Liczba wzorca**: hello liczba wzorców w klastrze hello.
    * **Diagnostyki maszyny Wirtualnej**: w przypadku niektórych orchestrators można włączyć diagnostyki maszyny Wirtualnej na powitania wzorców.

    ![Konfiguracja serwera głównego](./media/container-service-deployment/acs-portal4.png)  <br />

    Kliknij przycisk **OK** gdy wszystko będzie gotowe tooproceed.

5. Na powitania **konfiguracji agenta** bloku, wprowadź hello następujących informacji:

    * **Liczba agentów**: Docker Swarm i Kubernetes, ta wartość jest początkowa liczba agentów w zestawie skali agenta hello hello. DC/OS jest hello początkowa liczba agentów w prywatnym zestawie skali. Ponadto w przypadku koordynatora DC/OS jest tworzony publiczny zestaw skalowania zawierający wstępnie określoną liczbę agentów. Witaj agentów w tym publicznym zestawie jest określana na podstawie hello liczba wzorców w klastrze hello: jeden agent publiczny dla jeden z nich i dwóch agentów publicznych dla trzech lub 5 serwerów głównych.
    * **Rozmiar maszyny wirtualnej agenta**: hello rozmiar maszyn wirtualnych hello agenta.
    * **System operacyjny**: to ustawienie jest dostępne tylko wtedy, gdy wybrano hello Kubernetes orchestrator. Wybierz opcję dystrybucji systemu Linux lub toorun systemu operacyjnego Windows Server, na powitania agentów. To ustawienie określa, czy w klastrze można uruchamiać aplikacje kontenera systemu Linux czy Windows. 

        > [!NOTE]
        > Obsługa kontenerów systemu Windows dla klastrów Kubernetes jest dostępna w wersji zapoznawczej. W przypadku klastrów DC/OS i Swarm tylko agenci systemu Linux są obecnie obsługiwani przez usługę Azure Container Service.

    * **Poświadczenia agenta**: w przypadku wybrania systemu operacyjnego Windows hello, wprowadź administrator **nazwy użytkownika** i **hasło** dla agenta hello maszyn wirtualnych. 

    ![Konfiguracja agenta](./media/container-service-deployment/acs-portal5.png)  <br />

    Kliknij przycisk **OK** gdy wszystko będzie gotowe tooproceed.

6. Po zakończeniu weryfikacji usługi kliknij przycisk **OK**.

    ![Walidacja](./media/container-service-deployment/acs-portal6.png)  <br />

7. Przejrzyj postanowienia hello. proces wdrażania hello toostart, kliknij przycisk **Utwórz**.

    Został wybrany toopin hello wdrożenia toohello portalu Azure, można wyświetlić stan wdrożenia hello.

    ![Stan wdrożenia](./media/container-service-deployment/acs-portal8.png)  <br />

wdrożenie Hello zajmuje kilka minut toocomplete. Następnie hello klastra usługi kontenera platformy Azure jest gotowy do użycia.


## <a name="create-a-cluster-by-using-a-quickstart-template"></a>Tworzenie klastra przy użyciu szablonu szybkiego startu
Szablony szybkiego startu usługi Azure są dostępne toodeploy klastra usługi kontenera platformy Azure. Witaj pod warunkiem, że szablony szybkiego startu może być zmodyfikowany tooinclude dodatkowe lub zaawansowanych konfiguracji platformy Azure. toocreate klastra usługi kontenera platformy Azure przy użyciu szablonu Azure szybkiego startu, potrzebujesz subskrypcji platformy Azure. Jeśli jej nie masz, utwórz konto [bezpłatnej wersji próbnej](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935). 

Wykonaj te kroki toodeploy klastra przy użyciu szablonu i hello Azure CLI 2.0 (zobacz [instrukcje instalacji i](/cli/azure/install-az-cli2)).

> [!NOTE] 
> Jeśli w systemie Windows za pomocą podobne kroki toodeploy szablonu przy użyciu programu Azure PowerShell. Zobacz kroki w dalszej części tej sekcji. Można także wdrożyć szablon przy użyciu hello [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) lub innych metod.

1. toodeploy klastra DC/OS, Kubernetes lub Docker Swarm, wybierz jeden z szablonów Szybki Start dostępny hello z usługi GitHub. Częściowa lista została przedstawiona poniżej. są takie same, z wyjątkiem hello domyślnie wybraną aranżacją hello Hello DC/OS i Swarm szablonów.

    * [Szablon DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Szablon Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Szablon Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. Zaloguj się za tooyour konto platformy Azure (`az login`) i upewnij się, że hello Azure CLI jest połączonych tooyour subskrypcji platformy Azure. Hello domyślne subskrypcji można wyświetlić za pomocą następującego polecenia hello:

    ```azurecli
    az account show
    ```
    
    Jeśli masz więcej niż jeden tooset subskrypcji i potrzeb subskrypcji różne domyślne uruchomić `az account set --subscription` i określić nazwę lub identyfikator subskrypcji hello.

3. Najlepszym rozwiązaniem Użyj nowej grupy zasobów hello wdrożenia. toocreate grupę zasobów, użyj hello `az group create` polecenia Podaj nazwę grupy zasobów i lokalizacji: 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. Utwórz szablonu JSON w pliku zawierającego hello wymagane parametry. Plik parametrów hello pobierania o nazwie `azuredeploy.parameters.json` dołączony szablon usługi kontenera platformy Azure hello `azuredeploy.json` w witrynie GitHub. Wprowadź wymagane wartości parametrów dla klastra. 

    Na przykład toouse hello [szablon DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), podaj wartości parametrów dla `dnsNamePrefix` i `sshRSAPublicKey`. Zobacz opis hello w `azuredeploy.json` i opcje dla innych parametrów.  
 

5. Tworzenie klastra usługi kontenera przez przekazanie pliku parametrów wdrożenia hello z hello następujące polecenie, gdzie:

    * **RESOURCE_GROUP** to nazwa grupy zasobów hello utworzony w poprzednim kroku hello hello.
    * **DEPLOYMENT_NAME** (opcjonalnie) jest nazwą zapewniają toohello wdrożenia.
    * **TEMPLATE_URI** hello lokalizacja pliku wdrożenia hello `azuredeploy.json`. Ten identyfikator URI musi być hello plik Raw, nie toohello wskaźnika interfejsu użytkownika serwisu GitHub. toofind tego identyfikatora URI, wybierz hello `azuredeploy.json` pliku w usłudze GitHub, a następnie kliknij przycisk hello **Raw** przycisku.  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    Można też podać parametry jako ciąg w formacie JSON hello w wierszu polecenia. Użyj polecenia podobne toohello następującego:

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > wdrożenie Hello zajmuje kilka minut toocomplete.
    > 

### <a name="equivalent-powershell-commands"></a>Równoważne polecenia programu PowerShell
Szablon klastra usługi Azure Container Service można również wdrożyć przy użyciu programu PowerShell. Ten dokument jest oparty na powitania w wersji 1.0 [modułu Azure PowerShell](https://azure.microsoft.com/blog/azps-1-0/).

1. toodeploy klastra DC/OS, Kubernetes lub Docker Swarm, wybierz jeden z szablonów Szybki Start dostępny hello z usługi GitHub. Częściowa lista została przedstawiona poniżej. Należy pamiętać, że hello DC/OS i Swarm szablony są hello takie same, z wyjątkiem hello hello domyślnie wybraną aranżacją.

    * [Szablon DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Szablon Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Szablon Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. Przed utworzeniem klastra w ramach subskrypcji platformy Azure, sprawdź, czy w tooAzure została podpisana sesji programu PowerShell. Można to zrobić z hello `Get-AzureRMSubscription` polecenia:

    ```powershell
    Get-AzureRmSubscription
    ```

3. Jeśli potrzebujesz toosign w tooAzure, użyj hello `Login-AzureRMAccount` polecenia:

    ```powershell
    Login-AzureRmAccount
    ```

4. Najlepszym rozwiązaniem Użyj nowej grupy zasobów hello wdrożenia. toocreate grupę zasobów, użyj hello `New-AzureRmResourceGroup` polecenia, a następnie określ region nazwę i miejsce docelowe grupy zasobów:

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. Po utworzeniu grupy zasobów, można utworzyć klaster z hello następujące polecenia. Identyfikator URI hello Hello żądanego szablonu zostanie określony z hello `-TemplateUri` parametru. Po uruchomieniu tego polecenia program PowerShell wyświetli monit o wprowadzenie wartości parametrów wdrożenia.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a>Wprowadzanie parametrów szablonu
Jeśli znasz programu PowerShell, wiesz, że do przechodzenia między hello dostępne parametry polecenia cmdlet, wpisując znak minus (-), a następnie naciskając klawisz TAB hello. Ta funkcja działa również w przypadku parametrów zdefiniowanych w szablonie. Jak wpisywania nazwy szablonu hello hello polecenia cmdlet pobiera szablon hello, analizuje parametry hello i dynamicznie dodaje hello szablonu parametrów toohello polecenia. Dzięki temu wartości parametrów szablonu hello toospecify łatwe. A Jeśli zapomnisz wartości wymaganego parametru programu PowerShell wyświetla monit o podanie wartości hello.

Oto pełne polecenie Witaj z uwzględnionymi parametrami. Należy podać własne wartości nazw hello hello zasobów.

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a>Następne kroki
Teraz, gdy masz działający klaster, możesz zapoznać się z tymi dokumentami, aby uzyskać szczegółowe informacje na temat połączeń i zarządzania:

* [Połącz tooan klastra usługi kontenera platformy Azure](../container-service-connect.md)
* [Współpraca z usługą Azure Container Service i rozwiązaniem DC/OS](container-service-mesos-marathon-rest.md)
* [Współpraca z usługą Azure Container Service i rozwiązaniem Docker Swarm](container-service-docker-swarm.md)
* [Współpraca z usługą Azure Container Service i rozwiązaniem Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md)
