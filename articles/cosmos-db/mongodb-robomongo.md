---
title: "aaaUse Robomongo dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Robomongo z bazy danych Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB"
keywords: robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Użyj Robomongo z bazy danych Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB
tooan tooconnect bazy danych Azure rozwiązania Cosmos: interfejs API dla konta bazy danych MongoDB przy użyciu Robomongo, musi:

* Pobierz i zainstaluj [Robomongo](https://robomongo.org/)
* Z bazy danych rozwiązania Cosmos Azure ma: interfejsu API dla konta bazy danych MongoDB [ciąg połączenia](connect-mongodb-account.md) informacji

## <a name="connect-using-robomongo"></a>Połącz przy użyciu Robomongo
tooadd Twojego Azure DB rozwiązania Cosmos: interfejs API dla bazy danych MongoDB toohello konto połączenia bazy danych MongoDB Robomongo, wykonaj hello następujące kroki.

1. Pobieranie programu Azure DB rozwiązania Cosmos: interfejsu API, bazy danych MongoDB informacji o koncie połączenia przy użyciu instrukcji hello [tutaj](connect-mongodb-account.md).

    ![Zrzut ekranu przedstawiający blok ciągu połączenia hello](./media/mongodb-robomongo/connectionstringblade.png)
2. Uruchom *Robomongo.exe*

3. Kliknij przycisk połączenie hello w obszarze **pliku** toomanage połączenia. Następnie kliknij przycisk **Utwórz** w hello **połączenia bazy danych MongoDB** okna, które zostanie wyświetlone powitalne **ustawienia połączenia** okna.

4. W hello **ustawienia połączenia** okna, wybierz nazwę. Następnie znajdź hello **hosta** i **portu** z informacje o połączeniu w kroku 1, a następnie wprowadź je do **adres** i **portu**odpowiednio .

    ![Zrzut ekranu przedstawiający hello Robomongo Zarządzanie połączeniami](./media/mongodb-robomongo/manageconnections.png)
5. Na powitania **uwierzytelniania** , kliknij pozycję **uwierzytelniania wykonaj**. Następnie wprowadź bazy danych (domyślna to *Admin*), **nazwy użytkownika** i **hasło**.
Zarówno **nazwy użytkownika** i **hasło** znajdują się informacje o połączeniu w kroku 1.

    ![Zrzut ekranu: karta Uwierzytelnianie Robomongo hello](./media/mongodb-robomongo/authentication.png)
6. Na powitania **SSL** karcie wyboru **protokołu SSL używany**, następnie zmienić hello **metodę uwierzytelniania** za**certyfikatu z podpisem własnym**.

    ![Zrzut ekranu przedstawiający hello Robomongo kartę protokołu SSL](./media/mongodb-robomongo/SSL.png)
7. Na koniec kliknij **testu** tooverify następnie są możliwe tooconnect **zapisać**.

## <a name="next-steps"></a>Następne kroki
* Zapoznaj się z rozwiązania Cosmos Azure DB: Interfejs API, bazy danych mongodb [przykłady](mongodb-samples.md).
