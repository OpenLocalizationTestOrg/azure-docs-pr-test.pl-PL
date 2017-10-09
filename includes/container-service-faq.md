# <a name="container-service-frequently-asked-questions"></a>Często zadawane pytania dotyczące usługi Container Service

## <a name="orchestrators"></a>Koordynatorzy

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>Których koordynatorów kontenerów obsługuje usługa Azure Container Service? 

Obsługiwane są następujące usługi typu open source: DC/OS, Docker Swarm i Kubernetes. Aby uzyskać więcej informacji, zobacz hello [omówienie](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
 
### <a name="do-you-support-docker-swarm-mode"></a>Czy tryb Docker Swarm jest obsługiwany? 

Obecnie tryb Swarm nie jest obsługiwany, ale nie znajduje się na plan usługi hello. 

### <a name="does-azure-container-service-support-windows-containers"></a>Czy usługa Azure Container Service obsługuje kontenery z systemem Windows?  

Obecnie kontenery systemu Linux są obsługiwane przy użyciu wszystkich koordynatorów. Obsługa kontenerów systemu Windows przy użyciu usługi Kubernetes jest dostępna w wersji zapoznawczej.

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>Czy zalecane jest korzystanie z określonego koordynatora w usłudze Azure Container Service? 
Ogólnie nie zalecamy korzystania z określonego koordynatora. Jeśli masz doświadczenie z jednym orchestrators hello obsługiwane, należy zastosować środowiska usługi kontenera platformy Azure. Trendy danych sugerują jednak, że platforma DC/OS została sprawdzona podczas produkcji w przypadku obciążeń danych Big Data i IoT, usługa Kubernetes jest dobrym rozwiązaniem w przypadku natywnych obciążeń w chmurze, a usługa Docker Swarm jest znana z możliwości integrowania z narzędziami Docker oraz prostego procesu uczenia się.

W zależności od swojego scenariusza możesz również kompilować niestandardowe rozwiązania kontenerów i zarządzać nimi przy użyciu innych usług Azure. Usługi te to: [Virtual Machines](../articles/virtual-machines/linux/overview.md), [Service Fabric](../articles/service-fabric/service-fabric-overview.md), [Web Apps](../articles/app-service-web/app-service-web-overview.md) i [Batch](../articles/batch/batch-technical-overview.md).  

### <a name="what-is-hello-difference-between-azure-container-service-and-acs-engine"></a>Co to jest hello różnica między aparatu ACS i usługi kontenera platformy Azure? 
Usługa kontenera platformy Azure to usługa Azure kopii umowy dotyczącej poziomu usług z funkcjami w hello portalu Azure, narzędzi wiersza polecenia platformy Azure i interfejsów API usługi Azure. Usługa Hello umożliwia wdrożenie tooquickly i zarządzania klastrami uruchamiania narzędzi orchestration standardowe kontenera o stosunkowo małej liczby opcji konfiguracji. 

[Aparat ACS](http://github.com/Azure/acs-engine) to projekt open source, który umożliwia użytkownikom toocustomize hello klastra konfiguracji na każdym poziomie. Tej możliwości tooalter hello konfiguracji infrastruktury i oprogramowania oznacza oferujemy nie umowy SLA dla aparatu ACS. Obsługa odbywa się za pośrednictwem projektu open source hello w witrynie GitHub, a nie za pomocą oficjalnego kanały firmy Microsoft. 

## <a name="cluster-management"></a>Zarządzanie klastrami

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>Jak mogę utworzyć klucze SSH dla mojego klastra?

Standardowe narzędzia można użyć na toocreate Twojego systemu operacyjnego SSH publicznego i prywatnego pary kluczy RSA do uwierzytelniania względem maszyn wirtualnych systemu Linux hello dla klastra. Aby uzyskać instrukcje, zobacz hello [OS X i Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) lub [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) wskazówki. 

Jeśli używasz [poleceń Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy w kontenerze usługi klastrowania, SSH klucze mogą być generowane automatycznie dla klastra.

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>Jak mogę utworzyć nazwę główną usługi dla mojego klastra Kubernetes?

Identyfikator podmiotu zabezpieczeń usługi Azure Active Directory i hasło są również wymagane toocreate Kubernetes klastra usługi kontenera platformy Azure. Aby uzyskać więcej informacji, zobacz [o hello nazwy głównej usługi dla klastra Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-service-principal.md).

Jeśli używasz [poleceń Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy Kubernetes, usługa klastrowania poświadczenia główne mogą być generowane automatycznie dla klastra.

### <a name="how-large-a-cluster-can-i-create"></a>Jak duży klaster mogę utworzyć?
Możesz utworzyć klaster z 1, 3 lub 5 węzłami głównymi. Możesz się too100 agenta węzłów.

> [!IMPORTANT]
> W przypadku większych klastrów i w zależności od hello rozmiar maszyny Wirtualnej, wybranych dla węzłów może być konieczne przydziału rdzeni hello tooincrease w ramach subskrypcji. toorequest zwiększenia limitu przydziału, otwórz [żądania obsługi online klienta](../articles/azure-supportability/how-to-create-azure-support-request.md) bez dodatkowych opłat. Jeśli używasz [bezpłatnego konta platformy Azure](https://azure.microsoft.com/free/), możesz użyć ograniczonej liczby rdzeni obliczeniowych platformy Azure.
> 

### <a name="how-do-i-increase-hello-number-of-masters-after-a-cluster-is-created"></a>Jak zwiększyć hello liczba wzorców, po utworzeniu klastra? 
Po utworzeniu klastra hello hello liczba wzorców jest stała i nie można zmienić. Podczas tworzenia hello hello klastra należy wybrać w idealnym przypadku wielu wzorców wysokiej dostępności.

### <a name="how-do-i-increase-hello-number-of-agents-after-a-cluster-is-created"></a>Jak zwiększyć hello liczby agentów, po utworzeniu klastra? 
Witaj liczby agentów można skalować w klastrze hello przy użyciu portalu Azure hello lub narzędzia wiersza polecenia. Zobacz [Scale an Azure Container Service cluster](../articles/container-service/kubernetes/container-service-scale.md) (Skalowanie klastra usługi Azure Container Service).

### <a name="what-are-hello-urls-of-my-masters-and-agents"></a>Co to są adresy URL hello wzorców i agentów? 
adresy URL klastra, który zasobów w usłudze kontenera platformy Azure są oparte na powitania Hello prefiks dostarczania i hello nazwa hello region platformy Azure, którą wybrano dla wdrożenia nazw DNS. Na przykład hello pełną nazwę domeny (FQDN) głównego węzła hello jest formularza:

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

Często używane adresy URL można znaleźć klastra hello portalu Azure, hello Eksploratora zasobów Azure lub innych narzędzi platformy Azure.

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a>Jak sprawdzić, która wersja koordynatora jest uruchamiana w moim klastrze?

* DC/OS: Zobacz hello [dokumentację Mesosphere](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)
* Docker Swarm: uruchom polecenie `docker version`
* Kubernetes: uruchom polecenie `kubectl version`

### <a name="how-do-i-upgrade-hello-orchestrator-after-deployment"></a>Jak uaktualnić hello orchestrator po wdrożeniu?

Obecnie usługi kontenera platformy Azure nie zapewnia narzędzia tooupgrade hello wersji hello orchestrator, wdrożone w klastrze. Jeśli usługa Container Service obsługuje nowszą wersję, można wdrożyć nowy klaster. Innym rozwiązaniem jest toouse narzędzia specyficzne dla programu orchestrator, jeśli są one dostępne tooupgrade klastra w miejscu. Na przykład zobacz [DC/OS Upgrading](https://dcos.io/docs/1.8/administration/upgrading/) (Uaktualnianie rozwiązania DC/OS).
 
### <a name="where-do-i-find-hello-ssh-connection-string-toomy-cluster"></a>Gdzie znaleźć hello SSH połączenia ciąg toomy klastra?

Parametry połączenia hello można znaleźć w portalu Azure hello lub za pomocą narzędzi wiersza polecenia platformy Azure. 

1. W portalu hello Przejdź toohello grupy zasobów dla wdrożenia klastra hello.  

2. Kliknij przycisk **omówienie** i kliknij łącze hello **wdrożeń** w obszarze **Essentials**. 

3. W hello **historii wdrożenia** bloku, kliknij przycisk hello wdrożenia, który zaczyna się od nazwy **microsoft acs** następuje data wdrożenia. Przykład: microsoft-acs-201701310000.  

4. Na powitania **Podsumowanie** w obszarze **dane wyjściowe**, zostały podane kilka linki klastra. **SSHMaster0** zapewnia SSH połączenia ciąg toohello pierwszego serwera głównego w klastrze usługi kontenera. 

Jak wcześniej zanotowane umożliwia także hello toofind narzędzia Azure FQDN hello wzorca. Należy wzorca toohello przy użyciu nazwy FQDN hello wzorca i nazwa użytkownika hello określone podczas tworzenia klastra hello hello połączenie SSH. Na przykład:

```bash
ssh userName@masterFQDN –A –p 22 
```

Aby uzyskać więcej informacji, zobacz [klastra usługi kontenera platformy Azure tooan Connect](../articles/container-service/kubernetes/container-service-connect.md).

## <a name="next-steps"></a>Następne kroki

* [Dowiedz się więcej](../articles/container-service/kubernetes/container-service-intro-kubernetes.md) o usłudze Azure Container Service.
* Wdrażanie klastra usługi kontenera przy użyciu hello [portal](../articles/container-service/dcos-swarm/container-service-deployment.md) lub [Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md).
