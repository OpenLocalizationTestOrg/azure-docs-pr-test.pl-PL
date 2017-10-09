Rozwiązania w chmurze platformy Azure są oparte na maszynach wirtualnych (emulacja fizycznego sprzętu komputerowego), co umożliwia elastyczne tworzenie pakietów wdrożeń oprogramowania oraz lepszą konsolidację zasobów niż w przypadku sprzętu fizycznego. [Docker](https://www.docker.com) kontenery i hello ekosystem docker ma sposobów hello znacznie rozszerzonej mogą tworzyć, wysyłki i zarządzanie oprogramowaniem rozproszonych. Kod aplikacji w kontenerze jest odizolowana od hello hosta maszyny Wirtualnej i innych kontenerów na hello tej samej maszyny Wirtualnej. Izolacja zapewnia większą elastyczność projektowania i wdrażania.

Platforma Azure oferuje następujące wartości Docker hello:

* [Wiele](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) [różnych](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate sposobów Docker obsługuje dla kontenerów toosuit sytuacji
* Witaj [usługi kontenera platformy Azure](https://azure.microsoft.com/documentation/services/container-service/) tworzy klastry hostów kontenera przy użyciu orchestrators, takich jak **marathon** i **swarm**.
* [Usługa Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md) i [Szablony grupy zasobów](../articles/resource-group-authoring-templates.md) toosimplify wdrażania i aktualizowania złożonych aplikacji rozproszonych
* integracja z wieloma narzędziami do zarządzania konfiguracją, zarówno własnymi, jak i typu „open source”

I dlatego programowego można utworzyć maszyny wirtualne i Linux kontenerów na platformie Azure, można również użyć maszyny Wirtualnej, a kontener *aranżacji* narzędzi grup toocreate maszynach wirtualnych (VM) i aplikacje toodeploy wewnątrz zarówno systemu Linux kontenery i teraz [kontenery Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

W tym artykule omówiono nie tylko te pojęcia na wysokim poziomie, zawiera także tonach łączy toomore informacje, samouczki, i produkty związane z użyciem toocontainer i klaster na platformie Azure. Jeśli znasz wszystko to i po prostu chcesz hello łącza, są one tutaj na [narzędzia do pracy z kontenerami](#tools-for-working-with-azure-vms-and-containers).

## <a name="hello-difference-between-virtual-machines-and-containers"></a>Witaj różnica między maszynami wirtualnymi i kontenerów
Maszyny wirtualne działają w izolowanym środowisku wirtualizacji sprzętowej udostępnianym przez [funkcję hypervisor](http://en.wikipedia.org/wiki/Hypervisor). Na platformie Azure hello [maszyn wirtualnych](https://azure.microsoft.com/services/virtual-machines/) wszystkie te usługi uchwytów dla Ciebie: Tworzenie maszyn wirtualnych przez wybranie hello systemu operacyjnego i konfigurowanie &mdash;lub przekazując niestandardowego obrazu maszyny Wirtualnej. Maszyny wirtualne są technologii sprawdzona, "wzmocnione zabezpieczenia bitwy", a istnieje wiele narzędzi dostępnych toomanage hello systemu operacyjnego i aplikacji zawierają.  Aplikacje na maszynie wirtualnej są ukryte przed hello hosta systemu operacyjnego. Z hello punktu widzenia aplikacji lub użytkownika na maszynie Wirtualnej hello wirtualna pojawia się toobe autonomicznego komputera fizycznego.

[Kontenery Linux](http://en.wikipedia.org/wiki/LXC) i nie używaj te tworzone i hostowane przy użyciu narzędzia docker izolacji tooprovide funkcji hypervisor. Z kontenerami host kontenera hello używa procesu i funkcji izolacji system plików hello Linux jądra tooexpose toohello kontenera, jego aplikacji, niektóre funkcje jądra i swój własny system plików izolowanym. Z hello punktu widzenia aplikacji uruchomionych w kontenerze kontener hello jest wyświetlany toobe unikatowe wystąpienie systemu operacyjnego. Dla zawartej aplikacji nie są widoczne znajdujące się poza jej kontenerem procesy ani inne zasoby.

W kontenerze platformy Docker jest używanych znacznie mniej zasobów niż w przypadku maszyny wirtualnej. Kontenery docker stosować aplikacji izolacji i wykonywanie modelu, który nie udostępnia jądra hello hello Docker hosta. Witaj kontener ma znacznie niższe wpływ dysku, ponieważ nie ma wśród nich hello całego systemu operacyjnego. Czas uruchamiania jest znacznie krótszy, a ilość wymaganego miejsca na dysku znacznie mniejsza niż w przypadku maszyny wirtualnej.
Kontenery systemu Windows Podaj hello same zalety jako kontenery systemu Linux dla aplikacji uruchomionych w systemie Windows. Kontenery systemu Windows obsługuje format obrazu hello Docker i interfejsu API Docker, ale ich mogą być zarządzane przy użyciu programu PowerShell. W przypadku kontenerów systemu Windows dostępne są dwa środowiska uruchomieniowe — kontenery systemu Windows Server i kontenery funkcji Hyper-V. Kontenery funkcji Hyper-V zapewniają dodatkową warstwę izolacji dzięki hostowaniu każdego kontenera na wysoce zoptymalizowanej maszynie wirtualnej. więcej informacji na temat kontenery systemu Windows, zobacz toolearn [o kontenery Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview). tooget wprowadzenie kontenery systemu Windows na platformie Azure, Dowiedz się, jak za[wdrażanie klastra usługi kontenera platformy Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).

## <a name="what-are-containers-good-for"></a>Dla jakich zastosowań dobre są kontenery?

Kontenery mogą poprawić:

* Kod aplikacji Hello szybkości może być opracowane i udostępnionych powszechnie
* szybkość Hello i gwarancją można przetestować aplikację
* szybkość Hello i zaufania, które można wdrożyć aplikację

Kontenery działają na hoście kontenera, czyli w ramach systemu operacyjnego, co na platformie Azure oznacza maszynę wirtualną Azure Virtual Machines. Nawet jeśli lubisz pomysł hello kontenerów, nadal będzie tooneed infrastruktury maszyny Wirtualnej, hosting hello kontenerów, ale korzyści hello są kontenerami interesują w przypadku których maszyny Wirtualnej są na nich uruchomione (mimo tego, czy kontener hello chce Linux lub Windows środowisko wykonawcze będzie ważne, na przykład).


## <a name="what-are-containers-good-for"></a>Dla jakich zastosowań dobre są kontenery?
Są one bardzo wiele zastosowań, ale ich zachęca&mdash;jak [usługi w chmurze Azure](https://azure.microsoft.com/services/cloud-services/) i [sieć szkieletowa usług Azure](../articles/service-fabric/service-fabric-overview.md)&mdash;hello tworzenia pojedynczej usługi, zorientowane na mikrousługi aplikacje rozproszone, w której aplikacji projektu jest oparta na wielu części małe, która zezwala na składanie, a nie na składnikach większych i bardziej silnie sprzężonego.

Jest to szczególnie zalecane w środowiskach chmur publicznych, takich jak platforma Azure, w których maszyny wirtualne są wynajmowane i uruchamiane zgodnie z potrzebami. Nie tylko pozwala to uzyskać izolację i dostęp do narzędzi służących do szybkiego wdrażania i aranżowania, ale także pozwala podejmować bardziej efektywne decyzje dotyczące infrastruktury aplikacji.

Na przykład użytkownik może posiadać aktualnie wdrożenie składające się z 9 dużych maszyn wirtualnych platformy Azure na potrzeby aplikacji rozproszonej o wysokiej dostępności. Jeśli hello składniki tej aplikacji można wdrożyć w kontenerach, może być możliwe toouse tylko 4 maszyn wirtualnych i wdrożyć składniki aplikacji wewnątrz 20 kontenery nadmiarowość i równoważenie obciążenia.

Jest to po prostu przykład, ale jeśli w danym scenariuszu można to zrobić, można dostosować nagłego toousage więcej kontenerów, a nie więcej maszyn wirtualnych platformy Azure i używać hello bardziej wydajne niż wcześniej pozostałych całkowite obciążenie procesora CPU.

Ponadto istnieje wiele scenariuszy, które nie nadają się podejście mikrousług tooa; najlepiej będzie wiadomo, czy mikrousług i kontenery pomoże.

### <a name="container-benefits-for-developers"></a>Korzyści dla deweloperów wynikające z korzystania z kontenerów
Ogólnie rzecz biorąc jest łatwe toosee technologii kontenera jest krokiem do przodu, że istnieją również korzyści bardziej szczegółowych. Spójrzmy przykład Witaj kontenerów Docker. Ten temat zostanie nie Poznaj głęboko Docker od razu (odczytu [co to jest Docker?](https://www.docker.com/whatisdocker/) dla tego scenariusza, lub [wikipedia](http://wikipedia.org/wiki/Docker_%28software%29)), ale Docker i jej ekosystemu oferują ogromne korzyści tooboth deweloperzy i IT specjalistom ds.

Deweloperzy wykonać kontenery tooDocker szybko, ponieważ przede wszystkim pozwala kontenery systemu Linux i Windows za pomocą łatwo:

* Można użyć polecenia proste, przyrostowe toocreate środka obrazu, który jest łatwo toodeploy i można zautomatyzować tworzenie tych obrazów za pomocą plik dockerfile
* Mogą współużytkować tych obrazów za pomocą prostego, [git](https://git-scm.com/)— styl wypychania i ściągania polecenia zbyt[publicznego](https://registry.hub.docker.com/) lub [rejestrów prywatnej docker](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Możliwe jest działanie w kategoriach izolowanych składników aplikacji, a nie komputerów.
* Możliwe jest używanie wielu narzędzi, które współpracują z kontenerami platformy Docker i różnymi obrazami podstawowymi.

### <a name="container-benefits-for-operations-and-it-professionals"></a>Korzyści dla specjalistów ds. operacyjnych i informatyków wynikające z korzystania z kontenerów
IT i specjalistów operacji również korzystać z kombinacji hello kontenery i maszyn wirtualnych.

* Zawarte usługi są odizolowane od środowiska wykonywania hosta maszyny wirtualnej.
* Zawarty kod jest identyczny i możliwe jest tego sprawdzenie.
* Zawarte usługi można szybko uruchomić, zatrzymać oraz przenieść między środowiskiem programistycznym, testowym i produkcyjnym.

Funkcje, takie jak te&mdash;i istnieje więcej&mdash;wzbudzania ustalonych firmy, gdzie informacje specjalistów technologii organizacje mają zadania hello dopasowywania zasobów&mdash;tym mocy obliczeniowej czysty&mdash; toonot wymagane zadania toohello tylko pozostanie w firmie, ale bardziej zadowoleni i uzyskać dostęp. Małych firm, niezależnym dostawcom oprogramowania i uruchomienia mają dokładnie hello sam wymóg, ale może być zawiera jego opis inaczej.

## <a name="what-are-virtual-machines-good-for"></a>Dla jakich zastosowań dobre są maszyny wirtualne?
Maszyny wirtualne Podaj szkieletu hello rozwiązań w chmurze, a które nie zmieniają się. Jeśli maszyny wirtualne uruchamia wolniej, mają większy wpływ dysku, a nie mapują bezpośrednio tooa mikrousług architektury, mają bardzo istotne zalety:

1. Domyślnie mają one bardziej niezawodne zabezpieczenia dla komputera hosta.
2. Obsługują wszystkie główne konfiguracje systemów operacyjnych i aplikacji.
3. Mają one stałe ekosystemy narzędzi na potrzeby poleceń i kontroli.
4. Udostępniają one wykonywania hello kontenery toohost środowiska

ostatni element Hello jest ważne, ponieważ zawartych w niej aplikacji nadal wymaga określonego systemu operacyjnego i typ procesora CPU, w zależności od wywołania hello, który spowoduje, że aplikacja hello. Jest ważne tooremember zainstalować kontenerów na maszynach wirtualnych, ponieważ zawierają one aplikacji hello mają toodeploy; kontenery nie są elementy zastępcze maszyn wirtualnych lub systemów operacyjnych.

## <a name="high-level-feature-comparison-of-vms-and-containers"></a>Ogólne porównanie funkcji maszyn wirtualnych i kontenerów
Hello poniższej tabeli przedstawiono bardzo duże różnice rodzaj hello poziomu funkcji, która&mdash;bez dużo pracy dodatkowe&mdash;istnieje między maszynami wirtualnymi i Linux kontenerów. Należy pamiętać, że niektóre funkcje może być mniej lub bardziej pożądane w zależności od własnej aplikacji musi i że podobnie jak w przypadku każdego oprogramowania, dodatkowej pracy zawiera zwiększyć obsługę funkcji, szczególnie w obszarze hello zabezpieczeń.

| Funkcja | Maszyny wirtualne | Kontenery |
|:--- | --- | --- |
| „Domyślna” obsługa zabezpieczeń |lepszej tooa |tooa nieco mniejszym stopniu |
| Wymagane miejsce na dysku |Cały system operacyjny oraz aplikacje |Tylko zgodnie z wymaganiami aplikacji |
| Czas trwania toostart w |Znacznie dłuższy: rozruch systemu operacyjnego oraz ładowanie aplikacji |Znacznie krótszy: tylko aplikacje muszą toostart, ponieważ jądra jest już uruchomiona. |
| Przenośność |Przenośne przy odpowiednim przygotowaniu |Przenośne w formacie obrazu; zwykle mniejsza |
| Automatyzacja obrazu |Różni się w zależności od systemu operacyjnego i aplikacji |[Rejestr platformy Docker](https://registry.hub.docker.com/); inne |

## <a name="creating-and-managing-groups-of-vms-and-containers"></a>Tworzenie grup maszyn wirtualnych oraz kontenerów i zarządzanie nimi
W tym momencie każdy architekt, deweloper lub specjalista ds. operacji IT może pomyśleć: „Mogę zautomatyzować to wszystko; jest to po prostu centrum danych jako usługa”.

Masz prawo, można go oraz czy dowolnej liczby, z których wiele może być używany, można albo Zarządzaj grupami maszyn wirtualnych platformy Azure i systemów wstrzyknięcia kodu niestandardowego, skryptów, często z hello [CustomScriptingExtension dla systemu Windows](https://msdn.microsoft.com/library/azure/dn781373.aspx) lub Witaj [CustomScriptingExtension dla systemu Linux](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/). Można (i zapewne zostało to już zrobione) zautomatyzować wdrożenia platformy Azure za pomocą skryptów programu PowerShell lub interfejsu wiersza polecenia platformy Azure.

Te możliwości są często, a następnie tootools zmigrowane, takich jak [Puppet](https://puppetlabs.com/) i [Chef](https://www.chef.io/) tooautomate hello tworzenie i konfiguracja dla maszyn wirtualnych na dużą skalę. (W tym miejscu są zbyt niektóre łącza[za pomocą tych narzędzi z platformy Azure,](#tools-for-working-with-containers).)

### <a name="azure-resource-group-templates"></a>Szablony grupy zasobów platformy Azure
Niedawno, Azure wydane hello [zarządzania zasobami Azure](../articles/resource-manager-deployment-model.md) interfejsu API REST i zaktualizowane toouse narzędzia programu PowerShell i interfejsu wiersza polecenia Azure go łatwo. Można wdrożyć, zmodyfikować lub ponownie wdrożyć topologii całej aplikacji za pomocą [szablonów usługi Azure Resource Manager](../articles/resource-group-authoring-templates.md) z przy użyciu interfejsu API zarządzania zasobów platformy Azure hello:

* Witaj [portalu Azure za pomocą szablonów](https://github.com/Azure/azure-quickstart-templates)&mdash;wskazówki, użyj przycisku "DeployToAzure" hello
* Witaj [wiersza polecenia platformy Azure](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="deployment-and-management-of-entire-groups-of-azure-vms-and-containers"></a>Wdrażanie całych grup maszyn wirtualnych platformy Azure i kontenerów oraz zarządzanie nimi
Istnieje kilka popularnych systemów, w ramach których można wdrożyć całe grupy maszyn wirtualnych i zainstalować platformę Docker (lub inne systemy hosta kontenera systemu Linux) jako grupę możliwą do zautomatyzowania. Dla bezpośrednich łączy, zobacz hello [kontenery i narzędzia](#containers-and-vm-technologies) sekcji poniżej. Istnieje kilka systemów, które wykonują takim tooa mniejszej lub większej, a ta lista nie jest pełna. W zależności od potrzeb i posiadanych umiejętności mogą być one przydatne.

Na platformie Docker dostępny jest zestaw narzędzi do tworzenia maszyn wirtualnych ([docker-machine](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) oraz narzędzie do zarządzania klastrem kontenera platformy Docker w celu równoważenia obciążenia ([swarm](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Ponadto hello [rozszerzenia maszyny Wirtualnej Azure Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) jest dostarczany z domyślną obsługę [ `docker-compose` ](https://docs.docker.com/compose/), które można wdrożyć skonfigurowane kontenery aplikacji w ramach wielu kontenerów.

Ponadto można wypróbować [system Data Center Operating System (DCOS) firmy Mesosphere](http://docs.mesosphere.com). DCOS opiera się na powitania open source [mesos](http://mesos.apache.org/) "systemów rozproszonych jądra", która umożliwia tootreat możesz centrum danych jako jedna usługa adresowanego. System DCOS zawiera wbudowane pakiety dla kilku ważnych systemów, takie jak [Spark](http://spark.apache.org/) i [Kafka](http://kafka.apache.org/) (oraz inne), a także wbudowane usługi, takie jak [Marathon](https://mesosphere.github.io/marathon/) (system kontroli kontenera) i [Chronos](https://mesos.github.io/chronos/) (rozproszony program planujący). Rozwiązanie Mesos zostało utworzone między innymi na podstawie doświadczeń firm z branży sieci Web odpowiedzialnych za serwisy Twitter i AirBnb. Można również użyć **swarm** jako hello przez aparat aranżacji.

Oprócz tego [kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/) to system typu „open source” służący do zarządzania maszynami wirtualnymi i kontenerami utworzony na podstawie doświadczeń firmy Google. Można również użyć [kubernetes z fale obsługi sieci tooprovide](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave).

[Deis](http://deis.io/overview/) jest otwarty źródła "Platforma jako — usługa" (PaaS), dzięki którym łatwe toodeploy aplikacji i zarządzanie nimi na własnych serwerach. Deis kompilacji na Docker i CoreOS tooprovide lekkie PaaS inspirowana Heroku przepływu pracy.

W systemie [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html), czyli dystrybucji systemu Linux ze zoptymalizowaną zajmowaną przestrzenią dyskową, obsługą platformy Docker i własnym systemem kontenerów o nazwie [rkt](https://github.com/coreos/rkt), również istnieje narzędzie do zarządzania grupami kontenerów o nazwie [fleet](https://coreos.com/fleet/docs/latest/).

Ubuntu, inna bardzo popularna dystrybucja systemu Linux, również obsługuje platformę Docker, ale także obsługuje [klastry systemu Linux (typu LXC)](https://help.ubuntu.com/lts/serverguide/lxc.html).

## <a name="tools-for-working-with-azure-vms-and-containers"></a>Narzędzia do pracy z maszynami wirtualnymi platformy Azure i kontenerami
Podczas pracy z kontenerami i maszynami wirtualnymi platformy Azure używane są narzędzia. Ta sekcja zawiera listę tylko niektóre hello najbardziej przydatne lub ważne pojęcia i narzędzia o kontenerów, grupy i hello większych konfiguracji i aranżacji używane z nimi.

> [!NOTE]
> Ten obszar jest zmiana zdumiewająco szybko i gdy wykonamy nasze najlepsze tookeep ten temat i jego łączy się toodate również może być niemożliwe zadań. Upewnij się, że wyszukiwania na interesujące tookeep tematów w górę toodate!
>
>

### <a name="containers-and-vm-technologies"></a>Technologie dotyczące kontenerów i maszyn wirtualnych
Niektóre technologie dotyczące kontenerów systemu Linux:

* [Docker](https://www.docker.com)
* [LXC](https://linuxcontainers.org/)
* [CoreOS i rkt](https://github.com/coreos/rkt)
* [Projekt Open Container](http://opencontainers.org/)
* [RancherOS](http://rancher.com/rancher-os/)

Linki dotyczące kontenerów systemu Windows:

* [Kontenery systemu Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)

Linki dotyczące platformy Docker programu Visual Studio:

* [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/core/docker/visual-studio-tools-for-docker)

Narzędzia platformy Docker:

* [Demon platformy Docker](https://docs.docker.com/installation/#installation)
* Klienci platformy Docker
  * [Klient platformy Docker systemu Windows w ramach narzędzia Chocolatey](https://chocolatey.org/packages/docker)
  * [Instrukcje dotyczące instalacji platformy Docker](https://docs.docker.com/installation/#installation)

Platforma Docker na platformie Microsoft Azure:

* [Rozszerzenie maszyny wirtualnej platformy Docker dla systemu Linux na platformie Azure](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Podręcznik użytkownika rozszerzenia maszyny wirtualnej platformy Docker platformy Azure](https://github.com/Azure/azure-docker-extension/blob/master/README.md)
* [Przy użyciu hello Docker rozszerzenia maszyny Wirtualnej z hello interfejsu wiersza polecenia platformy Azure (Azure CLI)](../articles/virtual-machines/linux/classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Przy użyciu hello Docker rozszerzenia maszyny Wirtualnej z hello portalu Azure](../articles/virtual-machines/linux/classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Jak toouse komputera docker na platformie Azure](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Jak toouse docker z swarm na platformie Azure](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Wprowadzenie do platformy Docker i narzędzia Compose na platformie Azure](../articles/virtual-machines/linux/docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Przy użyciu toocreate szablonu grupy zasobów platformy Azure hostów Docker na platformie Azure szybko](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)
* [Witaj wbudowaną obsługę `compose` ](https://github.com/Azure/azure-docker-extension#11-public-configuration-keys) zawartych w niej aplikacji
* [Implementowanie prywatnego rejestru platformy Docker na platformie Azure](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Dystrybucje systemu Linux i przykłady związane z platformą Azure:

* [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)

Konfiguracja, zarządzanie klastrami i aranżacja kontenerów:

* [Narzędzie Fleet w systemie CoreOS](https://coreos.com/fleet/docs/latest/)
* Deis

  * [Ukończenie wdrożenia klastra Kubernetes tooautomated przewodnik CoreOS i splot](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
  * [Kubernetes Visualizer](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Mesos](http://mesos.apache.org/)

  * [System Data Center Operating System (DCOS) firmy Mesosphere](https://docs.mesosphere.com/1.7/overview/design/azure-container-service/)
* [Jenkins](https://jenkins.io/) i [Hudson](http://hudson-ci.org/)

  * [Wtyczka agenta maszyny wirtualnej rozwiązania Jenkins dla platformy Azure](https://wiki.jenkins.io/display/JENKINS/Azure+VM+Agents+plugin)
  * [Repozytorium GitHub: Wtyczka magazynu rozwiązania Jenkins dla platformy Azure](https://github.com/jenkinsci/windows-azure-storage-plugin)
  * [Inna firma: Wtyczka podrzędna rozwiązania Hudson dla platformy Azure](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
  * [Inna firma: Wtyczka magazynu rozwiązania Hudson dla platformy Azure](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Azure Automation](https://azure.microsoft.com/services/automation/)

  * [Wideo: Jak tooUse usługi Automatyzacja Azure z maszyn wirtualnych systemu Linux](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* Rozszerzenie DSC programu PowerShell dla systemu Linux

  * [Blog: Jak toodo DSC środowiska Powershell dla systemu Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
  * [GitHub: Rozszerzenie DSC klienta platformy Docker](https://github.com/anweiss/DockerClientDSC)

## <a name="next-steps"></a>Następne kroki
Zapoznaj się z platformą [Docker](https://www.docker.com) i [kontenerami systemu Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

<!--Anchors-->
[microservices]: http://martinfowler.com/articles/microservices.html
[microservice]: http://martinfowler.com/articles/microservices.html
<!--Image references-->
