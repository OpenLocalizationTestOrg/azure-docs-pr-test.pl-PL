---
title: "za pomocą odzyskiwania po awarii aaaImplement i przywracania kopii zapasowych w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse kopia zapasowa i przywracanie tooperform odzyskiwania po awarii w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="501c1-103">Jak za pomocą odzyskiwania po awarii tooimplement usługi tworzenia kopii zapasowej i przywracania w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="501c1-103">How tooimplement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="501c1-104">Przez wybranie toopublish i zarządzanie nimi swoje interfejsy API za pomocą usługi Azure API Management wykorzystaniu wielu odporność na uszkodzenia i infrastruktury możliwości, które w przeciwnym razie trzeba toodesign, wdrożenia i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="501c1-104">By choosing toopublish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have toodesign, implement, and manage.</span></span> <span data-ttu-id="501c1-105">Witaj platformy Azure zmniejsza duża część potencjalnych błędów w ułamku hello kosztów.</span><span class="sxs-lookup"><span data-stu-id="501c1-105">hello Azure platform mitigates a large fraction of potential failures at a fraction of hello cost.</span></span>

<span data-ttu-id="501c1-106">toorecover od dostępności problemów wpływających na powitania regionu, w którym usługi Zarządzanie interfejsami API hostowany możesz powinna być gotowe tooreconstitute usługi w innym regionie w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="501c1-106">toorecover from availability problems affecting hello region where your API Management service is hosted you should be ready tooreconstitute your service in a different region at any time.</span></span> <span data-ttu-id="501c1-107">W zależności od dostępności cele i celu czasu odzyskiwania może mają tooreserve usługi tworzenia kopii zapasowej w jednym lub więcej regionów i spróbuj toomaintain swojej konfiguracji i zawartości w synchronizacji z usługą active hello.</span><span class="sxs-lookup"><span data-stu-id="501c1-107">Depending on your availability goals and recovery time objective  you might want tooreserve a backup service in one or more regions and try toomaintain their configuration and content in sync with hello active service.</span></span> <span data-ttu-id="501c1-108">Witaj usługi tworzenia kopii zapasowej i funkcja przywracania zapewnia niezbędne bloków konstrukcyjnych hello Implementowanie strategię odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="501c1-108">hello service backup and restore feature provides hello necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="501c1-109">W tym przewodniku przedstawiono sposób żądań tooauthenticate usługi Azure Resource Manager i w jaki sposób toobackup i przywrócić swoich wystąpień usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="501c1-109">This guide shows how tooauthenticate Azure Resource Manager requests, and how toobackup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="501c1-110">można także Hello procesu tworzenia kopii zapasowych i przywracanie wystąpienia usługi Zarządzanie interfejsami API dla odzyskiwania po awarii do replikowania wystąpień usługi Zarządzanie interfejsami API dla scenariuszy, takich jak przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="501c1-110">hello process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="501c1-111">Należy pamiętać, że każda kopia zapasowa wygaśnie po upływie 30 dni.</span><span class="sxs-lookup"><span data-stu-id="501c1-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="501c1-112">Jeśli toorestore kopii zapasowej po wygaśnięciu okresu wygaśnięcia 30-dniowej hello, przywracania hello zakończy się niepowodzeniem z `Cannot restore: backup expired` wiadomości.</span><span class="sxs-lookup"><span data-stu-id="501c1-112">If you attempt toorestore a backup after hello 30 day expiration period has expired, hello restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="501c1-113">Żądań uwierzytelniania usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="501c1-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="501c1-114">Hello interfejsu API REST dla kopii zapasowej i przywracania używa usługi Azure Resource Manager i ma mechanizm uwierzytelniania inny niż hello interfejsów API REST zarządzania jednostek zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="501c1-114">hello REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than hello REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="501c1-115">Witaj w tej sekcji opisano sposób żądań tooauthenticate usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="501c1-115">hello steps in this section describe how tooauthenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="501c1-116">Aby uzyskać więcej informacji, zobacz [żądań uwierzytelniania usługi Azure Resource Manager](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="501c1-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="501c1-117">Wszystkie zadania hello, które można wykonywać na zasobów przy użyciu usługi Azure Resource Manager hello musi zostać uwierzytelniony w usłudze Azure Active Directory przy użyciu hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="501c1-117">All of hello tasks that you do on resources using hello Azure Resource Manager must be authenticated with Azure Active Directory using hello following steps.</span></span>

* <span data-ttu-id="501c1-118">Dodaj dzierżawę usługi Azure Active Directory toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="501c1-118">Add an application toohello Azure Active Directory tenant.</span></span>
* <span data-ttu-id="501c1-119">Ustawianie uprawnień dla aplikacji hello, który został dodany.</span><span class="sxs-lookup"><span data-stu-id="501c1-119">Set permissions for hello application that you added.</span></span>
* <span data-ttu-id="501c1-120">Pobierz hello token do uwierzytelniania żądań tooAzure Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="501c1-120">Get hello token for authenticating requests tooAzure Resource Manager.</span></span>

<span data-ttu-id="501c1-121">pierwszym krokiem Hello jest toocreate aplikację usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="501c1-121">hello first step is toocreate an Azure Active Directory application.</span></span> <span data-ttu-id="501c1-122">Zaloguj się do hello [klasycznego portalu Azure](http://manage.windowsazure.com/) przy użyciu subskrypcji hello, który zawiera usługi Zarządzanie interfejsami API wystąpienia, a następnie przejdź toohello **aplikacji** kartę domyślnej usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="501c1-122">Log into hello [Azure Classic Portal](http://manage.windowsazure.com/) using hello subscription that contains your API Management service instance and navigate toohello **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="501c1-123">Jeśli hello Azure Active Directory domyślny katalog nie jest widoczne tooyour konta, administrator kontaktu hello Witaj Witaj toogrant subskrypcji platformy Azure wymagane uprawnienia tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="501c1-123">If hello Azure Active Directory default directory is not visible tooyour account, contact hello administrator of hello Azure subscription toogrant hello required permissions tooyour account.</span></span>

![Utwórz aplikację usługi Azure Active Directory][api-management-add-aad-application]

<span data-ttu-id="501c1-125">Kliknij przycisk **Dodaj**, **Dodaj aplikację moją organizację**i wybierz polecenie **aplikację Native client**.</span><span class="sxs-lookup"><span data-stu-id="501c1-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="501c1-126">Wprowadź opisową nazwę, a następnie kliknij strzałkę dalej hello.</span><span class="sxs-lookup"><span data-stu-id="501c1-126">Enter a descriptive name, and click hello next arrow.</span></span> <span data-ttu-id="501c1-127">Wprowadź adres URL symbolu zastępczego, takich jak `http://resources` dla hello **identyfikator URI przekierowania**, ponieważ jest to wymagane pole, ale hello nie jest używana wartość później.</span><span class="sxs-lookup"><span data-stu-id="501c1-127">Enter a placeholder URL such as `http://resources` for hello **Redirect URI**, as it is a required field, but hello value is not used later.</span></span> <span data-ttu-id="501c1-128">Kliknij przycisk hello pole wyboru toosave hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="501c1-128">Click hello check box toosave hello application.</span></span>

<span data-ttu-id="501c1-129">Po zapisaniu aplikacji hello, kliknij przycisk **Konfiguruj**, przewiń w dół toohello **uprawnienia aplikacji tooother** sekcji, a następnie kliknij polecenie **Dodaj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="501c1-129">Once hello application is saved, click **Configure**, scroll down toohello **permissions tooother applications** section, and click **Add application**.</span></span>

![Dodaj uprawnienia][api-management-aad-permissions-add]

<span data-ttu-id="501c1-131">Wybierz **Windows** **interfejs API zarządzania usługami Azure** i kliknij przycisk hello wyboru tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="501c1-131">Select **Windows** **Azure Service Management API** and click hello checkbox tooadd hello application.</span></span>

![Dodaj uprawnienia][api-management-aad-permissions]

<span data-ttu-id="501c1-133">Kliknij przycisk **delegowane uprawnienia** obok hello nowo dodanych **Windows** **interfejs API zarządzania usługami Azure** aplikacji, pole wyboru hello **Azure dostępu Zarządzanie usługami (wersja zapoznawcza)**i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="501c1-133">Click **Delegated Permissions** beside hello newly added **Windows** **Azure Service Management API** application, check hello box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Dodaj uprawnienia][api-management-aad-delegated-permissions]

<span data-ttu-id="501c1-135">Wcześniejsze tooinvoking hello interfejsów API, który generuje hello kopii zapasowej i przywrócenie go, jest konieczne tooget tokenu.</span><span class="sxs-lookup"><span data-stu-id="501c1-135">Prior tooinvoking hello APIs that generate hello backup and restore it, it is necessary tooget a token.</span></span> <span data-ttu-id="501c1-136">Witaj poniższym przykładzie użyto hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) token hello tooretrieve pakietu nuget.</span><span class="sxs-lookup"><span data-stu-id="501c1-136">hello following example uses hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package tooretrieve hello token.</span></span>

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="501c1-137">Zastąp `{tentand id}`, `{application id}`, i `{redirect uri}` przy użyciu hello, postępując zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="501c1-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using hello following instructions.</span></span>

<span data-ttu-id="501c1-138">Zastąp `{tenant id}` o identyfikatorze dzierżawy hello hello utworzoną aplikację usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="501c1-138">Replace `{tenant id}` with hello tenant id of hello Azure Active Directory application you just created.</span></span> <span data-ttu-id="501c1-139">Identyfikator hello można uzyskać, klikając **wyświetlić punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="501c1-139">You can access hello id by clicking **View endpoints**.</span></span>

![Punkty końcowe][api-management-aad-default-directory]

![Punkty końcowe][api-management-endpoint]

<span data-ttu-id="501c1-142">Zastąp `{application id}` i `{redirect uri}` przy użyciu hello **identyfikator klienta** i hello adres URL z hello **identyfikator URI przekierowania** sekcji z poziomu aplikacji usługi Azure Active Directory **Konfiguruj**  kartę.</span><span class="sxs-lookup"><span data-stu-id="501c1-142">Replace `{application id}` and `{redirect uri}` using hello **Client Id** and  hello URL from hello **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Zasoby][api-management-aad-resources]

<span data-ttu-id="501c1-144">Po hello wartości są określone, hello przykładowy kod powinien zwrócić token toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="501c1-144">Once hello values are specified, hello code example should return a token similar toohello following example.</span></span>

![Token][api-management-arm-token]

<span data-ttu-id="501c1-146">Przed wywołaniem hello kopii zapasowej i przywracania czynności opisane w hello następujące sekcje, ustaw nagłówek żądania autoryzacji hello połączenia REST.</span><span class="sxs-lookup"><span data-stu-id="501c1-146">Before calling hello backup and restore operations described in hello following sections, set hello authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="501c1-147"><a name="step1"></a>Utwórz kopię zapasową usługi Zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="501c1-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="501c1-148">tooback się hello problem usługi Zarządzanie interfejsami API następujące żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="501c1-148">tooback up an API Management service issue hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="501c1-149">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="501c1-149">where:</span></span>

* <span data-ttu-id="501c1-150">`subscriptionId`— Identyfikator subskrypcji hello zawierający usługi Zarządzanie interfejsami API hello próbujesz toobackup</span><span class="sxs-lookup"><span data-stu-id="501c1-150">`subscriptionId` - id of hello subscription containing hello API Management service you are attempting toobackup</span></span>
* <span data-ttu-id="501c1-151">`resourceGroupName`-ciąg w formie "Api - Domyślnie — {usługi region}" hello gdzie `service-region` identyfikuje hello region platformy Azure, gdzie jest hostowana hello próbujesz toobackup usługi Zarządzanie interfejsami API, np.`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="501c1-151">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are trying toobackup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="501c1-152">`serviceName`-Nazwa hello hello usługi Zarządzanie interfejsami API określona w momencie jego tworzenia hello są tworzenie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="501c1-152">`serviceName` - hello name of hello API Management service you are making a backup of specified at hello time of its creation</span></span>
* <span data-ttu-id="501c1-153">`api-version`-Zamień`2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="501c1-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="501c1-154">W treści żądania hello hello Określ nazwę konta magazynu Azure docelowy hello, klucz dostępu, nazwa kontenera obiektów blob i nazwa kopii zapasowej:</span><span class="sxs-lookup"><span data-stu-id="501c1-154">In hello body of hello request, specify hello target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="501c1-155">Ustaw wartość hello hello `Content-Type` nagłówek żądania zbyt`application/json`.</span><span class="sxs-lookup"><span data-stu-id="501c1-155">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="501c1-156">Kopia zapasowa jest operacją wymagającą dużo czasu, który może potrwać kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="501c1-156">Backup is a long running operation that may take multiple minutes toocomplete.</span></span>  <span data-ttu-id="501c1-157">Jeśli Żądanie hello powiodło się i zainicjowano proces tworzenia kopii zapasowej hello otrzymasz `202 Accepted` kod stanu odpowiedzi z `Location` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="501c1-157">If hello request was successful and hello backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="501c1-158">Marka "GET" żądań URL toohello w hello `Location` toofind nagłówka się stan hello hello operacji.</span><span class="sxs-lookup"><span data-stu-id="501c1-158">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="501c1-159">W trakcie tworzenia kopii zapasowej hello będzie tooreceive kodu stanu "202 zaakceptowane".</span><span class="sxs-lookup"><span data-stu-id="501c1-159">While hello backup is in progress you will continue tooreceive a '202 Accepted' status code.</span></span> <span data-ttu-id="501c1-160">Kod odpowiedzi `200 OK` wskaże, że ukończenie operacji tworzenia kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="501c1-160">A Response code of `200 OK` will indicate successful completion of hello backup operation.</span></span>

<span data-ttu-id="501c1-161">Należy pamiętać, hello następujące ograniczenia, podczas tworzenia kopii zapasowej żądania.</span><span class="sxs-lookup"><span data-stu-id="501c1-161">Please note hello following constraints when making a backup request.</span></span>

* <span data-ttu-id="501c1-162">**Kontener** określony w treści żądania hello **musi istnieć**.</span><span class="sxs-lookup"><span data-stu-id="501c1-162">**Container** specified in hello request body **must exist**.</span></span>
* <span data-ttu-id="501c1-163">Gdy trwa wykonywanie kopii zapasowej możesz **nie powinny podejmować żadnych operacji zarządzania usługi** takich jak jednostki SKU uaktualnienia lub starszą wersję, zmiana nazwy domeny, itp.</span><span class="sxs-lookup"><span data-stu-id="501c1-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="501c1-164">Przywracanie **kopii zapasowej jest gwarantowana tylko przez 30 dni** od hello momencie jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="501c1-164">Restore of a **backup is guaranteed only for 30 days** since hello moment of its creation.</span></span>
* <span data-ttu-id="501c1-165">**Dane użycia** używany do tworzenia raportów analizy **nie jest dołączana** hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="501c1-165">**Usage data** used for creating analytics reports **is not included** in hello backup.</span></span> <span data-ttu-id="501c1-166">Użyj [interfejsu API REST Azure API Management] [ Azure API Management REST API] tooperiodically pobrać raportów analizy w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="501c1-166">Use [Azure API Management REST API][Azure API Management REST API] tooperiodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="501c1-167">Hello częstotliwość, z którym wykonywanie kopii zapasowych usługi będzie miało wpływ na celu punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="501c1-167">hello frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="501c1-168">toominimize go zaleca się wdrożenie regularnych kopii zapasowych, a także wykonywanie kopii zapasowych na żądanie po wprowadzeniu ważne zmiany usługi Zarządzanie interfejsami API tooyour.</span><span class="sxs-lookup"><span data-stu-id="501c1-168">toominimize it we advise implementing regular backups as well as performing on-demand backups after making important changes tooyour API Management service.</span></span>
* <span data-ttu-id="501c1-169">**Zmiany** toohello dokonano konfiguracji usługi (np. interfejsów API, zasady, wygląd portalu deweloperów) podczas operacji tworzenia kopii zapasowej jest w toku **mogą nie zostać uwzględnione w kopii zapasowej hello i w związku z tym zostaną utracone**.</span><span class="sxs-lookup"><span data-stu-id="501c1-169">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in hello backup and therefore will be lost**.</span></span>

## <span data-ttu-id="501c1-170"><a name="step2"></a>Przywrócenia usługi Zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="501c1-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="501c1-171">toorestore usługi API Management z wcześniej utworzonej kopii zapasowej należy hello następujące żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="501c1-171">toorestore an API Management service from a previously created backup make hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="501c1-172">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="501c1-172">where:</span></span>

* <span data-ttu-id="501c1-173">`subscriptionId`— Identyfikator subskrypcji hello zawierający usługi Zarządzanie interfejsami API hello są przywracanie kopii zapasowej do</span><span class="sxs-lookup"><span data-stu-id="501c1-173">`subscriptionId` - id of hello subscription containing hello API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="501c1-174">`resourceGroupName`-ciąg w formie "Api - Domyślnie — {usługi region}" hello gdzie `service-region` identyfikuje hello region platformy Azure, gdzie jest hostowana hello są przywracanie kopii zapasowej do usługi API Management, np.`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="501c1-174">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="501c1-175">`serviceName`-Nazwa hello hello zarządzanie interfejsami API usługi są przywracane do określonego na powitania czasu jej utworzenia</span><span class="sxs-lookup"><span data-stu-id="501c1-175">`serviceName` - hello name of hello API Management service being restored into specified at hello time of its creation</span></span>
* <span data-ttu-id="501c1-176">`api-version`-Zamień`2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="501c1-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="501c1-177">W treści hello hello żądania Określ lokalizację pliku kopii zapasowej hello, tj. Nazwa konta magazynu platformy Azure, klucz dostępu, nazwa kontenera obiektów blob i nazwa kopii zapasowej:</span><span class="sxs-lookup"><span data-stu-id="501c1-177">In hello body of hello request, specify hello backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="501c1-178">Ustaw wartość hello hello `Content-Type` nagłówek żądania zbyt`application/json`.</span><span class="sxs-lookup"><span data-stu-id="501c1-178">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="501c1-179">Przywracanie jest operacją wymagającą dużo czasu, który może potrwać too30 lub więcej toocomplete minut.</span><span class="sxs-lookup"><span data-stu-id="501c1-179">Restore is a long running operation that may take up too30 or more minutes toocomplete.</span></span>  <span data-ttu-id="501c1-180">Jeśli Żądanie hello powiodło się i został zainicjowany proces przywracania hello otrzymasz `202 Accepted` kod stanu odpowiedzi z `Location` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="501c1-180">If hello request was successful and hello restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="501c1-181">Marka "GET" żądań URL toohello w hello `Location` toofind nagłówka się stan hello hello operacji.</span><span class="sxs-lookup"><span data-stu-id="501c1-181">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="501c1-182">W trakcie przywracania hello będzie kod stanu tooreceive "202 zaakceptowane".</span><span class="sxs-lookup"><span data-stu-id="501c1-182">While hello restore is in progress you will continue tooreceive '202 Accepted' status code.</span></span> <span data-ttu-id="501c1-183">Kod odpowiedzi `200 OK` będą wskazywać pomyślne zakończenie operacji przywracania hello.</span><span class="sxs-lookup"><span data-stu-id="501c1-183">A response code of `200 OK` will indicate successful completion of hello restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="501c1-184">**Hello SKU** usługi hello są przywracane do **musi odpowiadać** hello SKU hello kopii zapasowej przywracanej usługi.</span><span class="sxs-lookup"><span data-stu-id="501c1-184">**hello SKU** of hello service being restored into **must match** hello SKU of hello backed up service being restored.</span></span>
>
> <span data-ttu-id="501c1-185">**Zmiany** toohello dokonano konfiguracji usługi (np. interfejsów API, zasady, wygląd portalu deweloperów) podczas operacji przywracania jest w toku **mogą zostać zastąpione**.</span><span class="sxs-lookup"><span data-stu-id="501c1-185">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="501c1-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="501c1-186">Next steps</span></span>
<span data-ttu-id="501c1-187">Zapoznaj się z następujących blogach firmy Microsoft dla dwóch różnych wskazówki dotyczące procesu tworzenia kopii zapasowej/przywracania hello hello.</span><span class="sxs-lookup"><span data-stu-id="501c1-187">Check out hello following Microsoft blogs for two different walkthroughs of hello backup/restore process.</span></span>

* [<span data-ttu-id="501c1-188">Replikowanie usługi Azure API Management kont</span><span class="sxs-lookup"><span data-stu-id="501c1-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="501c1-189">Dziękujemy tooGisela dla swojego udziału toothis artykułu.</span><span class="sxs-lookup"><span data-stu-id="501c1-189">Thank you tooGisela for her contribution toothis article.</span></span>
* [<span data-ttu-id="501c1-190">Usługi Azure API Management: Tworzenie kopii zapasowej i przywracanie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="501c1-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="501c1-191">podejście Hello szczegółowych przy Stuart jest niezgodna z oficjalnego wskazówki hello, ale jest bardzo interesujące.</span><span class="sxs-lookup"><span data-stu-id="501c1-191">hello approach detailed by Stuart does not match hello official guidance but it is very interesting.</span></span>

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
