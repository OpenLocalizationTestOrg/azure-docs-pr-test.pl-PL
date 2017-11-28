---
title: "aaaRestrict dostępu przy użyciu sygnatury dostępu współdzielonego - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse sygnatury dostępu współdzielonego toorestrict HDInsight dostępu toodata przechowywane w obiektach blob magazynu Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a><span data-ttu-id="ff68e-103">Użyj toodata dostępu toorestrict sygnatury dostępu współdzielonego magazynu Azure w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff68e-103">Use Azure Storage Shared Access Signatures toorestrict access toodata in HDInsight</span></span>

<span data-ttu-id="ff68e-104">HDInsight ma pełny dostęp toodata na kontach magazynu Azure hello skojarzony z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-104">HDInsight has full access toodata in hello Azure Storage accounts associated with hello cluster.</span></span> <span data-ttu-id="ff68e-105">Możesz użyć sygnatury dostępu współdzielonego w hello obiektów blob kontenera toorestrict dostępu toohello danych.</span><span class="sxs-lookup"><span data-stu-id="ff68e-105">You can use Shared Access Signatures on hello blob container toorestrict access toohello data.</span></span> <span data-ttu-id="ff68e-106">Na przykład tooprovide dostęp tylko do odczytu toohello danych.</span><span class="sxs-lookup"><span data-stu-id="ff68e-106">For example, tooprovide read-only access toohello data.</span></span> <span data-ttu-id="ff68e-107">Udostępniony sygnatur dostępu (SAS) są funkcją kontami magazynu Azure, umożliwiający toolimit toodata dostępu.</span><span class="sxs-lookup"><span data-stu-id="ff68e-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you toolimit access toodata.</span></span> <span data-ttu-id="ff68e-108">Na przykład dostarczanie toodata dostęp tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="ff68e-108">For example, providing read-only access toodata.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff68e-109">Jako rozwiązanie przy użyciu Apache zakres należy rozważyć użycie HDInsight przyłączonych do domeny.</span><span class="sxs-lookup"><span data-stu-id="ff68e-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="ff68e-110">Aby uzyskać więcej informacji, zobacz hello [HDInsight przyłączonych do domeny skonfiguruj](hdinsight-domain-joined-configure.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="ff68e-110">For more information, see hello [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="ff68e-111">HDInsight musi mieć pełny dostęp toohello domyślny magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-111">HDInsight must have full access toohello default storage for hello cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="ff68e-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="ff68e-112">Requirements</span></span>

* <span data-ttu-id="ff68e-113">Subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ff68e-113">An Azure subscription</span></span>
* <span data-ttu-id="ff68e-114">C# lub języka Python.</span><span class="sxs-lookup"><span data-stu-id="ff68e-114">C# or Python.</span></span> <span data-ttu-id="ff68e-115">Przykład kodu C# stanowi rozwiązanie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ff68e-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="ff68e-116">Visual Studio musi być w wersji 2013, 2015 lub 2017</span><span class="sxs-lookup"><span data-stu-id="ff68e-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="ff68e-117">Python musi być w wersji 2.7 lub wyższej</span><span class="sxs-lookup"><span data-stu-id="ff68e-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="ff68e-118">Klaster usługi HDInsight opartej na systemie Linux lub [programu Azure PowerShell] [ powershell] — Jeśli masz istniejący klaster opartych na systemie Linux, można użyć narzędzia Ambari tooadd klastra toohello sygnatura dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="ff68e-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari tooadd a Shared Access Signature toohello cluster.</span></span> <span data-ttu-id="ff68e-119">Jeśli nie, można użyć programu Azure PowerShell toocreate klastra i dodać sygnaturę dostępu współdzielonego podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="ff68e-119">If not, you can use Azure PowerShell toocreate a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ff68e-120">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ff68e-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ff68e-121">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="ff68e-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="ff68e-122">Witaj przykładowe pliki z [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="ff68e-122">hello example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="ff68e-123">To repozytorium zawiera hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ff68e-123">This repository contains hello following items:</span></span>

  * <span data-ttu-id="ff68e-124">Projektu programu Visual Studio, który można utworzyć kontenera magazynu, zapisane zasady i skojarzenia zabezpieczeń do użycia z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff68e-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="ff68e-125">Skrypt w języku Python, który można utworzyć kontenera magazynu, zapisane zasady i skojarzenia zabezpieczeń do użycia z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff68e-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="ff68e-126">Skrypt programu PowerShell, który może tworzyć HDInsight klastra i skonfigurować go toouse hello SAS.</span><span class="sxs-lookup"><span data-stu-id="ff68e-126">A PowerShell script that can create a HDInsight cluster and configure it toouse hello SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="ff68e-127">Sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="ff68e-127">Shared Access Signatures</span></span>

<span data-ttu-id="ff68e-128">Istnieją dwa rodzaje sygnatur dostępu współdzielonego:</span><span class="sxs-lookup"><span data-stu-id="ff68e-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="ff68e-129">Ad hoc: uprawnienia dla hello SAS są określone na powitania identyfikatora URI połączenia SAS, czas wygaśnięcia i godzina rozpoczęcia hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-129">Ad hoc: hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span>

* <span data-ttu-id="ff68e-130">Przechowywane zasad dostępu: zasady dostępu do przechowywanych jest zdefiniowany w kontenerze zasobów, takich jak kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="ff68e-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="ff68e-131">Zasady mogą być używane toomanage ograniczenia dla co najmniej jeden sygnatur dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="ff68e-131">A policy can be used toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="ff68e-132">Po skojarzeniu sygnatury dostępu Współdzielonego za pomocą zasad dostępu przechowywane, hello SAS dziedziczy ograniczenia hello — uprawnienia - zdefiniowane zasady dostępu hello przechowywane, czas wygaśnięcia i godzina rozpoczęcia hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-132">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span>

<span data-ttu-id="ff68e-133">Witaj różnica pomiędzy formularzami Witaj dwie ważne jest jeden scenariusz klucza: odwołania.</span><span class="sxs-lookup"><span data-stu-id="ff68e-133">hello difference between hello two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="ff68e-134">Sygnatury dostępu Współdzielonego jest adres URL, więc każdy, kto uzyskuje hello SAS może być używany, niezależnie od tego, kto go zażądało toobegin z.</span><span class="sxs-lookup"><span data-stu-id="ff68e-134">A SAS is a URL, so anyone who obtains hello SAS can use it, regardless of who requested it toobegin with.</span></span> <span data-ttu-id="ff68e-135">Sygnatury dostępu Współdzielonego zostanie opublikowana publicznie, może służyć każdy hello world.</span><span class="sxs-lookup"><span data-stu-id="ff68e-135">If a SAS is published publicly, it can be used by anyone in hello world.</span></span> <span data-ttu-id="ff68e-136">Sygnatury dostępu Współdzielonego, który jest rozpowszechniany jest prawidłowy, dopóki jedna z następujących czterech zdarzeń sytuacji:</span><span class="sxs-lookup"><span data-stu-id="ff68e-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="ff68e-137">czas wygaśnięcia Hello określony na powitania osiągnięty sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="ff68e-137">hello expiry time specified on hello SAS is reached.</span></span>

2. <span data-ttu-id="ff68e-138">czas wygaśnięcia Hello określone zasady dostępu hello przechowywane odwołuje się hello osiągnięty sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="ff68e-138">hello expiry time specified on hello stored access policy referenced by hello SAS is reached.</span></span> <span data-ttu-id="ff68e-139">Witaj następujące scenariusze spowodować czas wygaśnięcia hello toobe osiągnięto:</span><span class="sxs-lookup"><span data-stu-id="ff68e-139">hello following scenarios cause hello expiry time toobe reached:</span></span>

    * <span data-ttu-id="ff68e-140">Upłynął czas Hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-140">hello time interval has elapsed.</span></span>
    * <span data-ttu-id="ff68e-141">zasady dostępu Hello przechowywane jest zmodyfikowany toohave czas wygaśnięcia w przeszłości hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-141">hello stored access policy is modified toohave an expiry time in hello past.</span></span> <span data-ttu-id="ff68e-142">Zmiana czasu wygaśnięcia hello jest hello toorevoke jednokierunkowych SAS.</span><span class="sxs-lookup"><span data-stu-id="ff68e-142">Changing hello expiry time is one way toorevoke hello SAS.</span></span>

3. <span data-ttu-id="ff68e-143">Witaj przechowywane odwołuje hello SAS jest usuwane, który jest inny sposób hello toorevoke SAS zasad dostępu.</span><span class="sxs-lookup"><span data-stu-id="ff68e-143">hello stored access policy referenced by hello SAS is deleted, which is another way toorevoke hello SAS.</span></span> <span data-ttu-id="ff68e-144">Jeśli ponownego tworzenia zasad dostępu hello przechowywane z hello takie same nazwy, wszystkie tokeny sygnatury dostępu Współdzielonego dla poprzednich zasad hello są prawidłowe, (Jeśli czas wygaśnięcia hello na powitania nie przeszło SAS).</span><span class="sxs-lookup"><span data-stu-id="ff68e-144">If you recreate hello stored access policy with hello same name, all  SAS tokens for hello previous policy are valid (if hello expiry time on hello SAS has not passed).</span></span> <span data-ttu-id="ff68e-145">Jeśli planujesz hello toorevoke sygnatury dostępu Współdzielonego, można toouse się, że inną nazwę Jeśli ponownego tworzenia zasad dostępu hello z upływem czasu w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-145">If you intend toorevoke hello SAS, be sure toouse a different name if you recreate hello access policy with an expiry time in hello future.</span></span>

4. <span data-ttu-id="ff68e-146">ponownego wygenerowania klucza konta Hello, który był używany toocreate hello SAS.</span><span class="sxs-lookup"><span data-stu-id="ff68e-146">hello account key that was used toocreate hello SAS is regenerated.</span></span> <span data-ttu-id="ff68e-147">Trwa ponowne generowanie klucza hello powoduje, że wszystkie aplikacje używające hello poprzedniego klucza toofail uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="ff68e-147">Regenerating hello key causes all applications that use hello previous key toofail authentication.</span></span> <span data-ttu-id="ff68e-148">Zaktualizuj wszystkie składniki toohello nowego klucza.</span><span class="sxs-lookup"><span data-stu-id="ff68e-148">Update all components toohello new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff68e-149">Identyfikator URI sygnatury dostępu współdzielonego jest skojarzony z sygnaturą hello klucza toocreate używane konto hello i hello skojarzonych zasad dostępu przechowywanych (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="ff68e-149">A shared access signature URI is associated with hello account key used toocreate hello signature, and hello associated stored access policy (if any).</span></span> <span data-ttu-id="ff68e-150">Jeśli określono żadnych zasad dostępu przechowywane, hello tylko sposób toorevoke sygnatury dostępu współdzielonego jest klucz konta hello toochange.</span><span class="sxs-lookup"><span data-stu-id="ff68e-150">If no stored access policy is specified, hello only way toorevoke a shared access signature is toochange hello account key.</span></span>

<span data-ttu-id="ff68e-151">Firma Microsoft zaleca zawsze używać zasad dostępu przechowywane.</span><span class="sxs-lookup"><span data-stu-id="ff68e-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="ff68e-152">Podczas korzystania z zasady przechowywane, możesz odwołać podpisów lub przedłużyć datę wygaśnięcia hello, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="ff68e-152">When using stored policies, you can either revoke signatures or extend hello expiry date as needed.</span></span> <span data-ttu-id="ff68e-153">kroki Hello w tym dokumencie Użyj toogenerate zasady dostępu do przechowywanych sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="ff68e-153">hello steps in this document use stored access policies toogenerate SAS.</span></span>

<span data-ttu-id="ff68e-154">Aby uzyskać więcej informacji dotyczących sygnatur dostępu współdzielonego, zobacz [modelu sygnatur dostępu Współdzielonego hello opis](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="ff68e-154">For more information on Shared Access Signatures, see [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="ff68e-155">Tworzenie zasad przechowywane i sygnatury dostępu Współdzielonego, za pomocą C\#</span><span class="sxs-lookup"><span data-stu-id="ff68e-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="ff68e-156">Otwórz rozwiązanie hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ff68e-156">Open hello solution in Visual Studio.</span></span>

2. <span data-ttu-id="ff68e-157">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **SASToken** projekt i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="ff68e-157">In Solution Explorer, right-click on hello **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="ff68e-158">Wybierz **ustawienia** i Dodaj wartości hello następujące wpisy:</span><span class="sxs-lookup"><span data-stu-id="ff68e-158">Select **Settings** and add values for hello following entries:</span></span>

   * <span data-ttu-id="ff68e-159">StorageConnectionString: hello parametrów połączenia dla konta magazynu hello, które mają toocreate zapisane zasady i sygnatury dostępu Współdzielonego dla.</span><span class="sxs-lookup"><span data-stu-id="ff68e-159">StorageConnectionString: hello connection string for hello storage account that you want toocreate a stored policy and SAS for.</span></span> <span data-ttu-id="ff68e-160">powinna mieć ona Hello format `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` gdzie `myaccount` hello nazwa konta magazynu i `mykey` jest hello klucza dla konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-160">hello format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is hello name of your storage account and `mykey` is hello key for hello storage account.</span></span>

   * <span data-ttu-id="ff68e-161">ContainerName: hello kontenera na koncie magazynu hello, który ma dostęp toorestrict do.</span><span class="sxs-lookup"><span data-stu-id="ff68e-161">ContainerName: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="ff68e-162">SASPolicyName: hello toouse nazwy dla hello przechowywane toocreate zasad.</span><span class="sxs-lookup"><span data-stu-id="ff68e-162">SASPolicyName: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="ff68e-163">FileToUpload: hello ścieżka tooa pliku, który jest kontenerem toohello przekazane.</span><span class="sxs-lookup"><span data-stu-id="ff68e-163">FileToUpload: hello path tooa file that is uploaded toohello container.</span></span>

4. <span data-ttu-id="ff68e-164">Uruchom projekt hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-164">Run hello project.</span></span> <span data-ttu-id="ff68e-165">Po wygenerowaniu hello SAS, wyświetlane są toohello podobne informacje następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="ff68e-165">Information similar toohello following text is displayed once hello SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="ff68e-166">Zapisz token zasady sygnatury dostępu Współdzielonego hello, nazwa konta magazynu i nazwy kontenera.</span><span class="sxs-lookup"><span data-stu-id="ff68e-166">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="ff68e-167">Te wartości są używane podczas kojarzenia hello konta magazynu z klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff68e-167">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="ff68e-168">Tworzenie zasad przechowywane i SAS używany język Python</span><span class="sxs-lookup"><span data-stu-id="ff68e-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="ff68e-169">Otwórz plik SASToken.py hello i zmienić hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="ff68e-169">Open hello SASToken.py file and change hello following values:</span></span>

   * <span data-ttu-id="ff68e-170">zasady\_name: hello toouse nazwy dla hello przechowywane toocreate zasad.</span><span class="sxs-lookup"><span data-stu-id="ff68e-170">policy\_name: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="ff68e-171">Magazyn\_konta\_name: hello nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ff68e-171">storage\_account\_name: hello name of your storage account.</span></span>

   * <span data-ttu-id="ff68e-172">Magazyn\_konta\_klucz: hello klucza dla konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-172">storage\_account\_key: hello key for hello storage account.</span></span>

   * <span data-ttu-id="ff68e-173">Magazyn\_kontenera\_name: hello kontenera na koncie magazynu hello, który ma dostęp toorestrict do.</span><span class="sxs-lookup"><span data-stu-id="ff68e-173">storage\_container\_name: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="ff68e-174">przykład\_pliku\_ścieżki: hello ścieżka tooa pliku, który jest kontenerem toohello przekazane.</span><span class="sxs-lookup"><span data-stu-id="ff68e-174">example\_file\_path: hello path tooa file that is uploaded toohello container.</span></span>

2. <span data-ttu-id="ff68e-175">Uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-175">Run hello script.</span></span> <span data-ttu-id="ff68e-176">Wyświetla hello SAS tokenu podobne toohello następującego tekstu po ukończeniu działania skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="ff68e-176">It displays hello SAS token similar toohello following text when hello script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="ff68e-177">Zapisz token zasady sygnatury dostępu Współdzielonego hello, nazwa konta magazynu i nazwy kontenera.</span><span class="sxs-lookup"><span data-stu-id="ff68e-177">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="ff68e-178">Te wartości są używane podczas kojarzenia hello konta magazynu z klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff68e-178">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

## <a name="use-hello-sas-with-hdinsight"></a><span data-ttu-id="ff68e-179">Użyj hello SAS z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff68e-179">Use hello SAS with HDInsight</span></span>

<span data-ttu-id="ff68e-180">Podczas tworzenia klastra usługi HDInsight, należy określić konto magazynu głównego i opcjonalnie możesz określić dodatkowe konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ff68e-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="ff68e-181">Obie te metody dodawania magazynu wymagają konta magazynu toohello pełny dostęp i kontenerów, które są używane.</span><span class="sxs-lookup"><span data-stu-id="ff68e-181">Both of these methods of adding storage require full access toohello storage accounts and containers that are used.</span></span>

<span data-ttu-id="ff68e-182">toouse kontener tooa dostępu toolimit sygnatura dostępu współdzielonego, Dodaj toohello wpisu niestandardowego **lokacji podstawowej** konfiguracji hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ff68e-182">toouse a Shared Access Signature toolimit access tooa container, add a custom entry toohello **core-site** configuration for hello cluster.</span></span>

* <span data-ttu-id="ff68e-183">Aby uzyskać **opartych na systemie Windows** lub **opartych na systemie Linux** klastrów usługi HDInsight, można dodać wpisu hello podczas tworzenia klastra przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff68e-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add hello entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="ff68e-184">Aby uzyskać **opartych na systemie Linux** klastrów usługi HDInsight, zmień konfigurację powitania po utworzeniu klastra przy użyciu narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="ff68e-184">For **Linux-based** HDInsight clusters, change hello configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-hello-sas"></a><span data-ttu-id="ff68e-185">Tworzenie klastra, który wykorzystuje hello SAS</span><span class="sxs-lookup"><span data-stu-id="ff68e-185">Create a cluster that uses hello SAS</span></span>

<span data-ttu-id="ff68e-186">Przykład tworzenia klastra usługi HDInsight tego hello używa SAS jest uwzględniona w hello `CreateCluster` katalogu hello repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ff68e-186">An example of creating an HDInsight cluster that uses hello SAS is included in hello `CreateCluster` directory of hello repository.</span></span> <span data-ttu-id="ff68e-187">toouse, który go hello Użyj następujących kroków:</span><span class="sxs-lookup"><span data-stu-id="ff68e-187">toouse it, use hello following steps:</span></span>

1. <span data-ttu-id="ff68e-188">Otwórz hello `CreateCluster\HDInsightSAS.ps1` plik w edytorze tekstu i zmodyfikuj hello następujące wartości na początku hello hello dokumentu.</span><span class="sxs-lookup"><span data-stu-id="ff68e-188">Open hello `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify hello following values at hello beginning of hello document.</span></span>

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="ff68e-189">Na przykład zmienić `'mycluster'` toohello nazwy klastra hello ma toocreate.</span><span class="sxs-lookup"><span data-stu-id="ff68e-189">For example, change `'mycluster'` toohello name of hello cluster you want toocreate.</span></span> <span data-ttu-id="ff68e-190">wartości SAS Hello powinna odpowiadać wartości hello z poprzednich kroków hello podczas tworzenia konta magazynu i tokenu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="ff68e-190">hello SAS values should match hello values from hello previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="ff68e-191">Po zmianie wartości hello, Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-191">Once you have changed hello values, save hello file.</span></span>

2. <span data-ttu-id="ff68e-192">Otwórz nowy wiersz programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff68e-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="ff68e-193">Jeśli masz doświadczenia w pracy z programem Azure PowerShell lub nie został zainstalowany, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell][powershell].</span><span class="sxs-lookup"><span data-stu-id="ff68e-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="ff68e-194">W wierszu hello Użyj hello następujące polecenie tooyour tooauthenticate subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="ff68e-194">From hello prompt, use hello following command tooauthenticate tooyour Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="ff68e-195">Po wyświetleniu monitu zaloguj się za pomocą hello konta dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ff68e-195">When prompted, log in with hello account for your Azure subscription.</span></span>

    <span data-ttu-id="ff68e-196">Jeśli konto jest skojarzone z wieloma subskrypcjami platformy Azure, może być konieczne toouse `Select-AzureRmSubscription` tooselect hello subskrypcji chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="ff68e-196">If your account is associated with multiple Azure subscriptions, you may need toouse `Select-AzureRmSubscription` tooselect hello subscription you wish toouse.</span></span>

4. <span data-ttu-id="ff68e-197">W wierszu hello Zmień katalogi toohello `CreateCluster` katalog zawierający plik HDInsightSAS.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-197">From hello prompt, change directories toohello `CreateCluster` directory that contains hello HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="ff68e-198">Następnie użyj następującego skryptu hello toorun polecenia hello</span><span class="sxs-lookup"><span data-stu-id="ff68e-198">Then use hello following command toorun hello script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="ff68e-199">Jako hello skrypt będzie uruchamiany rejestruje wierszu polecenia programu PowerShell toohello danych wyjściowych podczas tworzenia zasobu hello konta grupy i magazynu.</span><span class="sxs-lookup"><span data-stu-id="ff68e-199">As hello script runs, it logs output toohello PowerShell prompt as it creates hello resource group and storage accounts.</span></span> <span data-ttu-id="ff68e-200">Jesteś użytkownikiem hello HTTP zostanie wyświetlony monit o tooenter hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff68e-200">You are prompted tooenter hello HTTP user for hello HDInsight cluster.</span></span> <span data-ttu-id="ff68e-201">To konto jest używane toosecure protokołu HTTP/s dostępu toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="ff68e-201">This account is used toosecure HTTP/s access toohello cluster.</span></span>

    <span data-ttu-id="ff68e-202">W przypadku tworzenia opartych na systemie Linux klaster, zostanie wyświetlony monit o nazwę konta użytkownika SSH i hasło.</span><span class="sxs-lookup"><span data-stu-id="ff68e-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="ff68e-203">To konto jest używane tooremotely dziennika w klastrze toohello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-203">This account is used tooremotely log in toohello cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ff68e-204">Po wyświetleniu monitu o hello protokołu HTTP/s lub SSH nazwy użytkownika i hasła, należy podać hasło, które spełnia następujące kryteria hello:</span><span class="sxs-lookup"><span data-stu-id="ff68e-204">When prompted for hello HTTP/s or SSH user name and password, you must provide a password that meets hello following criteria:</span></span>
   >
   > * <span data-ttu-id="ff68e-205">Musi być co najmniej 10 znaków</span><span class="sxs-lookup"><span data-stu-id="ff68e-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="ff68e-206">Musi zawierać co najmniej jedną cyfrę</span><span class="sxs-lookup"><span data-stu-id="ff68e-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="ff68e-207">Musi zawierać co najmniej jeden znak inny niż alfanumeryczny</span><span class="sxs-lookup"><span data-stu-id="ff68e-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="ff68e-208">Musi zawierać co najmniej jedną wielką lub małą literę</span><span class="sxs-lookup"><span data-stu-id="ff68e-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="ff68e-209">Trwa trochę czasu toocomplete tego skryptu, zazwyczaj około 15 minut.</span><span class="sxs-lookup"><span data-stu-id="ff68e-209">It takes a while for this script toocomplete, usually around 15 minutes.</span></span> <span data-ttu-id="ff68e-210">Po zakończeniu hello skryptu bez żadnych błędów, hello klaster został utworzony.</span><span class="sxs-lookup"><span data-stu-id="ff68e-210">When hello script completes without any errors, hello cluster has been created.</span></span>

### <a name="use-hello-sas-with-an-existing-cluster"></a><span data-ttu-id="ff68e-211">Użyj hello SAS z istniejącego klastra</span><span class="sxs-lookup"><span data-stu-id="ff68e-211">Use hello SAS with an existing cluster</span></span>

<span data-ttu-id="ff68e-212">Jeśli masz istniejący klaster opartych na systemie Linux, można dodać hello SAS toohello **lokacji podstawowej** konfiguracji przy użyciu hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ff68e-212">If you have an existing Linux-based cluster, you can add hello SAS toohello **core-site** configuration by using hello following steps:</span></span>

1. <span data-ttu-id="ff68e-213">Otwórz hello Ambari web UI dla klastra.</span><span class="sxs-lookup"><span data-stu-id="ff68e-213">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="ff68e-214">adres Hello na tej stronie jest https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="ff68e-214">hello address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="ff68e-215">Po wyświetleniu monitu uwierzytelniania toohello klastra przy użyciu nazwy administratora hello (Administrator) i hasło użyte podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-215">When prompted, authenticate toohello cluster using hello admin name (admin) and password you used when creating hello cluster.</span></span>

2. <span data-ttu-id="ff68e-216">Hello po lewej stronie powitania interfejsu użytkownika sieci web Ambari, zaznacz **HDFS** , a następnie wybierz hello **Configs** kartę w środku hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="ff68e-216">From hello left side of hello Ambari web UI, select **HDFS** and then select hello **Configs** tab in hello middle of hello page.</span></span>

3. <span data-ttu-id="ff68e-217">Wybierz hello **zaawansowane** , a następnie przewiń do momentu znalezienia hello **niestandardowe core-site** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ff68e-217">Select hello **Advanced** tab, and then scroll until you find hello **Custom core-site** section.</span></span>

4. <span data-ttu-id="ff68e-218">Rozwiń węzeł hello **niestandardowe core-site** sekcji, a następnie przewijania zakończenia toohello i wybierz hello **Dodaj właściwość... ** łącza.</span><span class="sxs-lookup"><span data-stu-id="ff68e-218">Expand hello **Custom core-site** section, then scroll toohello end and select hello **Add property...** link.</span></span> <span data-ttu-id="ff68e-219">Użyj następujących hello wartości hello **klucza** i **wartość** pola:</span><span class="sxs-lookup"><span data-stu-id="ff68e-219">Use hello following values for hello **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="ff68e-220">**Klucz**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ff68e-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="ff68e-221">**Wartość**: hello SAS zwrócony przez hello aplikacji C# lub Python został przeprowadzony wcześniej</span><span class="sxs-lookup"><span data-stu-id="ff68e-221">**Value**: hello SAS returned by hello C# or Python application you ran previously</span></span>

     <span data-ttu-id="ff68e-222">Zastąp **CONTAINERNAME** o nazwie kontenera hello używane z aplikacji hello C# lub SAS.</span><span class="sxs-lookup"><span data-stu-id="ff68e-222">Replace **CONTAINERNAME** with hello container name you used with hello C# or SAS application.</span></span> <span data-ttu-id="ff68e-223">Zastąp **STORAGEACCOUNTNAME** nazwy konta magazynu hello używane.</span><span class="sxs-lookup"><span data-stu-id="ff68e-223">Replace **STORAGEACCOUNTNAME** with hello storage account name you used.</span></span>

5. <span data-ttu-id="ff68e-224">Kliknij przycisk hello **Dodaj** przycisk toosave tego klucza i wartości, a następnie kliknij przycisk hello **zapisać** przycisk zmiany konfiguracji hello toosave.</span><span class="sxs-lookup"><span data-stu-id="ff68e-224">Click hello **Add** button toosave this key and value, then click hello **Save** button toosave hello configuration changes.</span></span> <span data-ttu-id="ff68e-225">Po wyświetleniu monitu, Dodaj opis zmian hello ("Dodawanie dostępu do pamięci masowej SAS" na przykład), a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="ff68e-225">When prompted, add a description of hello change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="ff68e-226">Kliknij przycisk **OK** kiedy hello zmiany zostały ukończone.</span><span class="sxs-lookup"><span data-stu-id="ff68e-226">Click **OK** when hello changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ff68e-227">Przed hello zmiany zostały uwzględnione, należy ponownie uruchomić kilka usług.</span><span class="sxs-lookup"><span data-stu-id="ff68e-227">You must restart several services before hello change takes effect.</span></span>

6. <span data-ttu-id="ff68e-228">W sieci web Ambari hello interfejsu użytkownika, wybierz **HDFS** liście hello na powitania po lewej, a następnie wybierz **Uruchom ponownie wszystkie** z hello **akcji usługi** listy rozwijanej listy na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="ff68e-228">In hello Ambari web UI, select **HDFS** from hello list on hello left, and then select **Restart All** from hello **Service Actions** drop down list on hello right.</span></span> <span data-ttu-id="ff68e-229">Po wyświetleniu monitu wybierz **Włącz tryb konserwacji** , a następnie uruchom ponownie wszystkie __Conform select ".</span><span class="sxs-lookup"><span data-stu-id="ff68e-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="ff68e-230">Powtórz ten proces dla MapReduce2 i YARN.</span><span class="sxs-lookup"><span data-stu-id="ff68e-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="ff68e-231">Po ponownym uruchomieniu usługi hello, wybierz każdego z nich i Wyłącz tryb konserwacji z hello **akcji usługi** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="ff68e-231">Once hello services have restarted, select each one and disable maintenance mode from hello **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="ff68e-232">Testowanie dostęp ograniczony</span><span class="sxs-lookup"><span data-stu-id="ff68e-232">Test restricted access</span></span>

<span data-ttu-id="ff68e-233">tooverify ograniczono dostępu, użyj hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="ff68e-233">tooverify that you have restricted access, use hello following methods:</span></span>

* <span data-ttu-id="ff68e-234">Aby uzyskać **opartych na systemie Windows** klastrów usługi HDInsight, użyj klastra toohello tooconnect pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="ff68e-234">For **Windows-based** HDInsight clusters, use Remote Desktop tooconnect toohello cluster.</span></span> <span data-ttu-id="ff68e-235">Aby uzyskać więcej informacji, zobacz [połączyć za pomocą protokołu RDP tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="ff68e-235">For more information, see [Connect tooHDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="ff68e-236">Po nawiązaniu połączenia użyj hello **Hadoop wiersza polecenia** ikonę na powitania pulpitu tooopen wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="ff68e-236">Once connected, use hello **Hadoop Command-Line** icon on hello desktop tooopen a command prompt.</span></span>

* <span data-ttu-id="ff68e-237">Aby uzyskać **opartych na systemie Linux** klastrów usługi HDInsight, użyj klastra toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="ff68e-237">For **Linux-based** HDInsight clusters, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="ff68e-238">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ff68e-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="ff68e-239">Po nawiązaniu połączenia toohello klastra, użyj hello następujące możliwe tylko odczyt i listy elementów na koncie magazynu SAS hello tooverify kroki:</span><span class="sxs-lookup"><span data-stu-id="ff68e-239">Once connected toohello cluster, use hello following steps tooverify that you can only read and list items on hello SAS storage account:</span></span>

1. <span data-ttu-id="ff68e-240">zawartość hello toolist hello kontenera, hello Użyj następującego polecenia w wierszu hello:</span><span class="sxs-lookup"><span data-stu-id="ff68e-240">toolist hello contents of hello container, use hello following command from hello prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="ff68e-241">Zastąp **SASCONTAINER** o nazwie hello kontenera hello utworzone dla hello sygnatury dostępu Współdzielonego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ff68e-241">Replace **SASCONTAINER** with hello name of hello container created for hello SAS storage account.</span></span> <span data-ttu-id="ff68e-242">Zastąp **SASACCOUNTNAME** o nazwie hello hello konto magazynu dla hello sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="ff68e-242">Replace **SASACCOUNTNAME** with hello name of hello storage account used for hello SAS.</span></span>

    <span data-ttu-id="ff68e-243">Lista Hello zawiera plik hello przekazane po utworzenia kontenera hello i skojarzenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ff68e-243">hello list includes hello file uploaded when hello container and SAS were created.</span></span>

2. <span data-ttu-id="ff68e-244">Użyj hello następujące polecenie tooverify przeczytanie hello zawartość pliku hello.</span><span class="sxs-lookup"><span data-stu-id="ff68e-244">Use hello following command tooverify that you can read hello contents of hello file.</span></span> <span data-ttu-id="ff68e-245">Zastąp hello **SASCONTAINER** i **SASACCOUNTNAME** jak hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="ff68e-245">Replace hello **SASCONTAINER** and **SASACCOUNTNAME** as in hello previous step.</span></span> <span data-ttu-id="ff68e-246">Zastąp **FILENAME** hello nazwą pliku hello wyświetlane w hello poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="ff68e-246">Replace **FILENAME** with hello name of hello file displayed in hello previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="ff68e-247">To polecenie wyświetla zawartość hello hello pliku.</span><span class="sxs-lookup"><span data-stu-id="ff68e-247">This command lists hello contents of hello file.</span></span>

3. <span data-ttu-id="ff68e-248">Witaj Użyj następującego polecenia toodownload hello pliku toohello lokalnego systemu plików:</span><span class="sxs-lookup"><span data-stu-id="ff68e-248">Use hello following command toodownload hello file toohello local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="ff68e-249">To polecenie pliki do pobrania hello tooa lokalnego pliku o nazwie **plik_testowy.txt**.</span><span class="sxs-lookup"><span data-stu-id="ff68e-249">This command downloads hello file tooa local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="ff68e-250">Użyj hello następujące polecenie tooupload hello pliku lokalnego tooa nowy plik o nazwie **testupload.txt** na powitania pamięci masowej SAS:</span><span class="sxs-lookup"><span data-stu-id="ff68e-250">Use hello following command tooupload hello local file tooa new file named **testupload.txt** on hello SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="ff68e-251">Pojawi się komunikat toohello podobne, następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="ff68e-251">You receive a message similar toohello following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="ff68e-252">Ten błąd występuje, ponieważ lokalizacja przechowywania hello jest odczytu + tylko z listy.</span><span class="sxs-lookup"><span data-stu-id="ff68e-252">This error occurs because hello storage location is read+list only.</span></span> <span data-ttu-id="ff68e-253">Witaj Użyj następującego polecenia tooput hello danych na hello domyślny magazyn dla klastra hello, który jest dostępny do zapisu:</span><span class="sxs-lookup"><span data-stu-id="ff68e-253">Use hello following command tooput hello data on hello default storage for hello cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="ff68e-254">Ten czas operacji hello powinno zakończyć się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="ff68e-254">This time, hello operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ff68e-255">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="ff68e-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="ff68e-256">Zadanie zostało anulowane</span><span class="sxs-lookup"><span data-stu-id="ff68e-256">A task was canceled</span></span>

<span data-ttu-id="ff68e-257">**Objawy**: podczas tworzenia klastra za pomocą skryptu PowerShell hello, może zostać wyświetlony następujący komunikat o błędzie hello:</span><span class="sxs-lookup"><span data-stu-id="ff68e-257">**Symptoms**: When creating a cluster using hello PowerShell script, you may receive hello following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="ff68e-258">**Przyczyna**: ten błąd może wystąpić, jeśli używasz hasła dla użytkownika administracyjnego/HTTP hello hello klastra lub (w przypadku klastrów z systemem Linux) hello użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="ff68e-258">**Cause**: This error can occur if you use a password for hello admin/HTTP user for hello cluster, or (for Linux-based clusters) hello SSH user.</span></span>

<span data-ttu-id="ff68e-259">**Rozdzielczość**: Użyj hasła spełniającego hello następujące kryteria:</span><span class="sxs-lookup"><span data-stu-id="ff68e-259">**Resolution**: Use a password that meets hello following criteria:</span></span>

* <span data-ttu-id="ff68e-260">Musi być co najmniej 10 znaków</span><span class="sxs-lookup"><span data-stu-id="ff68e-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="ff68e-261">Musi zawierać co najmniej jedną cyfrę</span><span class="sxs-lookup"><span data-stu-id="ff68e-261">Must contain at least one digit</span></span>
* <span data-ttu-id="ff68e-262">Musi zawierać co najmniej jeden znak inny niż alfanumeryczny</span><span class="sxs-lookup"><span data-stu-id="ff68e-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="ff68e-263">Musi zawierać co najmniej jedną wielką lub małą literę</span><span class="sxs-lookup"><span data-stu-id="ff68e-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff68e-264">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff68e-264">Next steps</span></span>

<span data-ttu-id="ff68e-265">Teraz, kiedy znasz już jak tooadd tooyour ograniczony dostęp do magazynu klastra usługi HDInsight, Dowiedz się inne sposoby toowork z danymi w klastrze:</span><span class="sxs-lookup"><span data-stu-id="ff68e-265">Now that you have learned how tooadd limited-access storage tooyour HDInsight cluster, learn other ways toowork with data on your cluster:</span></span>

* [<span data-ttu-id="ff68e-266">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff68e-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ff68e-267">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff68e-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ff68e-268">Korzystać z usługi MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff68e-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
