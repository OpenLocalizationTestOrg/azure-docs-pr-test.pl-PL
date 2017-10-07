---
title: aaaUsing Docker rozszerzenia maszyny Wirtualnej dla systemu Linux | Dokumentacja firmy Microsoft
description: "Opisuje Docker i hello rozszerzeń maszyny wirtualnej Azure oraz jak hello toocreate maszyn wirtualnych Azure, które są hostami docker przy użyciu wiersza polecenia platformy Azure w klasycznym modelu wdrażania."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a>Przy użyciu hello Docker rozszerzenia maszyny Wirtualnej z hello klasycznego portalu Azure
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

[Docker](https://www.docker.com/) jest jednym z hello najpopularniejszych podejść wirtualizacji, które używa [kontenery Linux](http://en.wikipedia.org/wiki/LXC) zamiast maszyn wirtualnych w sposób izolowanie danych i przetwarzania danych w udostępnionych zasobów. Można użyć rozszerzenia maszyny Wirtualnej platformy Docker hello zarządza [agenta systemu Linux Azure] toocreate Docker maszyny Wirtualnej, który obsługuje dowolną liczbę kontenerów dla aplikacji na platformie Azure.

> [!NOTE]
> W tym temacie opisano, jak toocreate a VM Docker z hello klasycznego portalu Azure. toosee toocreate maszyny Wirtualnej platformy Docker w wierszu polecenia hello, zobacz temat [jak toouse hello Docker rozszerzenia maszyny Wirtualnej z interfejsu wiersza polecenia platformy Azure (Azure CLI) hello]. Ogólne omówienie kontenery i ich zalety toosee Zobacz hello [Docker wysoki poziom tablicy](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a>Utwórz nową maszynę Wirtualną na podstawie hello Galeria obrazów
pierwszym krokiem Hello wymaga maszyny Wirtualnej platformy Azure z obrazu systemu Linux, który obsługuje hello Docker rozszerzenia maszyny Wirtualnej, przy użyciu obrazu Ubuntu 14.04 LTS z hello Galeria obrazów jako przykład obrazu serwera i Ubuntu 14.04 pulpitu jako klienta. W portalu powitania kliknij **+ nowy** w hello lewy dolny róg toocreate nowe wystąpienie maszyny Wirtualnej, a następnie wybierz obraz Ubuntu 14.04 LTS z dostępnych opcji hello lub hello ukończyć Galeria obrazów, jak pokazano poniżej.

> [!NOTE]
> Obecnie tylko obrazy Ubuntu 14.04 LTS nowsza niż lipca 2014 obsługują hello Docker rozszerzenia maszyny Wirtualnej.
> 
> 

![Utwórz nowy obraz Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a>Tworzenie certyfikatów Docker
Po hello utworzenia maszyny Wirtualnej upewnij się, że Docker jest zainstalowany na komputerze klienckim. (Aby uzyskać więcej informacji, zobacz [instrukcje dotyczące instalacji Docker](https://docs.docker.com/installation/#installation).)

Utwórz hello certyfikat i klucz pliki komunikacji Docker zbyt zgodnie z[systemem Docker z protokołu https] i umieścić je w hello  **`~/.docker`**  katalogu na komputerze klienckim.

> [!NOTE]
> Witaj Docker rozszerzenia maszyny Wirtualnej w portalu hello obecnie wymaga poświadczeń kodowany w standardzie base64.
> 
> 

W wierszu polecenia hello, użyj  **`base64`**  lub innego elementu ulubionego kodowanie tematy dotyczące narzędzia toocreate algorytmem Base64. W ten sposób z prostym zestawem plików certyfikat i klucz może wyglądać podobnie toothis:

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a>Dodaj hello Docker rozszerzenia maszyny Wirtualnej
tooadd hello rozszerzenia maszyny Wirtualnej platformy Docker Znajdź hello wystąpienia maszyny Wirtualnej został utworzony i przewiń w dół za**rozszerzenia** i kliknij go toobring się rozszerzeń maszyny Wirtualnej, jak pokazano poniżej.

> [!NOTE]
> Ta funkcja jest obsługiwana w portalu w wersji zapoznawczej hello tylko: https://portal.azure.com/
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a>Dodaj rozszerzenie
Kliknij przycisk hello **+ Dodaj** toodisplay hello możliwych rozszerzeń maszyny Wirtualnej można dodać toothis maszyny Wirtualnej.

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a>Wybierz hello Docker rozszerzenia maszyny Wirtualnej
Wybierz hello Docker rozszerzenia maszyny Wirtualnej, który wywołuje hello Docker opis i ważne łącza, a następnie kliknij przycisk **Utwórz** na powitania dolnej toobegin hello instalacji procedurze.

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a>Dodaj certyfikat i pliki klucza:
Hello pól formularza wprowadź hello algorytmem Base64 wersji certyfikat urzędu certyfikacji, certyfikat serwera i klucz serwera, jak pokazano w powitania po grafiki.

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> Należy pamiętać, że (jak hello poprzedzające obraz) hello 2376 jest wypełniane domyślnie. Możesz wprowadzić tutaj dowolnego punktu końcowego, ale hello następnym krokiem będzie tooopen się hello dopasowania punktu końcowego. W przypadku zmiany domyślnego hello, upewnij się, że tooopen się hello dopasowania punktu końcowego w następnym kroku hello.
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a>Dodaj hello punkt końcowy komunikacji Docker
Podczas wyświetlania po utworzeniu grupy zasobów hello, wybierz hello grupy zabezpieczeń sieci skojarzonych z maszyny Wirtualnej i kliknij **reguły zabezpieczeń ruchu przychodzącego** tooview hello reguł, jak pokazano poniżej.

![](media/portal-use-docker/AddingEndpoint.png)

Kliknij przycisk **+ Dodaj** tooadd inną regułę, a w przypadku domyślnego hello, wprowadź nazwę dla punktu końcowego hello (w tym przykładzie **Docker**), a 2376 "zakres portów docelowych". Ustaw przedstawiający wartość protokołu hello **TCP**i kliknij przycisk **OK** toocreate hello reguły.

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a>Przetestować klienta Docker i hostów Azure Docker
Zlokalizuj i skopiuj hello nazwy domeny maszyny Wirtualnej, a w wierszu polecenia hello komputera klienta typu `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (gdzie *dockerextension* zastępuje hello poddomeny dla maszyny Wirtualnej).

wynik Hello powinna zostać wyświetlona toothis podobne:

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

Po zakończeniu hello powyżej kroki masz teraz funkcjonalnej hostów Docker uruchomione na maszynie Wirtualnej platformy Azure, skonfigurować toobe połączone tooremotely z innych klientów.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
Wszystko jest gotowe toogo toohello [Podręcznik użytkownika Docker] i użyć maszyny Wirtualnej platformy Docker. Jeśli tooautomate tworzenie hostów Docker na maszynach wirtualnych Azure za pomocą interfejsu wiersza polecenia, zobacz [jak toouse hello Docker rozszerzenia maszyny Wirtualnej z interfejsu wiersza polecenia platformy Azure (Azure CLI) hello]

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[jak toouse hello Docker rozszerzenia maszyny Wirtualnej z interfejsu wiersza polecenia platformy Azure (Azure CLI) hello]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[agenta systemu Linux Azure]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[systemem Docker z protokołu https]:http://docs.docker.com/articles/https/
[Podręcznik użytkownika Docker]:https://docs.docker.com/userguide/
