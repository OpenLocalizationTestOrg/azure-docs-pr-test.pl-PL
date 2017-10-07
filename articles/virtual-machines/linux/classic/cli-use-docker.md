---
title: Witaj aaaUsing Docker rozszerzenia maszyny Wirtualnej dla systemu Linux na platformie Azure
description: "Opisuje Docker i rozszerzeń maszyny wirtualnej Azure hello i pokazuje, jak tooprogrammatically Tworzenie maszyn wirtualnych na platformie Azure, która hostów docker z wiersza polecenia hello przy użyciu interfejsu wiersza polecenia Azure hello."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a>Przy użyciu hello Docker rozszerzenia maszyny Wirtualnej z hello interfejsu wiersza polecenia platformy Azure (Azure CLI)
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Aby dowiedzieć się, jak przy użyciu rozszerzenia maszyny Wirtualnej platformy Docker hello hello modelu Resource Manager, zobacz [tutaj](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

W tym temacie opisano, jak toocreate maszyny Wirtualnej z hello Docker rozszerzenia maszyny Wirtualnej z hello usługi zarządzania (asm) trybu w wiersza polecenia platformy Azure na dowolnej platformie. [Docker](https://www.docker.com/) jest jednym z hello najpopularniejszych podejść wirtualizacji, które używa [kontenery Linux](http://en.wikipedia.org/wiki/LXC) zamiast maszyn wirtualnych w sposób izolowanie danych i przetwarzania danych w udostępnionych zasobów. Można użyć rozszerzenia maszyny Wirtualnej platformy Docker hello i hello [agenta systemu Linux Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate Docker maszyny Wirtualnej, który obsługuje dowolną liczbę kontenerów dla aplikacji na platformie Azure. Ogólne omówienie kontenery i ich zalety toosee Zobacz hello [Docker wysoki poziom tablicy](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a>Jak toouse hello Docker rozszerzenia maszyny Wirtualnej z platformy Azure
toouse rozszerzenia maszyny Wirtualnej platformy Docker hello Azure, należy zainstalować wersję hello [interfejsu wiersza polecenia platformy Azure](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) wyższa niż 0.8.6 (zgodnie z tym hello pisania bieżąca wersja to 0.10.0). Witaj wiersza polecenia platformy Azure można zainstalować na Mac, Linux i Windows.

Witaj Zakończ proces toouse Docker na platformie Azure jest prosty:

* Zainstaluj na komputerze hello, z którego mają zostać toocontrol Azure hello wiersza polecenia platformy Azure i jego zależności (w systemie Windows, to będzie dystrybucji systemu Linux, uruchomione jako maszyny wirtualnej)
* Użyj hello Azure CLI Docker polecenia toocreate hosta maszyny Wirtualnej platformy Docker na platformie Azure
* W maszynie Wirtualnej platformy Docker na platformie Azure, należy użyć toomanage polecenia Docker lokalne powitania kontenerów Docker.

### <a name="install-hello-azure-command-line-interface-azure-cli"></a>Zainstaluj hello interfejsu wiersza polecenia platformy Azure (Azure CLI)
tooinstall oraz konfigurowania hello wiersza polecenia platformy Azure, zobacz [jak tooinstall hello interfejsu wiersza polecenia platformy Azure](../../../cli-install-nodejs.md). tooconfirm hello instalacji, typ `azure` hello wiersza polecenia i po chwili krótkich powinna zostać wyświetlona hello grafikę ASCII interfejsu wiersza polecenia Azure, której znajduje się lista hello basic polecenia tooyou dostępne. Jeśli instalacja hello działał poprawnie, należy tootype stanie `azure help vm` i sprawdzić, czy jest jedno z poleceń hello wymienione "docker".

> [!NOTE]
> Docker ma narzędzi dla systemu Windows, [maszyny Docker](https://docs.docker.com/installation/windows/), która umożliwia także tworzenie hello tooautomate klienta docker czy toowork można używać z maszynami wirtualnymi Azure jako hostów docker.
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a>Połącz hello Azure CLI tootooyour konto platformy Azure
Przed użyciem hello Azure CLI poświadczenia konta Azure należy skojarzyć z hello Azure CLI na platformie. Witaj sekcji [jak tooyour tooconnect subskrypcji platformy Azure](../../../xplat-cli-connect.md) wyjaśniono, jak tooeither pobierać i importować z **.publishsettings** plików lub kojarzenie z wiersza polecenia platformy Azure przy użyciu identyfikatora organizacyjnego.

> [!NOTE]
> Istnieją pewne różnice w zachowaniu, korzystając z jednego lub hello innych metod uwierzytelniania, dlatego należy się, że dokument hello tooread powyżej toounderstand hello różne funkcje.
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a>Zainstaluj Docker i użyj hello rozszerzenia maszyny Wirtualnej platformy Docker na platformie Azure
Wykonaj hello [instrukcje dotyczące instalacji Docker](https://docs.docker.com/installation/#installation) tooinstall Docker lokalnie na komputerze.

toouse Docker z maszyny wirtualnej platformy Azure, hello Linux obraz powitania maszyna wirtualna musi mieć hello [Agent maszyny Wirtualnej systemu Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zainstalowane. Obecnie istnieją tylko dwa typy obrazów, które to zapewniają:

* Obraz Ubuntu z hello Galeria obrazów Azure lub
* Niestandardowy obraz systemu Linux utworzone hello Agent maszyny Wirtualnej systemu Linux jest zainstalowana i skonfigurowana. Zobacz [Agent maszyny Wirtualnej systemu Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Aby uzyskać więcej informacji o tym, jak toobuild niestandardowych maszyny Wirtualnej systemu Linux z hello Agent maszyny Wirtualnej.

### <a name="using-hello-azure-image-gallery"></a>Przy użyciu Galeria obrazów hello Azure
Bash lub sesję terminalu Użyj funkcji powitania po toolocate hello najnowszy obraz Ubuntu w hello wirtualna galerii toouse, wpisując polecenie wiersza polecenia platformy Azure

`azure vm image list | grep Ubuntu-14_04`

i wybierz jedną z nazw obraz powitania, takich jak `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, i użyj hello następujące polecenie toocreate nowej maszyny Wirtualnej za pomocą tego obrazu.

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

Gdzie:

* *&lt;Nazwa maszyny wirtualnej cloudservice&gt;*  jest nazwą hello hello maszyny Wirtualnej, który ma zostać komputerze hosta kontenera Docker hello na platformie Azure
* *&lt;Nazwa użytkownika&gt;*  jest nazwa hello hello domyślnego katalogu głównego użytkownika hello maszyny Wirtualnej
* *&lt;hasło&gt;*  jest hasło hello hello *username* konta, spełniającej standardy hello złożoności dla platformy Azure

> [!NOTE]
> Obecnie hasło musi być co najmniej 8 znaków, zawiera jeden małe litery i Wielka litera, liczbę i znaków specjalnych, takich jak jeden z następujących znaków hello: `!@#$%^&+=`. Nie, okres hello na końcu hello hello zdaniu poprzedzającym nie jest znak specjalny.
> 
> 

Jeśli polecenie hello zakończyło się pomyślnie, powinien zostać wyświetlony przypominać następujące hello, w zależności od hello dokładne argumentów i opcji, których użyto:

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> Tworzenie maszyny wirtualnej może potrwać kilka minut, ale po zostały udostępnione (wartość stanu hello jest `ReadyRole`) hello uruchamiania demona (hello usługi Docker) Docker i możesz połączyć hosta kontenera Docker toohello.
> 
> 

Witaj tootest Docker maszyny Wirtualnej zostały utworzone na platformie Azure, typ

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

gdzie  *&lt;vm nazwa--użyta&gt;*  jest nazwą hello hello maszyny wirtualnej, używany w połączeniu zbyt`azure vm docker create`. Powinny pojawić się coś podobnego następujące toohello, co oznacza, że Host maszyny Wirtualnej platformy Docker działa i działających na platformie Azure i Oczekiwanie na poleceniach. 

Teraz możesz spróbować tooconnect przy użyciu informacji tooobtain docker klienta (w niektórych ustawień klienta Docker, takim jak dla komputerów Mac, konieczne może być toouse `sudo`):

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

Po prostu toobe pewność, że jest ona wszystkie pracy, można sprawdzić hello maszyny Wirtualnej dla hello Docker rozszerzenia:

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a>Uwierzytelnianie programu docker hosta maszyny Wirtualnej
Ponadto hello toocreating hello wirtualna Docker `azure vm docker create` polecenia automatycznie tworzy hello wymagane certyfikaty tooallow Docker klienta komputera tooconnect toohello kontenera platformy Azure hosta przy użyciu protokołu HTTPS i hello certyfikaty są przechowywane na serwerze Witaj klientem i hostem maszyny, zależnie od potrzeb. Na kolejnych prób hello istniejących certyfikatów są ponownie i udostępniać hello nowego hosta.

Domyślnie certyfikaty są umieszczane w `~/.docker`, i Docker zostaną skonfigurowane toorun na porcie **2376**. Jeśli chcesz toouse inny port lub katalog, a następnie możesz skorzystać z jednej z następujących hello `azure vm docker create` wiersza polecenia Opcje tooconfigure Twojego Docker kontenera hosta maszyny Wirtualnej toouse inny port lub różnych certyfikatów klientów nawiązujących połączenie:

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

Hello demon Docker na hoście hello jest toolisten skonfigurowanych dla i uwierzytelniania klienta połączeń na powitania określony port przy użyciu certyfikatów hello generowane przez hello `azure vm docker create` polecenia. komputer kliencki Hello muszą mieć te certyfikaty toogain dostępu toohello Docker hosta.

> [!NOTE]
> Sieci hosta z systemem bez tych certyfikatów będzie tooanyone narażony, który można tooconnect toohello maszyny. Przed zmodyfikowaniem hello domyślnej konfiguracji upewnij się, że rozumiesz hello ryzyka tooyour komputery i aplikacje.
> 
> 

## <a name="next-steps"></a>Następne kroki
* Wszystko jest gotowe toogo toohello [Podręcznik użytkownika Docker] i użyć maszyny Wirtualnej platformy Docker. Zobacz toocreate włączone Docker maszyny Wirtualnej w ramach nowego portalu hello [jak toouse hello Docker rozszerzenia maszyny Wirtualnej z hello Portal].
* Hello rozszerzenia maszyny Wirtualnej Azure Docker również obsługuje rozwiązania Docker Compose, który używa deklaratywne tootake pliku yaml programu modelowane Deweloper aplikacji w każdym środowisku i wygenerować spójne wdrożenia. Zobacz [Rozpoczynanie pracy z rozwiązaniem Docker tworzą toodefine i uruchomić aplikację usługi kontenera na maszynie wirtualnej platformy Azure].  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[jak toouse hello Docker rozszerzenia maszyny Wirtualnej z hello Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[Podręcznik użytkownika Docker]:https://docs.docker.com/userguide/

[Rozpoczynanie pracy z rozwiązaniem Docker tworzą toodefine i uruchomić aplikację usługi kontenera na maszynie wirtualnej platformy Azure]:../docker-compose-quickstart.md
