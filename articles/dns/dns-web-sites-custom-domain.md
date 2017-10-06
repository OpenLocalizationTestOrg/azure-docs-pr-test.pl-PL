---
title: "aaaCreate niestandardowych rekordów DNS dla aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Jak toocreate niestandardową domenę DNS rekordów dla aplikacji sieci web przy użyciu usługi Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a>Utwórz rekordy DNS dla aplikacji sieci web w domenę niestandardową

Można użyć usługi Azure DNS toohost domeny niestandardowej dla aplikacji sieci web. Na przykład tworzysz aplikację sieci web platformy Azure i mają tooaccess Twojego użytkowników albo jej przy użyciu contoso.com lub www.contoso.com jako nazwy FQDN.

toodo, ma dwa rekordy toocreate:

* Główny "A" toocontoso.com wskazujące rekordów
* "CNAME" rekordu dla hello www nazwę, która wskazuje toohello rekordu

Należy pamiętać, że w przypadku utworzenia rekordu A dla aplikacji sieci web na platformie Azure, powitalne rekord należy ręcznie zaktualizować Jeśli hello źródłowy adres IP dla zmian aplikacji sieci web hello.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Przed rozpoczęciem, najpierw musisz utworzyć strefę DNS w usłudze Azure DNS i delegowanie strefy hello w tooAzure Twojego rejestratora DNS.

1. toocreate strefy DNS, wykonaj kroki hello w [utworzyć strefę DNS](dns-getstarted-create-dnszone.md).
2. toodelegate Twojego tooAzure DNS DNS, wykonaj kroki hello w [Delegowanie domeny DNS](dns-domain-delegation.md).

Po utworzeniu strefy i delegowanie go tooAzure DNS, następnie możesz utworzyć rekordów dla domeny niestandardowej.

## <a name="1-create-an-a-record-for-your-custom-domain"></a>1. Tworzenie rekordu A dla domeny niestandardowej

Rekord jest używane toomap adresu IP tooits nazwy. W hello poniższy przykład przypisze możemy w jako tooan rekord A adres IPv4:

### <a name="step-1"></a>Krok 1

Utwórz rekord a. i przypisz tooa $rs zmiennej

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a>Krok 2

Dodawanie zestawu rekordów hello IPv4 wartość toohello wcześniej utworzony "@" przy użyciu zmiennej hello $rs przypisane. Witaj przypisaną wartość IPv4 będzie hello adresu IP dla aplikacji sieci web.

adres IP hello toofind dla aplikacji sieci web, wykonaj kroki hello w [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a>Krok 3

Zatwierdź hello zestawu rekordów toohello zmiany. Użyj `Set-AzureRMDnsRecordSet` tooupload hello zmienia toohello tooAzure zestawu rekordów DNS:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a>2. Utwórz rekord CNAME dla domeny niestandardowej

Jeśli domena jest już zarządzany przez usługę Azure DNS (zobacz [Delegowanie domeny DNS](dns-domain-delegation.md), można użyć następującego toocreate przykład hello rekord CNAME dla contoso.azurewebsites.net hello.

### <a name="step-1"></a>Krok 1

Otwórz program PowerShell i Utwórz nowy zestaw rekordów CNAME i przypisać tooa $rs zmiennej. W tym przykładzie spowoduje utworzenie zestawu rekordów typu CNAME "czas toolive" 600 sekund w strefie DNS o nazwie "contoso.com".

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

Poniższy przykład Hello jest hello odpowiedzi.

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Krok 2

Po utworzeniu zestawu rekordów CNAME hello należy toocreate wartość aliasu jest wskazujących toohello aplikacji sieci web.

Przy użyciu hello przypisane wcześniej zmiennej "$rs" można użyć aliasu hello toocreate hello poniższe polecenie programu PowerShell dla contoso.azurewebsites.net aplikacji sieci web hello.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

Poniższy przykład Hello jest hello odpowiedzi.

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Krok 3

Zatwierdź zmiany hello przy użyciu hello `Set-AzureRMDnsRecordSet` polecenia cmdlet:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

Możesz to sprawdzić hello rekord został utworzony prawidłowo badając hello "www.contoso.com" za pomocą polecenia nslookup, jak pokazano poniżej:

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a>Utwórz rekord "awverify" dla aplikacji sieci web

Jeśli zdecydujesz toouse rekordu A dla aplikacji sieci web, można musi przejść przez tooensure procesu weryfikacji można hello własnej domeny niestandardowej. Ten krok weryfikacji jest realizowane przez utworzenie rekordu CNAME specjalne o nazwie "awverify". Ta sekcja dotyczy tylko tooA rekordy.

### <a name="step-1"></a>Krok 1

Utwórz rekord "awverify" hello. W poniższym przykładzie hello zostanie utworzony rekord "aweverify" hello własność tooverify contoso.com hello domeny niestandardowej.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

Poniższy przykład Hello jest hello odpowiedzi.

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Krok 2

Po utworzeniu zestawu rekordów hello "awverify" przypisać rekord CNAME hello ustawić alias. W poniższym przykładzie hello możemy przypisze tooawverify.contoso.azurewebsites.net alias zestawu rekordów CNAMe hello.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

Poniższy przykład Hello jest hello odpowiedzi.

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Krok 3

Zatwierdź zmiany hello przy użyciu hello `Set-AzureRMDnsRecordSet cmdlet`, jak pokazano w poniższym polecenie hello.

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a>Następne kroki

Wykonaj kroki hello w [Konfigurowanie niestandardowej nazwy domeny dla usługi App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure toouse aplikacji sieci web domeny niestandardowej.
