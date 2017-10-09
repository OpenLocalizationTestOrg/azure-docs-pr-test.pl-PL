---
title: "tooAzure aaaConnect usług Analysis Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect tooand pobrać dane z serwera usług Analysis Services na platformie Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a>Połączyć z serwerem usług Azure Analysis Services tooan

W tym artykule opisano serwer łączący tooa za pomocą modelowania danych i zarządzania aplikacji, takich jak SQL Server Management Studio (SSMS) lub SQL Server Data Tools (SSDT). Lub z klientem raportowanie aplikacji, takich jak program Microsoft Excel, Power BI Desktop lub niestandardowych aplikacji. Usługi Analysis Services tooAzure połączeń używać protokołu HTTPS.

## <a name="client-libraries"></a>Biblioteki klienckie
[Pobierz najnowsze bibliotek klienckich hello](analysis-services-data-providers.md)

Wszystkie połączenia serwera tooa, niezależnie od tego typu, wymagają zaktualizowanej AMO, ADOMD.NET i OLEDB biblioteki tooconnect tooand interfejsu klienta z serwerem usług Analysis Services. Dla narzędzia SSMS, narzędzi SSDT Excel 2016 i usługi Power BI bibliotek klienckich najnowsze hello są zainstalowane lub zaktualizowane wersje miesięcznych. Jednak w niektórych przypadkach jest aplikacja nie może mieć hello najnowsza wersja. Na przykład podczas aktualizacji opóźnienie zasad lub aktualizacji usługi Office 365 są na powitania kanału opóźnieniem.

## <a name="server-name"></a>Nazwa serwera

Podczas tworzenia serwera usług Analysis Services na platformie Azure, należy określić unikatowy region nazwy i hello której serwer hello jest toobe utworzony. Podczas określania nazwy serwera hello na połączenie, jest schemat nazewnictwa powitania serwera:

```
<protocol>://<region>/<servername>
```
 Gdy protokół jest ciągiem **asazure**, region jest hello identyfikatora Uri, której utworzono powitania serwera (na przykład westus.asazure.windows.net) i servername jest nazwą powitania serwera unikatowy w obrębie regionu hello.

### <a name="get-hello-server-name"></a>Pobierz nazwę serwera hello
W **portalu Azure** > serwera > **omówienie** > **nazwy serwera**, nazwa całego serwera hello kopii. Inni użytkownicy w organizacji za łączenia toothis serwera, można udostępniać tę nazwę serwera z nimi. Podczas określania nazwy serwera, należy użyć hello pełną ścieżkę.

![Pobieranie nazwy serwera z systemu Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a>Parametry połączenia

Podczas nawiązywania połączenia tooAzure Analysis Services przy użyciu hello tabelaryczny Model obiektów, użyj hello następujące formaty ciągu połączenia:

###### <a name="integrated-azure-active-directory-authentication"></a>Zintegrowane uwierzytelnianie usługi Azure Active Directory
Uwierzytelnianie zintegrowane przejmuje hello pamięci podręcznej poświadczeń usługi Azure Active Directory. Jeśli jest dostępna. Jeśli nie jest wyświetlane okno logowania do platformy Azure hello.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a>Azure uwierzytelniania usługi Active Directory za pomocą nazwy użytkownika i hasła

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a>Uwierzytelnianie systemu Windows (zintegrowane zabezpieczenia)
Użyj konta systemu Windows hello systemem hello bieżącego procesu.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a>Połącz, używając pliku odc
W starszych wersjach programu Excel użytkownicy mogą łączyć tooan usług Azure Analysis Services serwera przy użyciu pliku połączenia danych pakietu Office (odc). toolearn więcej, zobacz [Tworzenie pliku połączenia danych pakietu Office (odc)](analysis-services-odc.md).


## <a name="next-steps"></a>Następne kroki
[Połącz przy użyciu programu Excel](analysis-services-connect-excel.md)    
[Uzyskuj dostęp do usługi Power BI](analysis-services-connect-pbi.md)   
[Zarządzanie serwerem](analysis-services-manage.md)   

