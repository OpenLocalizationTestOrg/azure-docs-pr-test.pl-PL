---
title: "z pakiet integracyjny dla przedsiębiorstw przy użyciu certyfikatów aaaUsing | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse certyfikaty z hello pakiet integracyjny dla przedsiębiorstw | Aplikacje logiki platformy Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a>Informacje na temat certyfikatów i pakietu integracyjnego dla przedsiębiorstw
## <a name="overview"></a>Omówienie
Integracja przedsiębiorstwa używa komunikacji B2B toosecure certyfikatów. Można użyć dwóch typów certyfikatów, w aplikacjach integracji przedsiębiorstwa:

* Certyfikaty publiczne, które muszą być zakupione od urzędu certyfikacji (CA).
* Certyfikaty prywatne, które można wystawić samodzielnie. Te certyfikaty są czasami określonego tooas certyfikaty z podpisem własnym.

## <a name="what-are-certificates"></a>Co to są certyfikaty?
Certyfikaty są cyfrowe dokumentów, który zweryfikować tożsamość hello hello uczestników łączności elektronicznej i który również bezpieczna komunikacja elektronicznej.

## <a name="why-use-certificates"></a>Dlaczego warto używać certyfikatów?
Czasami komunikacji B2B musi poufne. Integracji przedsiębiorstwa używa certyfikatów toosecure otrzymywania tych wiadomości na dwa sposoby:

* Szyfrując hello zawartość wiadomości
* Przez cyfrowego podpisywania wiadomości  

## <a name="upload-a-public-certificate"></a>Przekaż certyfikat publiczny

toouse *certyfikatu publicznego* w aplikacjach logiki z możliwościami B2B, najpierw tooupload hello certyfikatu do konta integracji.  

Po przekazaniu certyfikat jest dostępny toohelp zabezpieczenia wiadomości B2B podczas definiowania ich właściwości w hello [umowy](logic-apps-enterprise-integration-agreements.md) utworzony.  

Poniżej przedstawiono szczegółowe informacje na temat przekazywania certyfikaty publiczne na koncie integracji, po zalogowaniu w portalu Azure toohello hello:

1. Wybierz **więcej usług** , a następnie wprowadź **integracji** w polu wyszukiwania hello filtru. Wybierz **konta integracji** z hello listy wyników     
![Wybierz opcję Przeglądaj](media/logic-apps-enterprise-integration-certificates/overview-1.png)  
2. Wybierz toowhich konta integracji hello ma tooadd hello certyfikatu.  
![Wybierz toowhich konta integracji hello ma tooadd hello certyfikatu](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. Wybierz hello **certyfikaty** kafelka.  
![Certyfikaty hello wybierz Kafelek](media/logic-apps-enterprise-integration-certificates/certificate-1.png)
4. W hello **certyfikaty** bloku, który zostanie otwarty, wybierz hello **Dodaj** przycisku.   
![Kliknij przycisk Dodaj hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
5. Wprowadź **nazwa** dla certyfikatu, a następnie wybierz opcję hello typ certyfikatu jako **publicznego** z listy rozwijanej hello.  
6. Ikona folderu wybierz powitania po prawej stronie powitania hello **certyfikatu** pola tekstowego. Po otwarciu hello selektor plików, Znajdź i wybierz plik certyfikatu hello, które mają tooupload tooyour integracji konta.
7. Wybierz certyfikat hello, a następnie wybierz **OK** w hello selektor plików. Weryfikuje i przekazuje hello certyfikatu tooyour integracji konta.
8. Na koniec kopii na powitania **Dodaj certyfikat** bloku, wybierz hello **OK** przycisku.  
![Wybierz przycisk OK hello](media/logic-apps-enterprise-integration-certificates/certificate-3.png)  
9. Wybierz hello **certyfikaty** kafelka. Powinien pojawić się hello nowo dodany certyfikat.  
![Zobacz hello nowego certyfikatu](media/logic-apps-enterprise-integration-certificates/certificate-4.png)  

## <a name="upload-a-private-certificate"></a>Przekaż certyfikat prywatny

toouse *certyfikatu prywatnego* w aplikacjach logiki z możliwościami B2B, możesz przekazać konto integracji tooyour certyfikatu prywatnego przez pobieranie hello następujące kroki

1. [Przekaż sieci prywatnej tooKey klucza magazynu](../key-vault/key-vault-get-started.md "więcej informacji na temat usługi Key Vault") i podaj **nazwa klucza** 
   
   > [!TIP]
   > Musisz autoryzować Logic Apps tooperform operacje magazynu kluczy. Jednostki usługi Logic Apps toohello dostępu można przyznać za pomocą następującego polecenia programu PowerShell hello:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`  
   > 
   > 

Po hello w poprzednim kroku, należy dodać konto toointegration certyfikatu prywatnego.

Poniżej są hello szczegółowe informacje na temat przekazywania prywatnej certyfikaty do konta integracji, po zalogowaniu toohello portalu Azure:  
 
1. Wybierz hello integracji konta toowhich tooadd hello certyfikatu a wybrać hello **certyfikaty** kafelka.  
![Certyfikaty hello wybierz Kafelek](media/logic-apps-enterprise-integration-certificates/certificate-1.png)  
2. W hello **certyfikaty** bloku, który zostanie otwarty, wybierz hello **Dodaj** przycisku.   
![Kliknij przycisk Dodaj hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
3. Wprowadź **nazwa** dla certyfikatu, a typ certyfikatu wybierz hello jako **prywatnej** z listy rozwijanej hello.   
4. Wybierz ikonę folder hello na powitania po prawej stronie powitania **certyfikatu** pola tekstowego. Po otwarciu selektor plików hello znaleźć hello odpowiedniego certyfikatu publicznego, które mają tooupload tooyour integracji konta.   
   
   > [!Note]
   > Podczas dodawania certyfikatu prywatnego jest ważne, tooadd odpowiadającego publicznego certyfikatu tooshow w [umowy AS2](logic-apps-enterprise-integration-as2.md) odbierania i wysyłania ustawień podpisywania i szyfrowania wiadomości powitania.
   > 
   >   

5. Wybierz hello **grupy zasobów**, **Key Vault**, **nazwa klucza** i wybierz hello **OK** przycisku.  
![Dodawanie certyfikatu](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)  
6. Wybierz hello **certyfikaty** kafelka. Powinien pojawić się hello nowo dodany certyfikat.
![Zobacz hello nowego certyfikatu](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)  



* [Tworzenie umowy z B2B](logic-apps-enterprise-integration-agreements.md)  
* [Dowiedz się więcej na temat usługi Key Vault](../key-vault/key-vault-get-started.md "więcej informacji na temat usługi Key Vault")  

