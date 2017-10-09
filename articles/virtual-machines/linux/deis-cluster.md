---
title: "aaaDeploy Deis 3 węzłami klastra | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocreate węzłem 3 Deis klastra na platformie Azure przy użyciu szablonu usługi Azure Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a>Wdrażanie i konfigurowanie węzłem 3 Deis klastra w systemie Azure
W tym artykule przedstawiono inicjowania obsługi administracyjnej [Deis](http://deis.io/) klastra na platformie Azure. Obejmuje wszystkie kroki hello tworzenie hello toodeploying wymagane certyfikaty i skalowanie próbkę **Przejdź** aplikacji w klastrze nowo aprowizowanej hello.

Witaj Poniższy diagram przedstawia hello architektury systemu hello wdrożone. Zarządza administrator systemu przy użyciu klastra hello Deis narzędzi, takich jak **deis** i **deisctl**. Nawiązywane są połączenia za pośrednictwem usługi równoważenia obciążenia Azure, który przesyła dalej węzłów w klastrze hello tooone połączeń hello hello elementu członkowskiego. dostęp klientom Witaj wdrożone aplikacje za pomocą hello również równoważenia obciążenia. W takim przypadku Usługa równoważenia obciążenia hello przekazuje tooa ruchu hello Deis routera sieci, które dodatkowo routs kontenery Docker toocorresponding ruchu hostowanych w klastrze hello.

  ![Diagram architektury wdrożonej Desis klastra](./media/deis-cluster/architecture-overview.png)

W kolejności toorun za pośrednictwem hello następujące kroki potrzebne są:

* Aktywna subskrypcja platformy Azure. Jeśli nie masz, możesz pobrać wolnego ślad [witryny azure.com](https://azure.microsoft.com/).
* Służbowy lub grup zasobów platformy Azure toouse identyfikator służbowe. Jeśli masz konto osobiste i zaloguj się za pomocą identyfikatora Microsoft, należy za[utworzyć identyfikator pracy niż osobiste](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Albo — w zależności od systemu operacyjnego klienta — Witaj [programu Azure PowerShell](/powershell/azureps-cmdlets-docs) lub hello [Azure CLI for Mac, Linux i Windows](../../cli-install-nodejs.md).
* [Biblioteki OpenSSL](https://www.openssl.org/). Biblioteki OpenSSL jest używane toogenerate hello wymagane certyfikaty.
* Klient Git, takich jak [Git Bash](https://git-scm.com/).
* tootest hello przykładowej aplikacji, należy również serwer DNS. Można użyć dowolnego serwerów DNS lub usługi, które obsługują rekordy A symboli wieloznacznych.
* Toorun komputera Deis narzędziami klienckimi. Można użyć komputera lokalnego lub maszyny wirtualnej. Te narzędzia można uruchomić na dowolnym dystrybucji systemu Linux, ale hello poniższe instrukcje korzystają z systemu Ubuntu.

## <a name="provision-hello-cluster"></a>Zainicjuj obsługę hello klastra
W tej sekcji użyjesz [usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) szablonu z repozytorium typu open source hello [azure — Szybki Start — szablony](https://github.com/Azure/azure-quickstart-templates). Po pierwsze będą kopiowane dół hello szablonu. Następnie utworzysz nową parę kluczy SSH do uwierzytelniania. A następnie należy skonfigurować nowy identyfikator dla klastra należy. A na koniec użyjesz skrypt powłoki hello lub hello PowerShell skryptu tooprovision hello klastra.

1. Klonowanie repozytorium hello: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. Folder szablonu przejdź toohello:
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. Utwórz nową parę kluczy SSH za pomocą ssh-keygen:
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. Generowanie za pomocą hello powyżej klucza prywatnego certyfikatu:
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. Przejdź za[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate nowy token klastra, który wygląda coś, takich jak:
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   Każdy klaster CoreOS musi toohave unikatowy tokenu z tej bezpłatnej usługi. Zobacz [CoreOS dokumentacji](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) więcej szczegółów.
6. Modyfikowanie hello **config.yaml chmury** pliku istniejących hello tooreplace **odnajdywania** tokenu z hello nowy token:
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. Modyfikowanie hello **parameters.JSON następującym kodem azuredeploy** plik: hello Otwórz certyfikat został utworzony w kroku 4 w edytorze tekstów. Skopiuj cały tekst między `----BEGIN CERTIFICATE-----` i `-----END CERTIFICATE-----` do hello **sshKeyData** parametr (należy tooremove wszystkie znaki nowego wiersza).
8. Modyfikowanie hello **newStorageAccountName** parametru. To konto magazynu hello dysków systemu operacyjnego maszyny Wirtualnej. Ta nazwa konta została toobe globalnie unikatowe.
9. Modyfikowanie hello **publicDomainName** parametru. Będzie to część nazwy DNS hello skojarzone z adresem IP publiczny moduł równoważenia obciążenia hello. Witaj FQDN końcowego ma hello format *[wartość tego parametru]*. *kolumny [region]* . cloudapp.azure.com. Na przykład jeśli określono nazwę hello jako deishbai32 i hello grupa zasobów jest wdrożony toohello regionu zachodnie stany USA, a następnie hello końcowego FQDN tooyour będzie usługa równoważenia obciążenia deishbai32.westus.cloudapp.azure.com.
10. Zapisz plik parametru hello. A następnie można udostępnić hello klastra przy użyciu programu Azure PowerShell:
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    lub interfejsu wiersza polecenia platformy Azure:
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. Po zainicjowaniu obsługi hello grupy zasobów, można wyświetlić wszystkie zasoby hello w grupie hello na klasycznego portalu Azure. Jak pokazano w hello następującego zrzutu ekranu, hello grupa zasobów zawiera sieć wirtualną z trzech maszyn wirtualnych, które są przyłączone do toohello tego samego zestawu dostępności. Grupa Hello zawiera również modułu równoważenia obciążenia, który ma skojarzone publicznego adresu IP.
    
    ![Grupa zasobów elastycznie Hello w klasycznym portalu Azure](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a>Instalowanie powitania klienta
Należy **deisctl** toocontrol Twojego Deis klastra. Chociaż deisctl jest automatycznie zainstalowane we wszystkich węzłach klastra hello, jest dobrym rozwiązaniem deisctl toouse na osobnym komputerze administracyjnych. Ponadto ponieważ wszystkie węzły są skonfigurowane przy użyciu tylko prywatnych adresów IP, należy toouse tunelowanie SSH za pośrednictwem usługi równoważenia obciążenia hello, który ma publicznego adresu IP, tooconnect toohello węzła maszyny. Witaj poniżej przedstawiono kroki hello konfigurowania deisctl na oddzielnych Ubuntu fizyczne lub maszyny wirtualnej.

1. Deis deisctl:mkdir instalacji
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. Dodaj agenta toossh klucza prywatnego:
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. Skonfiguruj deisctl:
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

Witaj szablon definiuje reguły NAT ruchu przychodzącego, które mapują 2223 tooinstance 1, 2224 tooinstance 2 i 2225 tooinstance 3. Za pomocą narzędzia deisctl hello zapewnia nadmiarowość. Można sprawdzić te reguły w klasycznym portalu Azure:

![Reguły NAT modułu równoważenia obciążenia hello](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> Obecnie hello szablon obsługuje tylko klastry węzłów 3. Jest to spowodowane ograniczenia w szablonie usługi Azure Resource Manager definicję reguły NAT, które nie obsługują pętli składni.
> 
> 

## <a name="install-and-start-hello-deis-platform"></a>Zainstaluj i uruchom hello Deis platformy
Teraz można używać deisctl tooinstall i rozpocząć hello Deis platformy:

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> Początkowy platformy hello zajmie trochę czasu (jak 10 minut). Szczególnie uruchamianie usługi konstruktora hello może zająć dużo czasu. Czasami zajmuje kilka prób toosucceed: Jeśli operacja hello toohang, spróbuj wpisać `ctrl+c` toobreak wykonanie polecenia hello i spróbuj ponownie.
> 
> 

Można użyć `deisctl list` tooverify, jeśli wszystkie usługi są uruchomione:

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

Gratulacje! Teraz już wiem uruchomionej Deis clsuter na platformie Azure! Następnie umożliwia wdrożenie przykładowego Przejdź aplikacji toosee hello klastra w akcji.

## <a name="deploy-and-scale-a-hello-world-application"></a>Wdrażanie i skalowanie aplikacji Hello World
Witaj poniższej procedurze pokazano, jak toodeploy "Hello World" Przejdź klastra toohello aplikacji. kroki Hello są oparte na [Deis dokumentacji](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).

1. Dla routingu toowork siatki hello prawidłowo, należy toohave rekord A symboli wieloznacznych dla domeny wskazuje toohello publicznego adresu IP usługi równoważenia obciążenia hello. Witaj Poniższy zrzut ekranu przedstawia hello A rekord rejestracji domen przykładowe na GoDaddy:
   
    ![Rekord GoDaddy A](./media/deis-cluster/go-daddy.png)
   
   <p />
2. Deis instalacji:
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. Utwórz nowy klucz SSH, a następnie dodaj tooGitHub klucza publicznego hello (oczywiście można również wykorzystać istniejące klucze). toocreate nową parę kluczy SSH, należy użyć:
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. Dodaj id_rsa.pub lub klucza publicznego hello wybranych tooGitHub. Można to zrobić za pomocą hello dodać SSH klucza przycisku w ekranie konfiguracji klucze SSH:
   
   ![Klucz usługi GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. Zarejestruj nowego użytkownika:
   
        deis register http://deis.[your domain]
   <p />
6. Dodaj klucz SSH hello:
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. Tworzenie aplikacji.
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p />
8.Witaj git wypychania wyzwoli toobe obrazów Docker wbudowany i wdrożeniu, którego może potrwać kilka minut. Moje doświadczeniu czasami kroku 10 (Pushing obrazu tooprivate repozytorium) mogą wykraczać. W takim przypadku można zatrzymać procesu hello przy użyciu aplikacji hello Usuń "deis aplikacji: zniszczyć <application name> ` tooremove hello application and try again. You can use `deis apps:list" toofind limit hello nazwę aplikacji. Jeśli wszystko działa powinny być widoczne przypominać następujące hello na końcu hello dane wyjściowe poleceń:
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. Sprawdź, czy aplikacja hello działa:
   
        curl -S http://[your application name].[your domain]
   Powinien zostać wyświetlony następujący ekran:
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. Skala wystąpień too3 aplikacji hello:
    
        deis scale cmd=3
    <p />
11. Opcjonalnie można użyć deis szczegóły tooexamine informacje o aplikacji. Witaj następujące dane wyjściowe są z mojej wdrożenia aplikacji:
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a>Następne kroki
W tym artykule udał za pośrednictwem wszystkich tooprovision kroki hello Deis nowy klaster na platformie Azure przy użyciu szablonu usługi Azure Resource Manager. Szablon Hello obsługuje nadmiarowości w narzędzi połączeń, a także równoważenie obciążenia dla wdrożonych aplikacji. Szablon Hello unika również na węzeł elementu członkowskiego, które zapisuje cenne zasoby publicznych adresów IP i zapewnia bardziej zabezpieczonym środowisku toohost aplikacji przy użyciu publicznych adresów IP. toolearn więcej, zobacz następujące artykuły hello:

[Omówienie usługi Azure Resource Manager][resource-group-overview]  
[Jak toouse hello wiersza polecenia platformy Azure][azure-command-line-tools]  
[Używanie programu Azure PowerShell z usługą Azure Resource Manager][powershell-azure-resource-manager]  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
