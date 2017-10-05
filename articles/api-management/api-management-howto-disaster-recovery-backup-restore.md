---
title: "Za pomocą odzyskiwania po awarii wdrożenie i przywracania kopii zapasowych w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać kopii zapasowej i przywracania do odzyskiwania po awarii w usłudze Azure API Management."
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
ms.openlocfilehash: 07c0265490cfae733133b6e0c938f90f9b392da4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="fa1d3-103">Jak zaimplementować odzyskiwania po awarii przy użyciu usługi Kopia zapasowa i przywracanie w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="fa1d3-103">How to implement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="fa1d3-104">Przez wybranie publikowanie i zarządzanie nimi swoje interfejsy API za pomocą usługi Azure API Management są korzystanie z wielu odporność na uszkodzenia i możliwości infrastruktury, które w przeciwnym razie byłyby projektowania, wdrożenia i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span></span> <span data-ttu-id="fa1d3-105">Platforma Azure zmniejsza duża część potencjalnych błędów w ułamku kosztów.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span></span>

<span data-ttu-id="fa1d3-106">Pozwoli na odzyskanie dostępności problemów wpływających na region, w którym zarządzania infrastrukturą interfejsu API usługi jest obsługiwana, możesz przystąpić do odtworzenia z usługą w innym regionie, w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-106">To recover from availability problems affecting the region where your API Management service is hosted you should be ready to reconstitute your service in a different region at any time.</span></span> <span data-ttu-id="fa1d3-107">W zależności od dostępności cele i celu czasu odzyskiwania można zarezerwować usługi tworzenia kopii zapasowej w jednym lub więcej regionów, a następnie spróbuj Obsługa swojej konfiguracji i zawartości w synchronizacji z usługą active.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-107">Depending on your availability goals and recovery time objective  you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span></span> <span data-ttu-id="fa1d3-108">Usługa tworzenia kopii zapasowej i funkcja przywracania zapewnia niezbędne bloku konstrukcyjnego Implementowanie strategię odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-108">The service backup and restore feature provides the necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="fa1d3-109">W tym przewodniku przedstawiono sposób uwierzytelniania usługi Azure Resource Manager żądań i wykonywania kopii zapasowej i przywracania swoich wystąpień usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-109">This guide shows how to authenticate Azure Resource Manager requests, and how to backup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="fa1d3-110">Proces tworzenia kopii zapasowych i przywracanie wystąpienia usługi Zarządzanie interfejsami API dla odzyskiwania po awarii można również do replikacji wystąpień usługi Zarządzanie interfejsami API dla scenariuszy, takich jak przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="fa1d3-111">Należy pamiętać, że każda kopia zapasowa wygaśnie po upływie 30 dni.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="fa1d3-112">Próba przywrócenia kopii zapasowej, po wygaśnięciu 30-dniowy okres ważności przywracania kończy się niepowodzeniem z `Cannot restore: backup expired` wiadomości.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-112">If you attempt to restore a backup after the 30 day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="fa1d3-113">Żądań uwierzytelniania usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fa1d3-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fa1d3-114">Interfejs API REST dla kopii zapasowej i przywracania używa usługi Azure Resource Manager i ma mechanizm uwierzytelniania inny niż interfejsów API REST zarządzania jednostek zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="fa1d3-115">W tej sekcji opisano sposób do uwierzytelniania żądań usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="fa1d3-116">Aby uzyskać więcej informacji, zobacz [żądań uwierzytelniania usługi Azure Resource Manager](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa1d3-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="fa1d3-117">Wszystkie zadania, które można wykonywać na zasobów przy użyciu usługi Azure Resource Manager musi zostać uwierzytelniony w usłudze Azure Active Directory, wykonując następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps.</span></span>

* <span data-ttu-id="fa1d3-118">Dodawanie aplikacji do dzierżawy usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-118">Add an application to the Azure Active Directory tenant.</span></span>
* <span data-ttu-id="fa1d3-119">Ustawianie uprawnień dla aplikacji, który został dodany.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-119">Set permissions for the application that you added.</span></span>
* <span data-ttu-id="fa1d3-120">Pobierz token uwierzytelniania żądań do usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-120">Get the token for authenticating requests to Azure Resource Manager.</span></span>

<span data-ttu-id="fa1d3-121">Pierwszym krokiem jest, aby utworzyć aplikację usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-121">The first step is to create an Azure Active Directory application.</span></span> <span data-ttu-id="fa1d3-122">Zaloguj się do [klasycznego portalu Azure](http://manage.windowsazure.com/) korzystanie z subskrypcji, który zawiera usługi Zarządzanie interfejsami API wystąpienia, a następnie przejdź do **aplikacji** kartę domyślnej usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-122">Log into the [Azure Classic Portal](http://manage.windowsazure.com/) using the subscription that contains your API Management service instance and navigate to the **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="fa1d3-123">Jeśli domyślny katalog Azure Active Directory nie jest widoczna na koncie, skontaktuj się z administratorem subskrypcji platformy Azure można udzielić wymaganych uprawnień do konta.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-123">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span></span>

![Utwórz aplikację usługi Azure Active Directory][api-management-add-aad-application]

<span data-ttu-id="fa1d3-125">Kliknij przycisk **Dodaj**, **Dodaj aplikację moją organizację**i wybierz polecenie **aplikację Native client**.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="fa1d3-126">Wprowadź opisową nazwę, a następnie kliknij strzałkę dalej.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-126">Enter a descriptive name, and click the next arrow.</span></span> <span data-ttu-id="fa1d3-127">Wprowadź adres URL symbolu zastępczego, takich jak `http://resources` dla **identyfikator URI przekierowania**, ponieważ jest to wymagane pole, ale nie jest używana wartość później.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-127">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span></span> <span data-ttu-id="fa1d3-128">Kliknij pole wyboru, aby zapisać aplikację.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-128">Click the check box to save the application.</span></span>

<span data-ttu-id="fa1d3-129">Po zapisaniu aplikacji, kliknij przycisk **Konfiguruj**, przewiń w dół do **uprawnień dotyczących innych aplikacji** sekcji, a następnie kliknij polecenie **Dodaj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-129">Once the application is saved, click **Configure**, scroll down to the **permissions to other applications** section, and click **Add application**.</span></span>

![Dodaj uprawnienia][api-management-aad-permissions-add]

<span data-ttu-id="fa1d3-131">Wybierz **Windows** **interfejs API zarządzania usługami Azure** i kliknij przycisk wyboru, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-131">Select **Windows** **Azure Service Management API** and click the checkbox to add the application.</span></span>

![Dodaj uprawnienia][api-management-aad-permissions]

<span data-ttu-id="fa1d3-133">Kliknij przycisk **delegowane uprawnienia** obok nowo dodanego **Windows** **interfejs API zarządzania usługami Azure** aplikacji, pole wyboru dla **dostępu do usługi Azure Service Management (wersja zapoznawcza)**i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-133">Click **Delegated Permissions** beside the newly added **Windows** **Azure Service Management API** application, check the box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Dodaj uprawnienia][api-management-aad-delegated-permissions]

<span data-ttu-id="fa1d3-135">Przed wywołaniem interfejsów API, które Generowanie kopii zapasowej i przywrócenie go, należy uzyskać token.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-135">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span></span> <span data-ttu-id="fa1d3-136">W poniższym przykładzie użyto [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) pakiet nuget w celu pobrania tokenu.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-136">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package to retrieve the token.</span></span>

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
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="fa1d3-137">Zastąp `{tentand id}`, `{application id}`, i `{redirect uri}` z poniższymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions.</span></span>

<span data-ttu-id="fa1d3-138">Zastąp `{tenant id}` o identyfikatorze dzierżawy utworzoną aplikację usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-138">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you just created.</span></span> <span data-ttu-id="fa1d3-139">Identyfikator można uzyskać, klikając **wyświetlić punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-139">You can access the id by clicking **View endpoints**.</span></span>

![Punkty końcowe][api-management-aad-default-directory]

![Punkty końcowe][api-management-endpoint]

<span data-ttu-id="fa1d3-142">Zastąp `{application id}` i `{redirect uri}` przy użyciu **identyfikator klienta** i adres URL z **identyfikator URI przekierowania** sekcji z poziomu aplikacji usługi Azure Active Directory **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-142">Replace `{application id}` and `{redirect uri}` using the **Client Id** and  the URL from the **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Zasoby][api-management-aad-resources]

<span data-ttu-id="fa1d3-144">Po wartości są określone, przykładowy kod powinien zwrócić token podobny do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-144">Once the values are specified, the code example should return a token similar to the following example.</span></span>

![Token][api-management-arm-token]

<span data-ttu-id="fa1d3-146">Przed wywołaniem metody tworzenia kopii zapasowej i przywracania czynności opisane w poniższych sekcjach, ustaw nagłówek żądania autoryzacji dla wywołania REST.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-146">Before calling the backup and restore operations described in the following sections, set the authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="fa1d3-147"><a name="step1"></a>Utwórz kopię zapasową usługi Zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="fa1d3-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="fa1d3-148">Aby utworzyć kopię zapasową problem dotyczący usługi Zarządzanie interfejsami API następujące żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="fa1d3-148">To back up an API Management service issue the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="fa1d3-149">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="fa1d3-149">where:</span></span>

* <span data-ttu-id="fa1d3-150">`subscriptionId`— Identyfikator subskrypcji zawierający usługi Zarządzanie interfejsami API próbujesz do kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="fa1d3-150">`subscriptionId` - id of the subscription containing the API Management service you are attempting to backup</span></span>
* <span data-ttu-id="fa1d3-151">`resourceGroupName`-ciąg w formie "Api - Domyślnie — {usługi region}" gdzie `service-region` identyfikuje region platformy Azure, gdzie zarządzanie interfejsami API usługi próbujesz kopii zapasowej jest obsługiwany, np.`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="fa1d3-151">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are trying to backup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="fa1d3-152">`serviceName`-Nazwa usługi Zarządzanie interfejsami API tworzysz kopię zapasową określony w momencie jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-152">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span></span>
* <span data-ttu-id="fa1d3-153">`api-version`-Zamień`2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="fa1d3-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="fa1d3-154">W treści żądania Określ nazwę konta magazynu Azure docelowej, klucz dostępu, nazwa kontenera obiektów blob i nazwa kopii zapasowej:</span><span class="sxs-lookup"><span data-stu-id="fa1d3-154">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="fa1d3-155">Ustaw wartość `Content-Type` nagłówek żądania do `application/json`.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-155">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="fa1d3-156">Kopia zapasowa jest operacją wymagającą dużo czasu, który może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-156">Backup is a long running operation that may take multiple minutes to complete.</span></span>  <span data-ttu-id="fa1d3-157">Jeśli żądanie zostało wykonane i zainicjowano proces tworzenia kopii zapasowej otrzymasz `202 Accepted` kod stanu odpowiedzi z `Location` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-157">If the request was successful and the backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="fa1d3-158">Upewnij się, "GET" żądania na adres URL w `Location` nagłówka, aby sprawdzić stan operacji.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-158">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="fa1d3-159">W trakcie tworzenia kopii zapasowej możesz nadal będziesz otrzymywać kodu stanu "202 zaakceptowane".</span><span class="sxs-lookup"><span data-stu-id="fa1d3-159">While the backup is in progress you will continue to receive a '202 Accepted' status code.</span></span> <span data-ttu-id="fa1d3-160">Kod odpowiedzi `200 OK` wskaże, że ukończenie operacji tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-160">A Response code of `200 OK` will indicate successful completion of the backup operation.</span></span>

<span data-ttu-id="fa1d3-161">Należy pamiętać następujące ograniczenia, podczas tworzenia kopii zapasowej żądania.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-161">Please note the following constraints when making a backup request.</span></span>

* <span data-ttu-id="fa1d3-162">**Kontener** określony w treści żądania **musi istnieć**.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-162">**Container** specified in the request body **must exist**.</span></span>
* <span data-ttu-id="fa1d3-163">Gdy trwa wykonywanie kopii zapasowej możesz **nie powinny podejmować żadnych operacji zarządzania usługi** takich jak jednostki SKU uaktualnienia lub starszą wersję, zmiana nazwy domeny, itp.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="fa1d3-164">Przywracanie **kopii zapasowej jest gwarantowana tylko przez 30 dni** od momentu jego utworzenia.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-164">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span></span>
* <span data-ttu-id="fa1d3-165">**Dane użycia** używany do tworzenia raportów analizy **nie jest dołączana** w kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-165">**Usage data** used for creating analytics reports **is not included** in the backup.</span></span> <span data-ttu-id="fa1d3-166">Użyj [interfejsu API REST Azure API Management] [ Azure API Management REST API] okresowo pobrać raportów analizy w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-166">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="fa1d3-167">Częstotliwość, z którym wykonywanie kopii zapasowych usługi będzie miało wpływ na celu punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-167">The frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="fa1d3-168">Aby zminimalizować zaleca się implementowania regularnych kopii zapasowych, a także wykonywanie kopii zapasowych na żądanie po wprowadzeniu istotnych zmian do usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-168">To minimize it we advise implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span></span>
* <span data-ttu-id="fa1d3-169">**Zmiany** wprowadzone w konfiguracji usługi (np. interfejsów API, zasady, wygląd portalu deweloperów) podczas tworzenia kopii zapasowej operacja jest w toku **mogą nie zostać uwzględnione w kopii zapasowej i w związku z tym zostaną utracone**.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-169">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span></span>

## <span data-ttu-id="fa1d3-170"><a name="step2"></a>Przywrócenia usługi Zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="fa1d3-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="fa1d3-171">Aby przywrócić zarządzanie interfejsami API usługi z kopii zapasowej utworzonej wcześniej upewnij następujące żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="fa1d3-171">To restore an API Management service from a previously created backup make the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="fa1d3-172">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="fa1d3-172">where:</span></span>

* <span data-ttu-id="fa1d3-173">`subscriptionId`— Identyfikator subskrypcji zawierający usługi Zarządzanie interfejsami API są przywracanie kopii zapasowej do</span><span class="sxs-lookup"><span data-stu-id="fa1d3-173">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="fa1d3-174">`resourceGroupName`-ciąg w formie "Api - Domyślnie — {usługi region}" gdzie `service-region` identyfikuje region platformy Azure, gdzie jest hostowana usługa API Management przywracania kopii zapasowej do, np.`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="fa1d3-174">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="fa1d3-175">`serviceName`-Nazwa zarządzanie interfejsami API usługi są przywracane do określonych w momencie jego tworzenia</span><span class="sxs-lookup"><span data-stu-id="fa1d3-175">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span></span>
* <span data-ttu-id="fa1d3-176">`api-version`-Zamień`2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="fa1d3-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="fa1d3-177">W treści żądania Określ lokalizację pliku kopii zapasowej, tj. Nazwa konta magazynu platformy Azure, klucz dostępu, nazwa kontenera obiektów blob i nazwa kopii zapasowej:</span><span class="sxs-lookup"><span data-stu-id="fa1d3-177">In the body of the request, specify the backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="fa1d3-178">Ustaw wartość `Content-Type` nagłówek żądania do `application/json`.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-178">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="fa1d3-179">Przywracanie jest operacją wymagającą dużo czasu, który może potrwać do co najmniej 30 minut, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-179">Restore is a long running operation that may take up to 30 or more minutes to complete.</span></span>  <span data-ttu-id="fa1d3-180">Jeśli żądanie zostało wykonane i zainicjowano proces przywracania otrzymasz `202 Accepted` kod stanu odpowiedzi z `Location` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-180">If the request was successful and the restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="fa1d3-181">Upewnij się, "GET" żądania na adres URL w `Location` nagłówka, aby sprawdzić stan operacji.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-181">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="fa1d3-182">W trakcie przywracania będzie odbierać "202 zaakceptowane" Kod stanu.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-182">While the restore is in progress you will continue to receive '202 Accepted' status code.</span></span> <span data-ttu-id="fa1d3-183">Kod odpowiedzi `200 OK` będą wskazywać pomyślne zakończenie operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-183">A response code of `200 OK` will indicate successful completion of the restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa1d3-184">**Jednostka SKU** usługi są przywracane do **musi odpowiadać** jednostki SKU usługi kopii zapasowej przywracanej.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-184">**The SKU** of the service being restored into **must match** the SKU of the backed up service being restored.</span></span>
>
> <span data-ttu-id="fa1d3-185">**Zmiany** wprowadzone w konfiguracji usługi (np. interfejsów API, zasady, wygląd portalu deweloperów) podczas przywracania operacja jest w toku **mogą zostać zastąpione**.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-185">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="fa1d3-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa1d3-186">Next steps</span></span>
<span data-ttu-id="fa1d3-187">Zapoznaj się z następujących blogach firmy Microsoft dla dwóch różnych wskazówki dotyczące procesu tworzenia kopii zapasowej/przywracania.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-187">Check out the following Microsoft blogs for two different walkthroughs of the backup/restore process.</span></span>

* [<span data-ttu-id="fa1d3-188">Replikowanie usługi Azure API Management kont</span><span class="sxs-lookup"><span data-stu-id="fa1d3-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="fa1d3-189">Dziękujemy do Gisela dla swojego udziału w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-189">Thank you to Gisela for her contribution to this article.</span></span>
* [<span data-ttu-id="fa1d3-190">Usługi Azure API Management: Tworzenie kopii zapasowej i przywracanie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="fa1d3-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="fa1d3-191">Podejście szczegółowych przy Stuart jest niezgodny z oficjalnego wytyczne, ale jest bardzo interesujące.</span><span class="sxs-lookup"><span data-stu-id="fa1d3-191">The approach detailed by Stuart does not match the official guidance but it is very interesting.</span></span>

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
