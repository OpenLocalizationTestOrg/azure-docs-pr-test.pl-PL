---
title: "wprowadzenie do usługi Azure Service Fabric i Azure CLI 2.0 aaaGet"
description: "Dowiedz się, jak toouse hello Azure Service Fabric polecenia moduł w Azure CLI w wersji 2.0. Dowiedz się, jak tooconnect tooa klastra i w jaki sposób toomanage aplikacji."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a>Usługa Azure Service Fabric i interfejs wiersza polecenia platformy Azure 2.0

Witaj narzędzia wiersza polecenia platformy Azure (Azure CLI) w wersji 2.0 obejmuje toohelp polecenia Zarządzanie klastrami usługi sieć szkieletowa usług Azure. Dowiedz się, jak tooget pracę z wiersza polecenia platformy Azure i sieci szkieletowej usług.

## <a name="install-azure-cli-20"></a>Instalowanie interfejsu wiersza polecenia platformy Azure 2.0

Można użyć toointeract poleceń Azure CLI 2.0 z i zarządzania klastrami usługi sieć szkieletowa usług. tooget hello najnowszą wersję interfejsu wiersza polecenia Azure, wykonaj hello [Azure CLI 2.0 standardowego procesu instalacji](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

Aby uzyskać więcej informacji, zobacz hello [omówienie Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="azure-cli-syntax"></a>Składnia interfejsu wiersza polecenia platformy Azure

W interfejsie wiersza polecenia platformy Azure wszystkie polecenia usługi Service Fabric mają prefiks `az sf`. Aby uzyskać ogólne informacje o poleceniach hello można użyć, należy użyć `az sf -h`. Aby uzyskać pomoc dotyczącą pojedynczego polecenia, użyj polecenia `az sf <command> -h`.

Polecenia usługi Service Fabric w interfejsie wiersza polecenia platformy Azure są zgodne z następującym wzorcem nazewnictwa:

```azurecli
az sf <object> <action>
```

`<object>`element docelowy hello dla `<action>`.

## <a name="select-a-cluster"></a>Wybieranie klastra

Przed wykonaniem jakichkolwiek operacji, należy wybrać tooconnect klastra, aby. Na przykład zobacz hello następującego kodu. Kod Hello łączy tooan niezabezpieczona klastra.

> [!WARNING]
> Nie używaj niezabezpieczonych klastrów usługi Service Fabric w środowisku produkcyjnym.

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

Witaj punktu końcowego klastra musi być poprzedzony `http` lub `https`. Musi on zawierać portu hello hello HTTP bramy. adres i Hello port są hello taka sama, jak hello adres URL Eksploratora usługi sieć szkieletowa.

W przypadku klastrów zabezpieczonych za pomocą certyfikatu można użyć niezaszyfrowanych plików PEM albo plików CRT i KEY. Na przykład:

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Aby uzyskać więcej informacji, zobacz [bezpiecznego klastra sieci szkieletowej usług Azure Connect tooa](service-fabric-connect-to-secure-cluster.md).

> [!NOTE]
> Witaj `select` polecenia nie działają na wszystkie żądania przed zwróceniem. tooverify, że klaster został podany poprawnie, należy użyć wiersza polecenia, takich jak `az sf cluster health`. Upewnij się, że polecenie hello nie zwraca żadnych błędów.

## <a name="basic-operations"></a>Operacje podstawowe

Informacje o połączeniu klastra są utrwalane w wielu sesjach interfejsu wiersza polecenia platformy Azure. Po wybraniu klastra sieci szkieletowej usług można uruchomić w klastrze hello dowolne polecenie sieci szkieletowej usług.

Na przykład hello tooget stan kondycji klastra usługi sieć szkieletowa, użyj hello następujące polecenie:

```azurecli
az sf cluster health
```

polecenie Hello wyniki hello następujących danych wyjściowych (przy założeniu, że dane wyjściowe JSON jest określona w konfiguracji interfejsu wiersza polecenia Azure hello):

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a>Porady i rozwiązywanie problemów

Może się okazać hello następujące informacje przydatne, jeśli wystąpiły problemy podczas używania poleceń usługi Service Fabric w wiersza polecenia platformy Azure.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Konwertuj certyfikatu z formatu tooPEM PFX

Interfejs wiersza polecenia platformy Azure obsługuje certyfikaty po stronie klienta w postaci plików PEM (rozszerzenie pem). Jeśli używasz pliki PFX z systemu Windows, należy przekonwertować format tooPEM tych certyfikatów. tooconvert pliku PEM tooa pliku PFX, należy użyć hello następujące polecenie:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Aby uzyskać więcej informacji, zobacz hello [dokumentacji biblioteki OpenSSL](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Problemy z połączeniem

Niektóre operacje może generować następujące wiadomość hello:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Sprawdź, czy określona hello tego punktu końcowego klastra jest dostępny i nasłuchuje. Sprawdź także, że powitalne interfejsu użytkownika Eksploratora sieci szkieletowej usług jest dostępna na hosta i portu. punkt końcowy z hello tooupdate, użyj `az sf cluster select`.

### <a name="detailed-logs"></a>Szczegółowe dzienniki

Szczegółowe dzienniki często bywają przydatne w przypadku debugowania lub zgłaszania problemu. Interfejs wiersza polecenia platformy Azure oferuje globalnym `--debug` flagi, które zwiększa poziom szczegółowości hello plików dziennika.

### <a name="command-help-and-syntax"></a>Polecenia — pomoc i składnia

Wykonaj polecenia usługi sieć szkieletowa hello tej samej Konwencji jako wiersza polecenia platformy Azure. Aby uzyskać pomoc dotyczącą określonego polecenia lub grupy poleceń, użyj hello `-h` flagi:

```azurecli
az sf application -h
```

Oto inny przykład:

```azurecli
az sf application create -h
```
