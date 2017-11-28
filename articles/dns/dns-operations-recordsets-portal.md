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
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a><span data-ttu-id="cf20a-103">Zarządzanie zestawów rekordów i rekordami DNS za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cf20a-103">Manage DNS records and record sets by using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf20a-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cf20a-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="cf20a-105">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="cf20a-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="cf20a-106">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="cf20a-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="cf20a-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf20a-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="cf20a-108">W tym artykule opisano, jak toomanage zestawów rekordów i rekordów dla strefy DNS przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cf20a-108">This article shows you how toomanage record sets and records for your DNS zone by using hello Azure portal.</span></span>

<span data-ttu-id="cf20a-109">Jest ważne toounderstand hello różnica między zestawów rekordów DNS i poszczególnych rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="cf20a-109">It's important toounderstand hello difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="cf20a-110">Zestaw rekordów jest kolekcją rekordów w strefie, które mają hello takie same nazwy i są hello tego samego typu.</span><span class="sxs-lookup"><span data-stu-id="cf20a-110">A record set is a collection of records in a zone that have hello same name and are hello same type.</span></span> <span data-ttu-id="cf20a-111">Aby uzyskać więcej informacji, zobacz [DNS Utwórz zestawów rekordów i rekordów przy użyciu portalu Azure hello](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cf20a-111">For more information, see [Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="cf20a-112">Tworzenie nowego zestawu rekordów i rekordu</span><span class="sxs-lookup"><span data-stu-id="cf20a-112">Create a new record set and record</span></span>

<span data-ttu-id="cf20a-113">toocreate rekord w hello portalu Azure, zobacz [rekordy DNS utworzyć przy użyciu hello portalu Azure](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cf20a-113">toocreate a record set in hello Azure portal, see [Create DNS records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="cf20a-114">Wyświetl zestaw rekordów</span><span class="sxs-lookup"><span data-stu-id="cf20a-114">View a record set</span></span>

1. <span data-ttu-id="cf20a-115">W hello portalu Azure, przejdź do pozycji toohello **strefy DNS** bloku.</span><span class="sxs-lookup"><span data-stu-id="cf20a-115">In hello Azure portal, go toohello **DNS zone** blade.</span></span>
2. <span data-ttu-id="cf20a-116">Wyszukaj hello zestawu rekordów i zaznacz go.</span><span class="sxs-lookup"><span data-stu-id="cf20a-116">Search for hello record set and select it.</span></span> <span data-ttu-id="cf20a-117">Spowoduje to otwarcie hello właściwości zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="cf20a-117">This opens hello record set properties.</span></span>

    ![Wyszukiwanie zestawu rekordów](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a><span data-ttu-id="cf20a-119">Dodaj nowy zestaw rekordów tooa rekordów</span><span class="sxs-lookup"><span data-stu-id="cf20a-119">Add a new record tooa record set</span></span>

<span data-ttu-id="cf20a-120">Możesz dodać too20 rekordów tooany rekordów zestawu.</span><span class="sxs-lookup"><span data-stu-id="cf20a-120">You can add up too20 records tooany record set.</span></span> <span data-ttu-id="cf20a-121">Zestaw rekordów nie może zawierać dwa identyczne rekordy.</span><span class="sxs-lookup"><span data-stu-id="cf20a-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="cf20a-122">Pusty zestawami rekordów (o zerowej rekordów) mogą być tworzone, ale nie są wyświetlane na serwery hello Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="cf20a-122">Empty record sets (with zero records) can be created, but do not appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="cf20a-123">Zestawy rekordów typu CNAME może zawierać co najwyżej jeden rekord.</span><span class="sxs-lookup"><span data-stu-id="cf20a-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="cf20a-124">Na powitania **właściwości zestawu rekordów** bloku dla swojej strefy DNS, kliknij przycisk Rejestruj hello ustawić mają tooadd rekord.</span><span class="sxs-lookup"><span data-stu-id="cf20a-124">On hello **Record set properties** blade for your DNS zone, click hello record set that you want tooadd a record to.</span></span>

    ![Wybierz zestaw rekordów](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="cf20a-126">Określ zestawu rekordów hello właściwości wypełniając hello pola.</span><span class="sxs-lookup"><span data-stu-id="cf20a-126">Specify hello record set properties by filling in hello fields.</span></span>

    ![Dodaj rekord](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="cf20a-128">Kliknij przycisk **zapisać** na hello początku hello toosave bloku ustawienia.</span><span class="sxs-lookup"><span data-stu-id="cf20a-128">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="cf20a-129">Następnie zamknij hello bloku.</span><span class="sxs-lookup"><span data-stu-id="cf20a-129">Then close hello blade.</span></span>
4. <span data-ttu-id="cf20a-130">Hello ekranu pojawi się zapisuje hello rekordu.</span><span class="sxs-lookup"><span data-stu-id="cf20a-130">In hello corner, you will see that hello record is saving.</span></span>

    ![Zapisywanie zestawu rekordów](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="cf20a-132">Po zapisaniu rekordu hello hello wartości na powitania **strefy DNS** bloku będzie odzwierciedlać hello nowego rekordu.</span><span class="sxs-lookup"><span data-stu-id="cf20a-132">After hello record has been saved, hello values on hello **DNS zone** blade will reflect hello new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="cf20a-133">Zaktualizuj rekord</span><span class="sxs-lookup"><span data-stu-id="cf20a-133">Update a record</span></span>

<span data-ttu-id="cf20a-134">Podczas aktualizacji rekordu w istniejącego zestawu rekordów hello pola, które można zaktualizować są zależne od typu hello rekordu pracujesz.</span><span class="sxs-lookup"><span data-stu-id="cf20a-134">When you update a record in an existing record set, hello fields you can update depend on hello type of record you're working with.</span></span>

1. <span data-ttu-id="cf20a-135">Na powitania **właściwości zestawu rekordów** bloku dla zestawu rekordów, Wyszukaj rekord hello.</span><span class="sxs-lookup"><span data-stu-id="cf20a-135">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="cf20a-136">Zmodyfikuj rekord hello.</span><span class="sxs-lookup"><span data-stu-id="cf20a-136">Modify hello record.</span></span> <span data-ttu-id="cf20a-137">Po zmodyfikowaniu rekordu, możesz zmienić ustawienia dostępne hello hello rekordu.</span><span class="sxs-lookup"><span data-stu-id="cf20a-137">When you modify a record, you can change hello available settings for hello record.</span></span> <span data-ttu-id="cf20a-138">W hello poniższy przykład, hello **adres IP** pole jest zaznaczone, a adres IP hello jest proces hello jest modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="cf20a-138">In hello following example, hello **IP address** field is selected, and hello IP address is in hello process of being modified.</span></span>

    ![Zmodyfikuj rekord](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="cf20a-140">Kliknij przycisk **zapisać** na hello początku hello toosave bloku ustawienia.</span><span class="sxs-lookup"><span data-stu-id="cf20a-140">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="cf20a-141">W górnym prawym rogu hello zostanie wyświetlone powiadomienie hello hello rekord został zapisany.</span><span class="sxs-lookup"><span data-stu-id="cf20a-141">In hello upper right corner, you'll see hello notification that hello record has been saved.</span></span>

    ![Zapisano zestaw rekordów](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="cf20a-143">Po zapisaniu rekordu hello hello wartości rekordu hello ustawiony na powitania **strefy DNS** bloku będzie odzwierciedlać hello zaktualizować rekord.</span><span class="sxs-lookup"><span data-stu-id="cf20a-143">After hello record has been saved, hello values for hello record set on hello **DNS zone** blade will reflect hello updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="cf20a-144">Usuwanie rekordu zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="cf20a-144">Remove a record from a record set</span></span>

<span data-ttu-id="cf20a-145">Możesz użyć hello Azure tooremove portalu rekordów z zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="cf20a-145">You can use hello Azure portal tooremove records from a record set.</span></span> <span data-ttu-id="cf20a-146">Należy pamiętać, że usunięcie ostatniego rekordu hello z zestawu rekordów nie powoduje usunięcia hello zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="cf20a-146">Note that removing hello last record from a record set does not delete hello record set.</span></span>

1. <span data-ttu-id="cf20a-147">Na powitania **właściwości zestawu rekordów** bloku dla zestawu rekordów, Wyszukaj rekord hello.</span><span class="sxs-lookup"><span data-stu-id="cf20a-147">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="cf20a-148">Kliknij przycisk Zarejestruj hello, które mają tooremove.</span><span class="sxs-lookup"><span data-stu-id="cf20a-148">Click hello record that you want tooremove.</span></span> <span data-ttu-id="cf20a-149">Następnie wybierz **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="cf20a-149">Then select **Remove**.</span></span>

    ![Usuwanie rekordu](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="cf20a-151">Kliknij przycisk **zapisać** na hello początku hello toosave bloku ustawienia.</span><span class="sxs-lookup"><span data-stu-id="cf20a-151">Click **Save** at hello top of hello blade toosave your settings.</span></span>
4. <span data-ttu-id="cf20a-152">Usunięcie rekordu hello hello wartości rekordu hello na powitania **strefy DNS** bloku będzie odzwierciedlać hello usuwania.</span><span class="sxs-lookup"><span data-stu-id="cf20a-152">After hello record has been removed, hello values for hello record on hello **DNS zone** blade will reflect hello removal.</span></span>

## <span data-ttu-id="cf20a-153"><a name="delete"></a>Usuń zestaw rekordów</span><span class="sxs-lookup"><span data-stu-id="cf20a-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="cf20a-154">Na powitania **właściwości zestawu rekordów** bloku dla zestawu rekordów, kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="cf20a-154">On hello **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Usuń zestaw rekordów](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="cf20a-156">Pojawi się komunikat z pytaniem, czy ma zestaw rekordów hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="cf20a-156">A message appears asking if you want toodelete hello record set.</span></span>
3. <span data-ttu-id="cf20a-157">Sprawdź, czy rekord hello dopasowania nazwy hello mają toodelete, a następnie kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="cf20a-157">Verify that hello name matches hello record set that you want toodelete, and then click **Yes**.</span></span>
4. <span data-ttu-id="cf20a-158">Na powitania **strefy DNS** bloku, sprawdź, czy zestaw rekordów hello nie jest już widoczna.</span><span class="sxs-lookup"><span data-stu-id="cf20a-158">On hello **DNS zone** blade, verify that hello record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="cf20a-159">Praca z rekordów NS i SOA</span><span class="sxs-lookup"><span data-stu-id="cf20a-159">Work with NS and SOA records</span></span>

<span data-ttu-id="cf20a-160">Rekordy NS i SOA, które są automatycznie tworzone są zarządzane zależy od innych typów rekordów.</span><span class="sxs-lookup"><span data-stu-id="cf20a-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="cf20a-161">Modyfikowania rekordów SOA</span><span class="sxs-lookup"><span data-stu-id="cf20a-161">Modify SOA records</span></span>

<span data-ttu-id="cf20a-162">Nie można dodać lub usunąć rekordy hello automatycznie utworzony rekord SOA na powitania wierzchołku strefy (nazwa = "@").</span><span class="sxs-lookup"><span data-stu-id="cf20a-162">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (name = "@").</span></span> <span data-ttu-id="cf20a-163">Jednak można zmodyfikować jego dowolne parametry hello w hello rekord SOA (z wyjątkiem "Host") i czas wygaśnięcia zestawu rekordów hello.</span><span class="sxs-lookup"><span data-stu-id="cf20a-163">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

### <a name="modify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="cf20a-164">Modyfikowania rekordów NS w wierzchołku strefy hello</span><span class="sxs-lookup"><span data-stu-id="cf20a-164">Modify NS records at hello zone apex</span></span>

<span data-ttu-id="cf20a-165">zestaw w wierzchołku strefy hello rekordów NS Hello jest tworzony automatycznie w każdej strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="cf20a-165">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="cf20a-166">Zawiera ona nazwy hello hello Azure DNS nazwy serwerów przypisanej toohello strefy.</span><span class="sxs-lookup"><span data-stu-id="cf20a-166">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="cf20a-167">Możesz dodać dodatkowe nazwy serwerów toothis NS zestawu rekordów, toosupport wspólnie hosting domeny z więcej niż jednego dostawcy usługi DNS.</span><span class="sxs-lookup"><span data-stu-id="cf20a-167">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="cf20a-168">Można również zmodyfikować hello TTL i metadanych dla tego zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="cf20a-168">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="cf20a-169">Jednak nie można usunąć ani zmodyfikować hello wstępnie wypełnione serwerów nazw usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="cf20a-169">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="cf20a-170">Należy pamiętać, że dotyczy to tylko toohello NS zestawu rekordów w wierzchołku strefy hello.</span><span class="sxs-lookup"><span data-stu-id="cf20a-170">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="cf20a-171">Inne NS zestawów rekordów w strefie (jako stref podrzędnych używane toodelegate) może być modyfikowany bez ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="cf20a-171">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="cf20a-172">Usuwanie zestawów rekordów SOA lub NS</span><span class="sxs-lookup"><span data-stu-id="cf20a-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="cf20a-173">Nie można usunąć hello SOA i NS zestawów rekordów w wierzchołku strefy hello (nazwa = "@") która są tworzone automatycznie po utworzeniu strefy hello.</span><span class="sxs-lookup"><span data-stu-id="cf20a-173">You cannot delete hello SOA and NS record sets at hello zone apex (name = "@") that are created automatically when hello zone is created.</span></span> <span data-ttu-id="cf20a-174">Są one usuwane automatycznie po usunięciu hello strefy.</span><span class="sxs-lookup"><span data-stu-id="cf20a-174">They are deleted automatically when you delete hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf20a-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cf20a-175">Next steps</span></span>

* <span data-ttu-id="cf20a-176">Aby uzyskać więcej informacji o usłudze Azure DNS, zobacz hello [Omówienie usługi Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cf20a-176">For more information about Azure DNS, see hello [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="cf20a-177">Aby uzyskać więcej informacji na temat automatyzacji DNS, zobacz [stref DNS tworzenia i zestawów rekordów przy użyciu zestawu .NET SDK hello](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="cf20a-177">For more information about automating DNS, see [Creating DNS zones and record sets using hello .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="cf20a-178">Aby uzyskać więcej informacji na temat odwrotnej rekordy DNS, zobacz [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cf20a-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
