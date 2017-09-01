# <a name="container-service-frequently-asked-questions"></a>Często zadawane pytania dotyczące usługi Container Service

## <a name="orchestrators"></a>Koordynatorzy

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>Których koordynatorów kontenerów obsługuje usługa Azure Container Service? 

Obsługiwane są następujące usługi typu open source: DC/OS, Docker Swarm i Kubernetes. Aby uzyskać więcej informacji, zapoznaj się z [omówieniem](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
 
### <a name="do-you-support-docker-swarm-mode"></a>Czy tryb Docker Swarm jest obsługiwany? 

Obecnie tryb Swarm nie jest obsługiwany, ale znajduje się w planie usług. 

### <a name="does-azure-container-service-support-windows-containers"></a>Czy usługa Azure Container Service obsługuje kontenery z systemem Windows?  

Obecnie kontenery systemu Linux są obsługiwane przy użyciu wszystkich koordynatorów. Obsługa kontenerów systemu Windows przy użyciu usługi Kubernetes jest dostępna w wersji zapoznawczej.

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>Czy zalecane jest korzystanie z określonego koordynatora w usłudze Azure Container Service? 
Ogólnie nie zalecamy korzystania z określonego koordynatora. Jeśli masz doświadczenie w pracy z jednym z obsługiwanych koordynatorów, możesz zastosować go w usłudze Azure Container Service. Trendy danych sugerują jednak, że platforma DC/OS została sprawdzona podczas produkcji w przypadku obciążeń danych Big Data i IoT, usługa Kubernetes jest dobrym rozwiązaniem w przypadku natywnych obciążeń w chmurze, a usługa Docker Swarm jest znana z możliwości integrowania z narzędziami Docker oraz prostego procesu uczenia się.

W zależności od swojego scenariusza możesz również kompilować niestandardowe rozwiązania kontenerów i zarządzać nimi przy użyciu innych usług Azure. Usługi te to: [Virtual Machines](../articles/virtual-machines/linux/overview.md), [Service Fabric](../articles/service-fabric/service-fabric-overview.md), [Web Apps](../articles/app-service-web/app-service-web-overview.md) i [Batch](../articles/batch/batch-technical-overview.md).  

### <a name="what-is-the-difference-between-azure-container-service-and-acs-engine"></a>Jaka jest różnica między usługą Azure Container Service i aparatem usługi ACS? 
Azure Container Service to usługa platformy Azure z umową SLA, która oferuje funkcje działające w witrynie Azure Portal, narzędziach wiersza polecenia platformy Azure oraz interfejsach API platformy Azure. Usługa ta umożliwia szybkie implementowanie klastrów z uruchomionymi standardowymi narzędziami koordynowania kontenerów i stosunkowo niewielką liczbą opcji konfiguracji do wyboru oraz zarządzanie nimi. 

[Aparat usługi ACS](http://github.com/Azure/acs-engine) to projekt typu open source, który umożliwia użytkownikom zaawansowanym dostosowywanie konfiguracji klastra na dowolnym poziomie. Ta zdolność do zmiany konfiguracji infrastruktury i oprogramowania oznacza, że w przypadku aparatu usługi ACS nie oferujemy umowy SLA. Obsługa odbywa się za pośrednictwem projektu typu open source w usłudze GitHub, a nie przez oficjalne kanały firmy Microsoft. 

## <a name="cluster-management"></a>Zarządzanie klastrami

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>Jak mogę utworzyć klucze SSH dla mojego klastra?

Aby utworzyć parę kluczy publicznych i prywatnych SSH RSA na potrzeby uwierzytelniania względem maszyn wirtualnych z systemem Linux dla klastra, możesz skorzystać ze standardowych narzędzi dostępnych w systemie operacyjnym. Informacje dotyczące kroków do wykonania można znaleźć we wskazówkach dotyczących systemów [OS X i Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) lub [Windows](../articles/virtual-machines/linux/ssh-from-windows.md). 

Jeśli używasz [poleceń interfejsu wiersza polecenia Azure 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) do wdrażania klastra usługi kontenera, klucze SSH dla klastra mogą być generowane automatycznie.

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>Jak mogę utworzyć nazwę główną usługi dla mojego klastra Kubernetes?

Do utworzenia klastra Kubernetes w usłudze Azure Container Service wymagany jest również identyfikator i hasło nazwy głównej usługi Azure Active Directory. Aby uzyskać więcej informacji, zobacz [About the service principal for a Kubernetes cluster](../articles/container-service/kubernetes/container-service-kubernetes-service-principal.md) (Informacje o nazwie głównej usługi dla klastra Kubernetes).

Jeśli używasz [poleceń interfejsu wiersza polecenia Azure 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) do wdrażania klastra Kubernetes, poświadczenia nazwy głównej usługi dla klastra mogą być generowane automatycznie.

### <a name="how-large-a-cluster-can-i-create"></a>Jak duży klaster mogę utworzyć?
Możesz utworzyć klaster z 1, 3 lub 5 węzłami głównymi. Możesz wybrać maksymalnie 100 węzłów agentów.

> [!IMPORTANT]
> W przypadku większych klastrów i w zależności od rozmiaru maszyny wirtualnej wybranego dla węzłów może być konieczne zwiększenie limitu przydziału rdzeni w ramach subskrypcji. Aby zażądać zwiększenia limitu przydziału, otwórz bezpłatnie [żądanie obsługi klienta online](../articles/azure-supportability/how-to-create-azure-support-request.md). Jeśli używasz [bezpłatnego konta platformy Azure](https://azure.microsoft.com/free/), możesz użyć ograniczonej liczby rdzeni obliczeniowych platformy Azure.
> 

### <a name="how-do-i-increase-the-number-of-masters-after-a-cluster-is-created"></a>Jak mogę zwiększyć liczbę wzorców po utworzeniu klastra? 
Po utworzeniu klastra liczba wzorców jest stała i nie można jej zmienić. Podczas tworzenia klastra najlepiej wybrać wiele wzorców wysokiej dostępności.

### <a name="how-do-i-increase-the-number-of-agents-after-a-cluster-is-created"></a>Jak mogę zwiększyć liczbę agentów po utworzeniu klastra? 
Liczbę agentów można skalować w klastrze za pomocą witryny Azure Portal lub narzędzi wiersza polecenia. Zobacz [Scale an Azure Container Service cluster](../articles/container-service/kubernetes/container-service-scale.md) (Skalowanie klastra usługi Azure Container Service).

### <a name="what-are-the-urls-of-my-masters-and-agents"></a>Jakie są adresy URL moich wzorców i agentów? 
Adresy URL zasobów klastra w usłudze Azure Container Service opierają się na podanym prefiksie nazwy DNS i nazwie regionu platformy Azure wybranego do wdrożenia. Na przykład w pełni kwalifikowana nazwa domeny (FQDN) węzła głównego ma następującą postać:

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

Często używane adresy URL dla klastra można znaleźć w witrynie Azure Portal, Eksploratorze zasobów Azure lub innych narzędziach platformy Azure.

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a>Jak sprawdzić, która wersja koordynatora jest uruchamiana w moim klastrze?

* DC/OS: zobacz [dokumentację w witrynie Mesosphere](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)
* Docker Swarm: uruchom polecenie `docker version`
* Kubernetes: uruchom polecenie `kubectl version`

### <a name="how-do-i-upgrade-the-orchestrator-after-deployment"></a>Jak uaktualnić koordynatora po wdrożeniu?

Obecnie usługa Azure Container Service nie oferuje narzędzi umożliwiających uaktualnianie wersji koordynatora wdrożonego w klastrze. Jeśli usługa Container Service obsługuje nowszą wersję, można wdrożyć nowy klaster. Inna opcja to miejscowe uaktualnienie klastra przy użyciu narzędzi specyficznych dla koordynatora, jeśli są dostępne. Na przykład zobacz [DC/OS Upgrading](https://dcos.io/docs/1.8/administration/upgrading/) (Uaktualnianie rozwiązania DC/OS).
 
### <a name="where-do-i-find-the-ssh-connection-string-to-my-cluster"></a>Gdzie mogę znaleźć parametry połączenia SSH z moim klastrem?

Parametry połączenia można znaleźć w witrynie Azure Portal lub za pomocą narzędzia wiersza polecenia platformy Azure. 

1. W portalu przejdź do grupy zasobów dla wdrożenia klastra.  

2. Kliknij pozycję **Przegląd** i kliknij link dla pozycji **Wdrożenia** w obszarze **Podstawy**. 

3. W bloku **Historia wdrażania** kliknij wdrożenie z nazwą rozpoczynającą się od **microsoft acs**, po której następuje data wdrożenia. Przykład: microsoft-acs-201701310000.  

4. Na stronie **Podsumowanie** w obszarze **Dane wyjściowe** znajduje się kilka linków klastra. Element **SSHMaster0** zawiera parametry połączenia SSH z pierwszym wzorcem w klastrze usługi kontenera. 

Jak wspomniano wcześniej, do wyszukania nazwy FQDN wzorca można również użyć narzędzi platformy Azure. Utwórz połączenie SSH z wzorcem, używając nazwy FQDN wzorca i nazwy użytkownika podanej podczas tworzenia klastra. Na przykład:

```bash
ssh userName@masterFQDN –A –p 22 
```

Aby uzyskać więcej informacji, zobacz [Łączenie z klastrem usługi Azure Container Service](../articles/container-service/kubernetes/container-service-connect.md).

## <a name="next-steps"></a>Następne kroki

* [Dowiedz się więcej](../articles/container-service/kubernetes/container-service-intro-kubernetes.md) o usłudze Azure Container Service.
* Wdrażanie klastra usługi kontenera przy użyciu [portalu](../articles/container-service/dcos-swarm/container-service-deployment.md) lub [interfejsu wiersza polecenia platformy Azure w wersji 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md).
