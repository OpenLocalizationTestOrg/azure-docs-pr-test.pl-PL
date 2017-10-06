---
title: "zasady uwierzytelniania interfejsu API zarządzania aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zasad uwierzytelniania hello dostępne do użycia w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a>Zarządzanie interfejsami API zasady uwierzytelniania
W tym temacie znajdują się informacje na następujące zasady usługi API Management hello. Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AuthenticationPolicies"></a>Zasady uwierzytelniania  
  
-   [Uwierzytelnianie za pomocą Basic](api-management-authentication-policies.md#Basic) -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego.  
  
-   [Uwierzytelniania za pomocą certyfikatu klienta](api-management-authentication-policies.md#ClientCertificate) -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu certyfikatów klienta.  
  
##  <a name="Basic"></a>Uwierzytelniania Basic  
 Użyj hello `authentication-basic` tooauthenticate zasad z usługi wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego. Ta zasada efektywnie ustawia wartość odpowiednie poświadczenia toohello podany w zasadzie hello toohello nagłówek autoryzacji HTTP hello.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a>Przykład  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|Uwierzytelnianie — podstawowy|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|nazwa użytkownika|Określa nazwy użytkownika hello hello podstawowe poświadczenia.|Tak|Nie dotyczy|  
|hasło|Określa hasło hello hello podstawowe poświadczenia.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** dla ruchu przychodzącego  
  
-   **Zakresy zasad:** interfejsu API  
  
##  <a name="ClientCertificate"></a>Uwierzytelniania za pomocą certyfikatu klienta  
 Użyj hello `authentication-certificate` tooauthenticate zasad z usługi wewnętrznej bazy danych przy użyciu certyfikatu klienta. certyfikat Hello musi toobe [zainstalowane do interfejsu API zarządzania](http://go.microsoft.com/fwlink/?LinkID=511599) pierwszy i jest identyfikowany przez jego odcisk palca.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a>Przykład  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|certyfikat uwierzytelniania|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|Odcisk palca|Witaj odcisk palca certyfikatu klienta hello.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** dla ruchu przychodzącego  
  
-   **Zakresy zasad:** interfejsu API  
  

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).  