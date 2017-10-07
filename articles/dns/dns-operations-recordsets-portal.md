---
title: "rekord aaaManage DNS zestawów rekordów i rekordów z usługi Azure DNS | Dokumentacja firmy Microsoft"
description: "Usługa Azure DNS zawiera rekord DNS toomanage możliwości hello ustawia i rejestruje podczas hosting domeny."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a>Zarządzanie zestawów rekordów i rekordami DNS za pomocą hello portalu Azure

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

W tym artykule opisano, jak toomanage zestawów rekordów i rekordów dla strefy DNS przy użyciu hello portalu Azure.

Jest ważne toounderstand hello różnica między zestawów rekordów DNS i poszczególnych rekordów DNS. Zestaw rekordów jest kolekcją rekordów w strefie, które mają hello takie same nazwy i są hello tego samego typu. Aby uzyskać więcej informacji, zobacz [DNS Utwórz zestawów rekordów i rekordów przy użyciu portalu Azure hello](dns-getstarted-create-recordset-portal.md).

## <a name="create-a-new-record-set-and-record"></a>Tworzenie nowego zestawu rekordów i rekordu

toocreate rekord w hello portalu Azure, zobacz [rekordy DNS utworzyć przy użyciu hello portalu Azure](dns-getstarted-create-recordset-portal.md).

## <a name="view-a-record-set"></a>Wyświetl zestaw rekordów

1. W hello portalu Azure, przejdź do pozycji toohello **strefy DNS** bloku.
2. Wyszukaj hello zestawu rekordów i zaznacz go. Spowoduje to otwarcie hello właściwości zestawu rekordów.

    ![Wyszukiwanie zestawu rekordów](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a>Dodaj nowy zestaw rekordów tooa rekordów

Możesz dodać too20 rekordów tooany rekordów zestawu. Zestaw rekordów nie może zawierać dwa identyczne rekordy. Pusty zestawami rekordów (o zerowej rekordów) mogą być tworzone, ale nie są wyświetlane na serwery hello Azure DNS. Zestawy rekordów typu CNAME może zawierać co najwyżej jeden rekord.

1. Na powitania **właściwości zestawu rekordów** bloku dla swojej strefy DNS, kliknij przycisk Rejestruj hello ustawić mają tooadd rekord.

    ![Wybierz zestaw rekordów](./media/dns-operations-recordsets-portal/selectset500.png)

2. Określ zestawu rekordów hello właściwości wypełniając hello pola.

    ![Dodaj rekord](./media/dns-operations-recordsets-portal/addrecord500.png)

3. Kliknij przycisk **zapisać** na hello początku hello toosave bloku ustawienia. Następnie zamknij hello bloku.
4. Hello ekranu pojawi się zapisuje hello rekordu.

    ![Zapisywanie zestawu rekordów](./media/dns-operations-recordsets-portal/saving150.png)

Po zapisaniu rekordu hello hello wartości na powitania **strefy DNS** bloku będzie odzwierciedlać hello nowego rekordu.

## <a name="update-a-record"></a>Zaktualizuj rekord

Podczas aktualizacji rekordu w istniejącego zestawu rekordów hello pola, które można zaktualizować są zależne od typu hello rekordu pracujesz.

1. Na powitania **właściwości zestawu rekordów** bloku dla zestawu rekordów, Wyszukaj rekord hello.
2. Zmodyfikuj rekord hello. Po zmodyfikowaniu rekordu, możesz zmienić ustawienia dostępne hello hello rekordu. W hello poniższy przykład, hello **adres IP** pole jest zaznaczone, a adres IP hello jest proces hello jest modyfikowany.

    ![Zmodyfikuj rekord](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. Kliknij przycisk **zapisać** na hello początku hello toosave bloku ustawienia. W górnym prawym rogu hello zostanie wyświetlone powiadomienie hello hello rekord został zapisany.

    ![Zapisano zestaw rekordów](./media/dns-operations-recordsets-portal/saved150.png)

Po zapisaniu rekordu hello hello wartości rekordu hello ustawiony na powitania **strefy DNS** bloku będzie odzwierciedlać hello zaktualizować rekord.

## <a name="remove-a-record-from-a-record-set"></a>Usuwanie rekordu zestawu rekordów

Możesz użyć hello Azure tooremove portalu rekordów z zestawu rekordów. Należy pamiętać, że usunięcie ostatniego rekordu hello z zestawu rekordów nie powoduje usunięcia hello zestawu rekordów.

1. Na powitania **właściwości zestawu rekordów** bloku dla zestawu rekordów, Wyszukaj rekord hello.
2. Kliknij przycisk Zarejestruj hello, które mają tooremove. Następnie wybierz **Usuń**.

    ![Usuwanie rekordu](./media/dns-operations-recordsets-portal/removerecord500.png)

3. Kliknij przycisk **zapisać** na hello początku hello toosave bloku ustawienia.
4. Usunięcie rekordu hello hello wartości rekordu hello na powitania **strefy DNS** bloku będzie odzwierciedlać hello usuwania.

## <a name="delete"></a>Usuń zestaw rekordów

1. Na powitania **właściwości zestawu rekordów** bloku dla zestawu rekordów, kliknij przycisk **usunąć**.

    ![Usuń zestaw rekordów](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. Pojawi się komunikat z pytaniem, czy ma zestaw rekordów hello toodelete.
3. Sprawdź, czy rekord hello dopasowania nazwy hello mają toodelete, a następnie kliknij przycisk **tak**.
4. Na powitania **strefy DNS** bloku, sprawdź, czy zestaw rekordów hello nie jest już widoczna.

## <a name="work-with-ns-and-soa-records"></a>Praca z rekordów NS i SOA

Rekordy NS i SOA, które są automatycznie tworzone są zarządzane zależy od innych typów rekordów.

### <a name="modify-soa-records"></a>Modyfikowania rekordów SOA

Nie można dodać lub usunąć rekordy hello automatycznie utworzony rekord SOA na powitania wierzchołku strefy (nazwa = "@"). Jednak można zmodyfikować jego dowolne parametry hello w hello rekord SOA (z wyjątkiem "Host") i czas wygaśnięcia zestawu rekordów hello.

### <a name="modify-ns-records-at-hello-zone-apex"></a>Modyfikowania rekordów NS w wierzchołku strefy hello

zestaw w wierzchołku strefy hello rekordów NS Hello jest tworzony automatycznie w każdej strefie DNS. Zawiera ona nazwy hello hello Azure DNS nazwy serwerów przypisanej toohello strefy.

Możesz dodać dodatkowe nazwy serwerów toothis NS zestawu rekordów, toosupport wspólnie hosting domeny z więcej niż jednego dostawcy usługi DNS. Można również zmodyfikować hello TTL i metadanych dla tego zestawu rekordów. Jednak nie można usunąć ani zmodyfikować hello wstępnie wypełnione serwerów nazw usługi Azure DNS.

Należy pamiętać, że dotyczy to tylko toohello NS zestawu rekordów w wierzchołku strefy hello. Inne NS zestawów rekordów w strefie (jako stref podrzędnych używane toodelegate) może być modyfikowany bez ograniczeń.

### <a name="delete-soa-or-ns-record-sets"></a>Usuwanie zestawów rekordów SOA lub NS

Nie można usunąć hello SOA i NS zestawów rekordów w wierzchołku strefy hello (nazwa = "@") która są tworzone automatycznie po utworzeniu strefy hello. Są one usuwane automatycznie po usunięciu hello strefy.

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji o usłudze Azure DNS, zobacz hello [Omówienie usługi Azure DNS](dns-overview.md).
* Aby uzyskać więcej informacji na temat automatyzacji DNS, zobacz [stref DNS tworzenia i zestawów rekordów przy użyciu zestawu .NET SDK hello](dns-sdk.md).
* Aby uzyskać więcej informacji na temat odwrotnej rekordy DNS, zobacz [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md).
