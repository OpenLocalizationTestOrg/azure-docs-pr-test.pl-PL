---
title: tooconfigure aaaHow aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate Konfiguruj aplikację serwera Proxy aplikacji w kilku prostych krokach"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a>Jak tooconfigure aplikacji serwera Proxy aplikacji

W tym artykule pomocy toounderstand jak tooconfigure aplikację serwera Proxy aplikacji w usłudze Azure AD tooexpose Twojego toohello aplikacji lokalnej w chmurze.

## <a name="recommended-documents"></a>Zalecane dokumenty 

toolearn o hello początkowej konfiguracji i tworzenia aplikacji serwera Proxy aplikacji za pośrednictwem portalu administracyjnego hello wykonaj hello [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Aby uzyskać więcej informacji na temat konfigurowania łączników, zobacz [Włączanie serwera Proxy aplikacji w portalu Azure hello](active-directory-application-proxy-enable.md).

Aby uzyskać informacje na przekazywanie certyfikatów i przy użyciu domen niestandardowych, zobacz [Praca z domenami niestandardowymi w serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).

## <a name="create-hello-applicationsetting-hello-urls"></a>Utwórz hello adresy URL hello ustawienie/aplikacji

Jeśli wykonujesz hello etapami hello [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) dokumentacji i czy wprowadzenie błąd podczas tworzenia aplikacji hello, zobacz szczegóły błędu hello informacji i sugestie na temat Aplikacja hello toofix. Większość komunikaty o błędach obejmują sugerowanej poprawki. Sprawdź tooavoid typowych błędów:

-   Administratorzy z toocreate uprawnienia aplikacji serwera Proxy aplikacji

-   wewnętrzny adres URL Hello jest unikatowa

-   zewnętrzny adres URL Hello jest unikatowa

-   Witaj adresy URL rozpoczyna się od http lub https i kończyć się "/"

-   adres URL Hello powinien być nazwą domeny, a nie adres IP

komunikat o błędzie Hello powinien być wyświetlany w prawym górnym rogu hello podczas tworzenia aplikacji hello. Można również wybrać hello powiadomień ikona toosee hello komunikaty o błędach.

   ![Wiersz powiadomień](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>Konfigurowanie grup łączników/łącznika

Jeśli masz trudności w konfigurowaniu aplikacji z powodu ostrzeżenie o hello łączników i grupach łącznika, zobacz instrukcje na Włączanie serwera Proxy aplikacji, aby uzyskać więcej informacji na temat łączników toodownload. Więcej informacji na temat łączników toolearn, zobacz hello [dokumentacji łączniki](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).

Jeśli łączniki nie są aktywne, oznacza to, czy są one tooreach hello usługi. Jest to często spowodowane wszystkie hello wymagane porty nie są otwarte. toosee listę wymaganych portów zawiera sekcja wymagania wstępne hello hello włączenie dokumentacji serwera Proxy aplikacji.

## <a name="upload-certificates-for-custom-domains"></a>Przekaż certyfikaty dla domen niestandardowych

Domen niestandardowych można domeny hello toospecify Twojego zewnętrznych adresów URL. domen niestandardowych toouse, potrzebujesz tooupload hello certyfikatu dla tej domeny. Aby uzyskać informacje na temat używania domeny niestandardowej i certyfikatów, zobacz [Praca z domenami niestandardowymi w serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains). 

Pojawiły się problemy, przekazywanie certyfikatu, poszukaj komunikatów o błędach hello w portalu hello dodatkowe informacje na temat hello problem z certyfikatem hello. Typowe problemy z certyfikatem obejmują:

-   Wygaśnięcie certyfikatu

-   Certyfikat jest certyfikatem z podpisem

-   Certyfikat nie ma klucza prywatnego hello

Witaj błąd wyświetlania komunikatów w hello prawym górnym rogu jako spróbuj tooupload hello certyfikatu. Można również wybrać hello powiadomień ikona toosee hello komunikaty o błędach.

   ![Wiersz powiadomień](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>Następne kroki
[Publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](application-proxy-publish-azure-portal.md)
