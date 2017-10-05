---
title: "Wprowadzenie do korzystania z usługi Azure Service Fabric interfejsu wiersza polecenia XPlat"
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
ms.openlocfilehash: ddf881f6c202a82a3f64773639aa29b660057f8d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-xplat-cli-to-interact-with-a-service-fabric-cluster"></a>Przy użyciu wiersza polecenia XPlat wchodzić w interakcje z klastra sieci szkieletowej usług

Zakłócają klastra sieci szkieletowej usług z maszyn z systemem Linux przy użyciu wiersza polecenia XPlat w systemie Linux.

Pierwszym krokiem jest Pobierz najnowszą wersję interfejsu wiersza polecenia z git rep i skonfigurować ją w ścieżce przy użyciu następujących poleceń:

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

Dla każdego polecenia obsługuje, można wpisać nazwę polecenia, aby uzyskać pomoc dotyczącą tego polecenia.
Automatyczne uzupełnianie jest obsługiwana dla polecenia. Na przykład następujące polecenie zapewnia pomoc dla poleceń aplikacji. 

```sh
 azure servicefabric application 
```

Można dokładniej przefiltrować ułatwiają danego polecenia, jak przedstawiono na poniższym przykładzie:

```sh
 azure servicefabric application  create
```

Aby włączyć automatyczne uzupełnianie w interfejsu wiersza polecenia, uruchom następujące polecenia:

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

Poniższe polecenia, połącz się z klastrem i wyświetlić węzły w klastrze:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

Parametry nazwane i Znajdź, jakie są, możesz wpisać — pomoc po użyciu polecenia. Na przykład:

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

Podczas nawiązywania połączenia z maszyną klastrze z wieloma maszynami **oznacza to nie jest częścią klastra**, użyj następującego polecenia:

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

Zamień PublicIPorFQDN tag rzeczywistych adres IP lub nazwa FQDN zależnie od potrzeb. Podczas nawiązywania połączenia z maszyną klastrze z wieloma maszynami **będącego częścią klastra**, użyj następującego polecenia:

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

Możesz użyć programu PowerShell lub interfejsu wiersza polecenia do interakcji z klastra sieci szkieletowej usług z systemem Linux został utworzony za pomocą portalu Azure.

> [!WARNING]
> Tych klastrów nie są bezpieczne, w związku z tym można może być otwarcia jednego — okno przez dodanie publicznego adresu IP w manifeście klastra.

## <a name="using-the-xplat-cli-to-connect-to-a-service-fabric-cluster"></a>Przy użyciu wiersza polecenia XPlat do nawiązania połączenia klastra sieci szkieletowej usług

Następujące polecenia interfejsu wiersza polecenia Azure opisują sposób podłączania do bezpiecznego klastra. Szczegóły certyfikatu musi odpowiadać certyfikatu w węzłach klastra.

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

Jeśli certyfikat ma urzędy certyfikacji (CA), należy dodać parametr — urzędu certyfikacji certyfikatu ścieżki, jak w następującym przykładzie: 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

Jeśli masz wiele urzędów certyfikacji, należy użyć przecinka jako ogranicznik.

Jeśli Twoje nazwa pospolita w certyfikacie nie odpowiada punktu końcowego połączenia, można użyć parametru `--strict-ssl-false` do pominięcia weryfikacji, jak pokazano w poniższym poleceniu:

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

Jeśli chcesz pominąć weryfikacji urzędu certyfikacji, można dodać parametr Odrzuć — Dostęp nieautoryzowany — wartość false, jak pokazano w poniższym poleceniu: 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

Po nawiązaniu połączenia można innych poleceń interfejsu wiersza polecenia w celu wchodzenia w interakcje z klastrem.

## <a name="deploying-your-service-fabric-application"></a>Wdrażanie aplikacji sieci szkieletowej usług

Wykonaj następujące polecenia, aby skopiować, zarejestrować i uruchomić aplikacji sieci szkieletowej usług:

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>Uaktualnianie aplikacji

Proces jest podobny do [procesu w systemie Windows](service-fabric-application-upgrade-tutorial-powershell.md)).

Tworzenie, skopiuj zarejestrować i utworzyć aplikację z katalogu głównego projektu. Jeśli wystąpienie aplikacji ma nazwę `fabric:/MySFApp`, a typ to MySFApp, polecenia zostaną wyświetlone następujące:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

Wprowadź zmiany w aplikacji i skompiluj ponownie zmodyfikowaną usługę.  Zaktualizuj usługę zmodyfikowanego pliku manifestu (ServiceManifest.xml) z zaktualizowane wersje usługi (i kodu ani konfiguracji lub danych, zależnie od potrzeb). Numer zaktualizowaną wersję aplikacji i modyfikacji usługi również zmodyfikować manifest aplikacji (pliku ApplicationManifest.xml).  Teraz skopiuj i zarejestruj zaktualizowaną aplikację za pomocą następujących poleceń:

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

Teraz można rozpocząć uaktualniania aplikacji przy użyciu następującego polecenia:

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

Teraz można monitorować przy użyciu SFX uaktualnienie aplikacji. W ciągu kilku minut aplikacja zostanie zaktualizowana. Można również skorzystać z aplikacji zaktualizowane z powodu błędu i sprawdzić funkcji automatycznego wycofania w sieci szkieletowej usług.

## <a name="converting-from-pfx-to-pem-and-vice-versa"></a>Konwertowanie z PFX PEM i na odwrót

Może być konieczne do bezpiecznych klastrów, które mogą być w innym środowisku należy zainstalować certyfikat w komputerze lokalnym (z systemem Windows lub Linux). Na przykład podczas uzyskiwania dostępu do zabezpieczonych klaster systemu Linux na komputerze z systemem Windows i na odwrót może być konieczne konwertowanie certyfikatu PFX do PEM i na odwrót. 

Aby dokonać konwersji pliku PEM, do pliku PFX, użyj następującego polecenia:

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

Aby przekonwertować plik PFX na plik PEM, użyj następującego polecenia:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Aby uzyskać szczegółowe informacje, zapoznaj się z [dokumentacją rozwiązania OpenSSL](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html).

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>Rozwiązywanie problemów


### <a name="copying-of-the-application-package-does-not-succeed"></a>Kopiowanie pakietu aplikacji nie powiedzie się

Sprawdź, czy `openssh` jest zainstalowany. Domyślnie Ubuntu pulpitu nie jest zainstalowany. Zainstaluj za pomocą następującego polecenia:

```sh
sudo apt-get install openssh-server openssh-client**
```

Jeśli problem będzie się powtarzał, spróbuj wyłączyć PAM dla ssh, zmieniając `sshd_config` plik za pomocą następujących poleceń:

```sh
sudo vi /etc/ssh/sshd_config
#Change the line with UsePAM to the following: UsePAM no
sudo service sshd reload
```

Jeśli problem będzie nadal występować, spróbuj zwiększyć liczbę ssh sesji, wykonując następujące polecenia:

```sh
sudo vi /etc/ssh/sshd\_config
# Add the following to lines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

Przy użyciu kluczy dla ssh uwierzytelniania (w przeciwieństwie do hasła) nie jest jeszcze obsługiwana (ponieważ platformy używa ssh można kopiować pakiety), dlatego zamiast tego Użyj uwierzytelniania hasła.

## <a name="next-steps"></a>Następne kroki

[Konfigurowanie środowiska projektowego i wdrażanie aplikacji sieci szkieletowej usług do klastra z systemem Linux.](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>Pokrewne artykuły:

* [Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md) (Wprowadzenie do usługi Service Fabric i interfejsu wiersza polecenia platformy Azure 2.0)
