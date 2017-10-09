---
title: aaaOverview maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Opisuje usługi rozwiązań usługi obliczenia Azure, magazynu i sieci maszyn wirtualnych systemu Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: rickstercdn
manager: timlt
editor: 
ms.assetid: 7965a80f-ea24-4cc2-bc43-60b574101902
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/14/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 958e219d53026d787a7a41f2fd13c29c739a9238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux"></a>Azure i Linux
Microsoft Azure to wciąż rozrastający się zbiór zintegrowanych publicznego usług bazy danych analizy, maszyny wirtualne, mobilnych, sieci, magazynu, w tym chmury i sieci web&mdash;nadaje się doskonale dla hostingu rozwiązań.  Microsoft Azure oferuje skalowalne platforma przetwarzania, która pozwala tooonly płatności dla używane, należy go — bez konieczności tooinvest sprzętu lokalnego.  Azure jest gotowy, gdy są tooscale rozwiązań się i limit skali toowhatever wymagają tooservice hello potrzeb klientów.

Jeśli znasz hello różnych funkcji w portalu Amazon usług AWS, można sprawdzić hello Azure vs usług AWS [dokumentu mapowania definicji](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/).

## <a name="regions"></a>Regiony
Microsoft Azure zasoby są rozpowszechniane w różnych regionach geograficznych wokół hello world.  "region" reprezentuje wielu centrów danych w jednym obszarze geograficznym.  Mamy 34 regionów ogólnie dostępna wokół hello world z dodatkowe regiony 4 anonsowania. Ponieważ firma Microsoft trwają tooexpand naszych globalnych pokrycia — możemy Obsługa zaktualizowaną listę istniejących i nowo ogłoszenia regionów.

* [Regiony platformy Azure](https://azure.microsoft.com/regions/)

## <a name="availability"></a>Dostępność
Firma Microsoft opublikowała branży wiodące pojedynczego wystąpienia maszyny wirtualnej z umową dotyczącą poziomu usług z wartością 99,9% pod warunkiem, że wdrażanie hello maszyny Wirtualnej z magazyn w warstwie premium dla wszystkich dysków.  Aby tooqualify Twojego wdrożenia dla naszego standardowego 99,95% wirtualna umową dotyczącą poziomu usług, nadal potrzebujesz toodeploy co najmniej dwie maszyny wirtualne z systemami obciążenie wewnątrz zestawu dostępności. Zapewni to maszyny wirtualne są rozproszone na wielu domen błędów w naszych centrach danych, jak również wdrożyć na hostach z systemem windows konserwacji. Pełna Hello [umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) wyjaśniono hello gwarancji dostępności Azure jako całość.

## <a name="managed-disks"></a>Managed Disks

Zarządzane dysków dojścia do usługi Azure Storage o tworzeniu konta i zarządzania w tle powitania dla Ciebie i sprawia, że nie mogą tooworry dotyczących ograniczeń skalowalności hello hello konta magazynu. Po prostu określić rozmiar dysku hello i warstwę wydajności hello (standardowy lub Premium) i Azure tworzy i zarządza hello dysku. Również w przypadku dodawania dysków lub skalować hello maszyny Wirtualnej w górę i w dół, nie masz tooworry o magazyn hello jest używany. Jeśli tworzysz nowe maszyny wirtualne, [Użyj hello Azure CLI 2.0](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub hello toocreate portalu Azure maszyn wirtualnych z zarządzanych systemu operacyjnego i dysków z danymi. Jeśli masz maszyny wirtualne z dyskami niezarządzane, możesz [przekonwertować toobe sieci maszyn wirtualnych, kopie dysków zarządzanych](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Można również zarządzać niestandardowych obrazów w jedno konto magazynu na region platformy Azure i używać ich toocreate setki maszyn wirtualnych w hello tej samej subskrypcji. Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz hello [omówienie dysków zarządzanych](../windows/managed-disks-overview.md).

## <a name="azure-virtual-machines--instances"></a>Maszyny wirtualne platformy Azure i wystąpień
Microsoft Azure obsługuje uruchamianie wielu popularnych dystrybucje systemu Linux podane i aktualizowany przez liczbę partnerów.  Znajdziesz dystrybucje, takich jak Red Hat Enterprise, CentOS, Debian, Ubuntu, CoreOS, RancherOS, FreeBSD i więcej informacji, zobacz hello Azure Marketplace. Aktywnie pracujemy z różnych tooadd społeczności Linux jeszcze więcej odmian toohello [zatwierdzone Dystrybucjach systemu Linux na platformie Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) listy.

Jeśli z preferowanych distro Linux wyboru nie jest aktualnie w galerii Witaj, "przełączeniem własne Linux" maszyny Wirtualnej przez [tworzenie i przekazywanie wirtualnego dysku twardego systemu Linux na platformie Azure](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Maszyny wirtualne platformy Azure pozwala toodeploy szeroką gamę rozwiązań opartych na przetwarzaniu w sposób elastyczne. Możesz wdrożyć niemal dowolnym obciążeniu i dowolnego języka na niemal każde system operacyjny: Windows, Linux, lub niestandardowy utworzony z jednego z naszych coraz dłuższej listy partnerów. Nadal nie widać, czego szukasz?  Nie martw się — można również przełączyć własnych obrazów z lokalnymi.

## <a name="vm-sizes"></a>Rozmiary maszyn wirtualnych
Podczas wdrażania maszyny Wirtualnej na platformie Azure ma tooselect dla rozmiaru maszyny Wirtualnej w ramach jednej z naszych serii rozmiary odpowiedniego tooyour obciążenia. rozmiar Hello wpływa także hello przetwarzania zasilania, pamięć i pojemność magazynu hello maszyny wirtualnej. Rozliczenie jest oparte na powitania ilość czasu hello maszyna wirtualna jest uruchomiona i korzystanie z jej przydzielone zasoby. Pełna lista [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Poniżej przedstawiono podstawowe wskazówki dotyczące wybierania rozmiar maszyny Wirtualnej z jednego z naszych serii (A, D, DS, G i GS).
* A-series maszyny wirtualne są nasze wartość cenach klasy podstawowej maszyn wirtualnych dla lekkich obciążeń i scenariusze tworzenia/testowania. Są powszechnie dostępne we wszystkich regionach i mogą połączyć i używać wszystkie standardowe zasoby dostępne toovirtual maszyny.
* A-series (A8 - A11) są specjalne obliczeń znacznym konfiguracje odpowiedni w przypadku wysokiej wydajności obliczeniowej klastra.
* D-series maszyny wirtualne są zaprojektowane toorun aplikacji, które wymaga wyższej moc obliczeniową i wydajność dysku tymczasowym. Maszyny wirtualne D-series zapewniają szybkich procesorów, większy współczynnik pamięci — podstawowe i dysków półprzewodnikowych (SSD) dla dysku tymczasowym hello.
* Dv2 serii jest najnowsza wersja hello naszych D-series, funkcje większe możliwości procesora CPU. Hello serii Dv2 Procesora CPU D-series jest około 35% szybciej niż hello. Jest on oparty na powitania najnowszej generacji 2.4 v3® GHz Intel Xeon E5-2673 procesora (Haskell) i z hello Intel Turbo zwiększanie wyniku technologii 2.0, może przejść w górę too3.2 GHz. ma Hello serii Dv2 hello takie same konfiguracje pamięci i dysku, ponieważ hello D-series.
* Maszyny wirtualne z serii G oferują hello najwięcej pamięci i uruchom na hostach, które mają rodziny procesorów Intel Xeon E5 V3.

Uwaga: Serii DS i GS-series maszyny wirtualne mają tooPremium dostępu do magazynu — nasze SSD kopii wysokiej wydajności i małych opóźnieniach magazynu dla intensywnych obciążeń we/wy. Usługa Premium Storage jest dostępna w określonych regionach. Aby uzyskać szczegółowe informacje, zobacz:

* [Magazyn w warstwie Premium: Magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej platformy Azure](../../storage/common/storage-premium-storage.md)

## <a name="automation"></a>Automatyzacja
tooachieve właściwe kultury DevOps wszystkie infrastruktury musi być kodem.  Gdy wszystkie hello infrastruktury życie w kodzie mogą być łatwo odtworzyć (Phoenix serwerów).  Azure współpracuje z wszystkich automatyzacji głównych hello narzędzi, takich jak Ansible, Chef, SaltStack i Puppet.  Platforma Azure ma własną narzędziami automatyzacji:

* [Szablony usługi Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure rozszerzenia VMAccess.](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Azure wprowadza obsługę [init chmury](http://cloud-init.io/) przez większość Dystrybucjach systemu Linux, który go obsługuje.  Obecnie maszyn wirtualnych systemu Ubuntu na Canonical zostały wdrożone za pomocą chmury inicjowaniem domyślnie włączone.  Czerwony Kapelusze RHEL, CentOS i Fedora obsługi chmury init, jednak hello Azure obsługiwanego przez RedHat obrazów nie mają zainstalowany inicjowania chmury.  toouse chmury inicjowania w danej rodzinie RedHat systemu operacyjnego, należy utworzyć niestandardowy obraz z inicjowaniem chmury zainstalowane.

* [Za pomocą init chmurze na maszynach wirtualnych systemu Linux platformy Azure](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quotas"></a>Przydziały
Każda subskrypcja platformy Azure ma domyślne limity przydziału w miejscu, które mogą wpłynąć na powitania wdrażania wielu maszyn wirtualnych dla projektu. bieżący limit Hello na podstawie subskrypcji na to 20 maszyn wirtualnych na region.  Limity przydziału może zostać wywołane szybko i łatwo zgłaszając bilet pomocy technicznej żąda limit zwiększyć.  Aby uzyskać więcej informacji na temat limitów przydziału:

* [Ograniczenia usługi subskrypcji platformy Azure](../../azure-subscription-service-limits.md)

## <a name="partners"></a>Partnerzy
Firma Microsoft ściśle współpracuje z partnerami dostępnych obrazów hello tooensure są aktualizowane i zoptymalizowany pod kątem obsługi usługi Azure.  Aby uzyskać więcej informacji na temat naszych partnerów Sprawdź stronach witryny marketplace poniżej.

* Linux na platformie Azure - [dystrybucje zatwierdzone](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* SUSE - [witrynę Azure Marketplace — SUSE Linux Enterprise Server](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=%27SUSE%27)
* RedHat - [witrynę Azure Marketplace — RedHat Enterprise Linux 7.2](https://azure.microsoft.com/marketplace/partners/redhat/redhatenterpriselinux72/)
* Canonical - [witrynę Azure Marketplace — LTS Ubuntu Server 16.04](https://azure.microsoft.com/marketplace/partners/canonical/ubuntuserver1604lts/)
* Debian - [witrynę Azure Marketplace — 8 Debian "Joasia"](https://azure.microsoft.com/marketplace/partners/credativ/debian8/)
* FreeBSD - [witrynę Azure Marketplace — FreeBSD 10.3](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
* CoreOS - [witrynę Azure Marketplace — CoreOS (stały)](https://azure.microsoft.com/marketplace/partners/coreos/coreosstable/)
* RancherOS - [witrynę Azure Marketplace — RancherOS](https://azure.microsoft.com/marketplace/partners/rancher/rancheros/)
* Bitnami - [Bitnami biblioteki dla platformy Azure](https://azure.bitnami.com/)
* Mesosphere - [witrynę Azure Marketplace — Mesosphere DC/OS na platformie Azure](https://azure.microsoft.com/marketplace/partners/mesosphere/dcosdcos/)
* Docker - [witrynę Azure Marketplace — usługi kontenera platformy Azure z Docker Swarm](https://azure.microsoft.com/marketplace/partners/microsoft/acsswarms/)
* Wpięć - [witrynę Azure Marketplace — CloudBees Wpięć platformy](https://azure.microsoft.com/marketplace/partners/cloudbees/jenkins-platformjenkins-platform/)

## <a name="getting-started-with-linux-on-azure"></a>Rozpoczynanie pracy z systemem Linux na platformie Azure
toobegin za pomocą platformy Azure jest potrzebne konto platformy Azure, hello Azure CLI zainstalowany i parę kluczy publicznych i prywatnych SSH.

### <a name="sign-up-for-an-account"></a>Tworzenie konta
pierwszym krokiem Hello za pomocą hello chmury Azure jest toosign dla konta platformy Azure.  Przejdź toohello [możliwość tworzenia konta Azure](https://azure.microsoft.com/pricing/free-trial/) strony tooget uruchomiona.

### <a name="install-hello-cli"></a>Zainstaluj hello interfejsu wiersza polecenia
Przy użyciu nowego konta platformy Azure możesz rozpocząć pracę od razu przy użyciu portalu Azure, czyli panelu opartych na sieci web admin hello.  toomanage hello chmury Azure za pośrednictwem hello wiersza polecenia, należy zainstalować hello `azure-cli`.  Zainstaluj hello [Azure CLI 2.0](/cli/azure/install-azure-cli) na stacji roboczej Mac lub Linux.

### <a name="create-an-ssh-key-pair"></a>Tworzenie pary kluczy SSH
Teraz masz konto platformy Azure, portalu sieci web platformy Azure hello i hello wiersza polecenia platformy Azure.  Witaj następnym krokiem jest toocreate parę kluczy SSH, który jest używany tooSSH w systemie Linux bez użycia hasła.  [Tworzenie kluczy SSH w systemie Linux i komputerów Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooenable hasła bez nazwy logowania i większe bezpieczeństwo.

### <a name="create-a-vm-using-hello-cli"></a>Utwórz maszynę Wirtualną przy użyciu hello interfejsu wiersza polecenia
Tworzenie maszyny Wirtualnej systemu Linux przy użyciu interfejsu wiersza polecenia hello jest toodeploy szybko Maszynę wirtualną bez zostawianie hello terminali pracujesz w.  Wszystkie obiekty, które można określić w portalu sieci web hello jest dostępna za pośrednictwem flagi wiersza polecenia lub przełącznika.  

* [Utwórz Maszynę wirtualną systemu Linux przy użyciu hello interfejsu wiersza polecenia](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="create-a-vm-in-hello-portal"></a>Tworzenie maszyny Wirtualnej w portalu hello
Tworzenie maszyny Wirtualnej systemu Linux w portalu sieci web platformy Azure hello jest sposób punktu tooeasily i kliknij przycisk za pośrednictwem hello różne opcje tooget tooa wdrożenia.  Zamiast używać flagi wiersza polecenia i przełączniki, jest możliwe tooview układ nieuprzywilejowany web różnych opcji i ustawień.  Wszystkie dostępne za pośrednictwem interfejsu wiersza polecenia hello jest również dostępna w portalu hello.

* [Utwórz Maszynę wirtualną systemu Linux przy użyciu hello portalu](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="login-using-ssh-without-a-password"></a>Zaloguj się przy użyciu protokołu SSH bez hasła
Witaj maszyna wirtualna jest teraz uruchomiona na platformie Azure i są gotowe toolog w.  Za pomocą hasła toolog w za pośrednictwem SSH jest niebezpieczne i czasochłonna.  Przy użyciu kluczy SSH jest hello najbezpieczniejszą metodą, a także hello najszybszy sposób toologin.  Po utworzeniu można maszyny Wirtualnej systemu Linux za pośrednictwem portalu hello lub hello interfejsu wiersza polecenia, dostępne są dwie opcje uwierzytelniania.  Jeśli hasło SSH, Azure konfiguruje hello wirtualna tooallow logowania za pomocą hasła.  Jeśli została wybrana opcja toouse klucz publiczny SSH, Azure konfiguruje hello wirtualna tooonly Zezwalaj logowania za pośrednictwem SSH kluczy i wyłącza hasło logowania. toosecure maszyny Wirtualnej systemu Linux przez tylko umożliwienia logowania do klucza SSH, użyj hello publicznego opcji klucza SSH podczas hello tworzenie maszyny Wirtualnej w portalu hello lub interfejsu wiersza polecenia.

## <a name="related-azure-components"></a>Powiązane składniki platformy Azure
## <a name="storage"></a>Magazyn
* [Wprowadzenie tooMicrosoft usługi Azure Storage](../../storage/common/storage-introduction.md)
* [Dodaj tooa dysku maszyny Wirtualnej systemu Linux przy użyciu wiersza polecenia platformy azure hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Jak tooattach danych na dysku tooa maszyny Wirtualnej systemu Linux w hello portalu Azure](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Sieć
* [Omówienie sieci wirtualnej](../../virtual-network/virtual-networks-overview.md)
* [Adresy IP na platformie Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)
* [Otwieranie portów tooa maszyny Wirtualnej systemu Linux na platformie Azure](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Utwórz w pełni kwalifikowaną nazwę domeny w hello portalu Azure](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="containers"></a>Kontenery
* [Maszyny wirtualne i kontenerów na platformie Azure](containers.md)
* [Wprowadzenie usługi kontenera platformy Azure](../../container-service/container-service-intro.md)
* [Wdrażanie klastra usługi Azure Container Service](../../container-service/dcos-swarm/container-service-deployment.md)

## <a name="next-steps"></a>Następne kroki
Masz teraz Omówienie systemu Linux na platformie Azure.  następnym krokiem Hello toodive w i utworzyć kilka maszyn wirtualnych!

* [Eksploruj nasze coraz dłuższej listy przykładowe skrypty do wykonywania typowych zadań za pomocą AzureCLI](cli-samples.md)
