---
title: "wprowadzenie do usługi Azure Service Fabric interfejsu wiersza polecenia XPlat aaaGetting"
description: "Wprowadzenie do korzystania z usługi Azure Service Fabric interfejsu wiersza polecenia XPlat"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a>Przy użyciu interfejsu wiersza polecenia XPlat toointeract hello z klastra sieci szkieletowej usług

Zakłócają klastra sieci szkieletowej usług z maszyn z systemem Linux przy użyciu interfejsu wiersza polecenia XPlat hello w systemie Linux.

pierwszym krokiem Hello jest pobrać najnowszą wersję hello hello interfejsu wiersza polecenia z hello git rep i zestaw hello go w ścieżce za pomocą następującego polecenia:

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

Dla każdego polecenia obsługuje, można wpisać nazwę hello hello polecenia tooobtain hello pomocy dla tego polecenia.
Automatyczne uzupełnianie jest obsługiwane w przypadku hello poleceń. Na przykład powitania po pomocy dla poleceń aplikacji hello oferuje polecenia. 

```sh
 azure servicefabric application 
```

Hello pomocy tooa danego polecenia, można dodatkowo filtrować jako powitania po przykładzie:

```sh
 azure servicefabric application  create
```

tooenable automatycznego uzupełniania w hello interfejsu wiersza polecenia, uruchom następujące polecenia hello:

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

Hello następujących poleceń połączyć toohello klastra i Pokaż hello węzłów w klastrze hello:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

toouse nazwanych parametrów i Znajdź, jakie są, można wpisać — pomoc po użyciu polecenia. Na przykład:

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

Podczas łączenia tooa obsługi wielu komputerów klastra na komputerze **oznacza to nie jest częścią klastra hello**, użyj następującego polecenia hello:

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

Zamień hello PublicIPorFQDN tag hello rzeczywistych adres IP lub nazwa FQDN zależnie od potrzeb. Podczas łączenia tooa obsługi wielu komputerów klastra na komputerze **będącego częścią klastra hello**, użyj następującego polecenia hello:

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

Można użyć programu PowerShell lub interfejsu wiersza polecenia toointeract z klastra sieci szkieletowej usług z systemem Linux został utworzony za pomocą hello portalu Azure.

> [!WARNING]
> Tych klastrów nie są bezpieczne, w związku z tym może być otwierasz się jeden — okno przez dodanie hello publicznego adresu IP w manifeście klastra hello.

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a>Przy użyciu hello klastra sieci szkieletowej usług tooa tooconnect interfejsu wiersza polecenia XPlat

Witaj następującego polecenia wiersza polecenia platformy Azure opisano, jak tooconnect tooa zabezpieczyć klastra. Szczegóły certyfikatu Hello zgodny z certyfikatem w węzłach klastra hello.

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

Jeśli certyfikat ma urzędy certyfikacji (CA), należy tooadd hello — urzędu certyfikacji certyfikatu ścieżki parametru jak hello poniższy przykład: 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

Jeśli masz wiele urzędów certyfikacji, należy użyć przecinka jako ogranicznik hello.

Jeśli Twoje nazwa pospolita certyfikatu hello jest niezgodny z punktu końcowego połączenia hello, można użyć parametru hello `--strict-ssl-false` toobypass hello weryfikacji, jak pokazano w hello następujące polecenie:

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

Jeśli chcesz tooskip weryfikacji hello urzędu certyfikacji, można dodać hello — Odrzuć — Dostęp nieautoryzowany — wartość false parametru pokazane na powitania następujące polecenie: 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

Po nawiązaniu połączenia, powinno być możliwe toorun innych toointeract polecenia interfejsu wiersza polecenia z hello klastra.

## <a name="deploying-your-service-fabric-application"></a>Wdrażanie aplikacji sieci szkieletowej usług

Wykonaj następujące polecenia toocopy, zarejestrować i uruchomić aplikacji sieci szkieletowej usług hello hello:

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>Uaktualnianie aplikacji

proces Hello jest podobne toohello [procesu w systemie Windows](service-fabric-application-upgrade-tutorial-powershell.md)).

Tworzenie, skopiuj zarejestrować i utworzyć aplikację z katalogu głównego projektu. Jeśli wystąpienie aplikacji ma nazwę `fabric:/MySFApp`i typ hello jest MySFApp, hello poleceń będzie następujące:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

Należy hello zmienić tooyour aplikację i skompiluj ponownie usługi hello zmodyfikowane.  Aktualizacja hello zmodyfikowane w pliku manifestu usługi (ServiceManifest.xml) hello zaktualizowane wersje na powitania usługi (i kodu lub konfiguracji lub danych, zależnie od potrzeb). Również zmodyfikować manifest aplikacji hello (ApplicationManifest.xml) za pomocą hello zaktualizować numer wersji aplikacji hello i hello modyfikacji usługi.  Teraz skopiuj i zarejestruj zaktualizowaną aplikację za pomocą hello następującego polecenia:

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

Teraz można rozpocząć uaktualniania aplikacji hello z hello następujące polecenie:

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

Teraz można monitorować przy użyciu SFX uaktualniania aplikacji hello. W ciągu kilku minut aplikacji hello czy zostały zaktualizowane. Można również skorzystać z aplikacji zaktualizowane z powodu błędu i sprawdzić funkcję wycofywania automatycznie hello w sieci szkieletowej usług.

## <a name="converting-from-pfx-toopem-and-vice-versa"></a>Konwertowanie z PFX tooPEM i na odwrót

Tooinstall certyfikat może być konieczne w klastrach bezpiecznego tooaccess komputera lokalnego (z systemem Windows lub Linux), które mogą być w innym środowisku. Na przykład podczas uzyskiwania dostępu do zabezpieczonych klaster systemu Linux na komputerze z systemem Windows i na odwrót może być konieczne tooconvert certyfikatu PFX tooPEM i na odwrót. 

tooconvert z pliku PFX tooa pliku PEM o hello Użyj następującego polecenia:

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

tooconvert z pliku tooa PEM pliku PFX, hello Użyj następującego polecenia:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Odwołuje się zbyt[dokumentacji biblioteki OpenSSL](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) szczegółowe informacje.

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>Rozwiązywanie problemów


### <a name="copying-of-hello-application-package-does-not-succeed"></a>Kopiowanie pakietu aplikacji hello nie powiedzie się

Sprawdź, czy `openssh` jest zainstalowany. Domyślnie Ubuntu pulpitu nie jest zainstalowany. Zainstaluj za pomocą hello następujące polecenie:

```sh
sudo apt-get install openssh-server openssh-client**
```

Jeśli hello problem będzie nadal występował, spróbuj wyłączyć PAM dla ssh, zmieniając hello `sshd_config` plik przy użyciu hello następującego polecenia:

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

Jeśli hello problem będzie nadal występować, spróbuj rosnący numer hello ssh sesji, wykonując następujące polecenia hello:

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

Przy użyciu kluczy ssh uwierzytelniania (w przeciwieństwie toopasswords) nie jest jeszcze obsługiwana (ponieważ platformy hello używa ssh pakiety toocopy), dlatego zamiast tego Użyj uwierzytelniania hasła.

## <a name="next-steps"></a>Następne kroki

[Konfigurowanie środowiska deweloperskiego hello i wdrożyć klaster sieci szkieletowej usług aplikacji tooa systemu Linux.](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>Pokrewne artykuły:

* [Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md) (Wprowadzenie do usługi Service Fabric i interfejsu wiersza polecenia platformy Azure 2.0)
