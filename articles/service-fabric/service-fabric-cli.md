---
title: "wprowadzenie do usługi Azure Service Fabric interfejsu wiersza polecenia (sfctl) aaaGet"
description: "Dowiedz się, jak toouse hello interfejsu wiersza polecenia Azure Service Fabric. Dowiedz się, jak tooconnect tooa klastra i w jaki sposób toomanage aplikacji."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a>Wiersz polecenia usługi Azure Service Fabric

Hello Azure Service Fabric interfejsu wiersza polecenia (sfctl) jest narzędziem wiersza polecenia interakcji i zarządzania nimi jednostki sieci szkieletowej usług Azure. Interfejs sfctl może być używany z klastrami systemu Windows lub Linux. Interfejs sfctl działa na dowolnej platformie, która obsługuje język Python.

## <a name="prerequisites"></a>Wymagania wstępne

Wcześniejsze tooinstallation, upewnij się, że w środowisku ma python oraz narzędzia pip zainstalowane. Aby uzyskać więcej informacji, zapoznaj się hello [narzędzia pip dokumentacji szybkiego startu](https://pip.pypa.io/en/latest/quickstart/)i oficjalna [python zainstalować dokumentację](https://wiki.python.org/moin/BeginnersGuide/Download).

Obsługiwane są zarówno python 2.7 i 3,6, zalecane jest python toouse 3,6.

## <a name="install"></a>Instalowanie

Hello Azure Service Fabric interfejsu wiersza polecenia (sfctl) jest dostarczana jako pakiet języka python. tooinstall hello najnowszej wersji Uruchom:

```bash
pip install sfctl
```

Po zakończeniu instalacji, uruchom `sfctl -h` tooget informacji o dostępnych poleceń.

## <a name="cli-syntax"></a>Składnia interfejsu wiersza polecenia

Polecenia mają zawsze prefiks `sfctl`. Aby uzyskać ogólne informacje na temat wszystkich poleceń, z których możesz korzystać, użyj polecenia `sfctl -h`. Aby uzyskać pomoc dotyczącą pojedynczego polecenia, użyj polecenia `sfctl <command> -h`.

Wykonaj polecenia powtarzalne struktury, z docelowym hello hello polecenia poprzedniego zlecenie hello lub akcji:

```azurecli
sfctl <object> <action>
```

W tym przykładzie `<object>` jest hello celu `<action>`.

## <a name="select-a-cluster"></a>Wybieranie klastra

Przed wykonaniem jakichkolwiek operacji, należy wybrać tooconnect klastra, aby. Na przykład uruchom powitania po tooselect i połącz toohello klastra o nazwie hello `testcluster.com`.

> [!WARNING]
> Nie używaj niezabezpieczonych klastrów usługi Service Fabric w środowisku produkcyjnym.

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

Witaj punktu końcowego klastra musi być poprzedzony `http` lub `https`. Musi on zawierać portu hello hello HTTP bramy. adres i Hello port są hello taka sama, jak hello adres URL Eksploratora usługi sieć szkieletowa.

W przypadku klastrów zabezpieczonych certyfikatem możesz określić certyfikat zakodowany w formacie PEM. certyfikat Hello można określić jako pojedynczy plik lub certyfikat i parę kluczy.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Aby uzyskać więcej informacji, zobacz [bezpiecznego klastra sieci szkieletowej usług Azure Connect tooa](service-fabric-connect-to-secure-cluster.md).

## <a name="basic-operations"></a>Operacje podstawowe

Informacje o połączeniu z klastrem są utrwalane między sesjami interfejsu sfctl. Po wybraniu klastra sieci szkieletowej usług można uruchomić w klastrze hello dowolne polecenie sieci szkieletowej usług.

Na przykład hello tooget stan kondycji klastra usługi sieć szkieletowa, użyj hello następujące polecenie:

```azurecli
sfctl cluster health
```

polecenie Hello wyniki hello następujące dane wyjściowe:

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

Kilka sugestii i porad dotyczących rozwiązywania typowych problemów.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Konwertuj certyfikatu z formatu tooPEM PFX

Hello interfejsu wiersza polecenia usługi sieć szkieletowa obsługuje certyfikaty klienta jako pliki PEM (rozszerzenie PEM). Jeśli używasz pliki PFX z systemu Windows, należy przekonwertować format tooPEM tych certyfikatów. tooconvert pliku PEM tooa pliku PFX, użyj następującego polecenia:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Aby uzyskać więcej informacji, zobacz hello [dokumentacji biblioteki OpenSSL](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Problemy z połączeniem

Niektóre operacje może generować następujące wiadomość hello:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Sprawdź, czy określona hello tego punktu końcowego klastra jest dostępny i nasłuchuje. Sprawdź także, że powitalne interfejsu użytkownika Eksploratora sieci szkieletowej usług jest dostępna na hosta i portu. punkt końcowy z hello tooupdate, użyj `sfctl cluster select`.

### <a name="detailed-logs"></a>Szczegółowe dzienniki

Szczegółowe dzienniki często bywają przydatne w przypadku debugowania lub zgłaszania problemu. Brak globalnym `--debug` flagi, które zwiększa poziom szczegółowości hello plików dziennika.

### <a name="command-help-and-syntax"></a>Polecenia — pomoc i składnia

Aby uzyskać pomoc dotyczącą określonego polecenia lub grupy poleceń, użyj hello `-h` flagi:

```azurecli
sfctl application -h
```

Inny przykład:

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a>Następne kroki

* [Wdrażanie aplikacji przy użyciu interfejsu wiersza polecenia Azure Service Fabric hello](service-fabric-application-lifecycle-sfctl.md)
* [Wprowadzenie do usługi Service Fabric w systemie Linux](service-fabric-get-started-linux.md)
