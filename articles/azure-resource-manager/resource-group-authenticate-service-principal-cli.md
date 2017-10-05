---
title: "Utwórz tożsamość aplikacji usługi Azure z wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób użycia interfejsu wiersza polecenia Azure do tworzenia aplikacji usługi Azure Active Directory i nazwę główną usługi i przyznać jej dostęp do zasobów za pomocą kontroli dostępu opartej na rolach. Widoczny jest sposób uwierzytelniania aplikacji za pomocą hasła lub certyfikatu."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 3c5826d58887ff1af4df8e66999d9c1a1643bcc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-cli-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="9432b-104">Use Azure CLI to create a service principal to access resources (Tworzenie jednostki usługi używanej do uzyskiwania dostępu do zasobów przy użyciu interfejsu wiersza polecenia platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="9432b-104">Use Azure CLI to create a service principal to access resources</span></span>

<span data-ttu-id="9432b-105">Jeśli aplikacji lub skryptu, który ma dostęp do zasobów, można skonfigurować tożsamości aplikacji i uwierzytelniania w aplikacji przy użyciu własne poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="9432b-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="9432b-106">Ta tożsamość jest określany jako nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="9432b-106">This identity is known as a service principal.</span></span> <span data-ttu-id="9432b-107">Takie podejście umożliwia:</span><span class="sxs-lookup"><span data-stu-id="9432b-107">This approach enables you to:</span></span>

* <span data-ttu-id="9432b-108">Przypisanie uprawnień do tożsamości aplikacji, które są inne niż własnych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="9432b-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="9432b-109">Zazwyczaj te uprawnienia są ograniczone do dokładnie co aplikacja powinna wykonać.</span><span class="sxs-lookup"><span data-stu-id="9432b-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="9432b-110">Użyj certyfikatu do uwierzytelnienia, podczas wykonywania skryptu instalacji nienadzorowanej.</span><span class="sxs-lookup"><span data-stu-id="9432b-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="9432b-111">W tym artykule przedstawiono sposób użycia [Azure CLI 1.0](../cli-install-nodejs.md) do skonfigurowania aplikacji do uruchamiania w własne poświadczenia i tożsamości.</span><span class="sxs-lookup"><span data-stu-id="9432b-111">This article shows you how to use [Azure CLI 1.0](../cli-install-nodejs.md) to set up an application to run under its own credentials and identity.</span></span> <span data-ttu-id="9432b-112">Zainstaluj najnowszą wersję pakietu [Azure CLI 1.0](../cli-install-nodejs.md) się upewnić, że środowisko odpowiada przykłady w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="9432b-112">Install the latest version of [Azure CLI 1.0](../cli-install-nodejs.md) to make sure your environment matches the examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="9432b-113">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="9432b-113">Required permissions</span></span>
<span data-ttu-id="9432b-114">Do ukończenia tego tematu, należy posiadać odpowiednie uprawnienia w usłudze Azure Active Directory i Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9432b-114">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="9432b-115">W szczególności należy utworzyć aplikację w usłudze Azure Active Directory i przypisać nazwę główną usługi do roli.</span><span class="sxs-lookup"><span data-stu-id="9432b-115">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="9432b-116">Najłatwiejszym sposobem sprawdzenia, czy Twoje konto ma odpowiednie uprawnienia, jest skorzystanie z portalu.</span><span class="sxs-lookup"><span data-stu-id="9432b-116">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="9432b-117">Zobacz [Sprawdzanie wymaganego uprawnienia w portalu](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="9432b-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="9432b-118">Teraz, przejdź do sekcji w obu [hasło](#create-service-principal-with-password) lub [certyfikatu](#create-service-principal-with-certificate) uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="9432b-118">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="9432b-119">Tworzenie nazwy głównej usługi z hasłem</span><span class="sxs-lookup"><span data-stu-id="9432b-119">Create service principal with password</span></span>
<span data-ttu-id="9432b-120">W tej sekcji wykonaj kroki umożliwiające utworzenie aplikacji usługi AD przy użyciu hasła i przypisać rolę czytelnika do nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="9432b-120">In this section, you perform the steps to create the AD application with a password, and assign the Reader role to the service principal.</span></span>

1. <span data-ttu-id="9432b-121">Zaloguj się do swojego konta.</span><span class="sxs-lookup"><span data-stu-id="9432b-121">Sign in to your account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="9432b-122">Aby utworzyć tożsamość aplikacji, należy podać nazwę aplikacji i hasło, jak pokazano w poniższym poleceniu:</span><span class="sxs-lookup"><span data-stu-id="9432b-122">To create an app identity, provide the name of the app and a password, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="9432b-123">Zwracany jest nową główną nazwę usługi.</span><span class="sxs-lookup"><span data-stu-id="9432b-123">The new service principal is returned.</span></span> <span data-ttu-id="9432b-124">Identyfikator obiektu jest potrzebna do przyznawania uprawnień.</span><span class="sxs-lookup"><span data-stu-id="9432b-124">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="9432b-125">Identyfikator guid na liście z główne nazwy usług jest potrzebne podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="9432b-125">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="9432b-126">Ten identyfikator guid jest taką samą wartość jak identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9432b-126">This guid is the same value as the app id.</span></span> <span data-ttu-id="9432b-127">W przykładowych aplikacji, ta wartość jest określana jako `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="9432b-127">In the sample applications, this value is referred to as the `Client ID`.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. <span data-ttu-id="9432b-128">Przyznaj uprawnienia głównej usługi w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9432b-128">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="9432b-129">W tym przykładzie należy dodać nazwy głównej usługi do roli Czytelnik, co powoduje przyznanie uprawnień do odczytu wszystkich zasobów w subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9432b-129">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="9432b-130">Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="9432b-130">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="9432b-131">Dla parametru objectid Podaj identyfikator obiektu, który został użyty podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9432b-131">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="9432b-132">Przed uruchomieniem tego polecenia, musisz zezwolić na pewien czas dla nowej nazwy głównej usługi propagację w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9432b-132">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="9432b-133">Po uruchomieniu tych poleceń ręcznie, zwykle wystarczająco dużo czasu upłynął między zadaniami.</span><span class="sxs-lookup"><span data-stu-id="9432b-133">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="9432b-134">W skrypcie, należy dodać krok w stan uśpienia poleceń (takich jak `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="9432b-134">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="9432b-135">Jeśli zostanie wyświetlony komunikat o błędzie informujący, że podmiot zabezpieczeń nie istnieje w katalogu, ponownie uruchom polecenie.</span><span class="sxs-lookup"><span data-stu-id="9432b-135">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="9432b-136">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="9432b-136">That's it!</span></span> <span data-ttu-id="9432b-137">Twojej aplikacji usługi AD i nazwę główną usługi są skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="9432b-137">Your AD application and service principal are set up.</span></span> <span data-ttu-id="9432b-138">Następnej sekcji przedstawiono sposób Zaloguj się przy użyciu poświadczeń przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9432b-138">The next section shows you how to log in with the credential through Azure CLI.</span></span> <span data-ttu-id="9432b-139">Jeśli chcesz użyć poświadczeń w kodzie aplikacji, nie należy kontynuować w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="9432b-139">If you want to use the credential in your code application, you do not need to continue with this topic.</span></span> <span data-ttu-id="9432b-140">Można przejść do [przykładowe aplikacje](#sample-applications) przykłady logowania się za pomocą identyfikatora aplikacji id oraz hasła.</span><span class="sxs-lookup"><span data-stu-id="9432b-140">You can jump to the [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="9432b-141">Podaj poświadczenia, za pomocą wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9432b-141">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="9432b-142">Teraz musisz zalogować się jako aplikacji w celu wykonania operacji.</span><span class="sxs-lookup"><span data-stu-id="9432b-142">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="9432b-143">Gdy zalogujesz się jako nazwy głównej usługi, należy podać identyfikator dzierżawcy katalogu dla aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="9432b-143">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="9432b-144">Dzierżawa jest wystąpieniem usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9432b-144">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="9432b-145">Aby pobrać identyfikator dzierżawcy, uwierzytelnionym subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="9432b-145">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="9432b-146">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="9432b-146">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="9432b-147">Jeśli konieczne jest uzyskanie identyfikatora dzierżawy innej subskrypcji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9432b-147">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="9432b-148">Można pobrać identyfikatora klienta na potrzeby logowania, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="9432b-148">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="9432b-149">Wartość do użycia na potrzeby rejestrowania jest identyfikatorem guid, na liście głównych nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="9432b-149">The value to use for logging in is the guid listed in the service principal names.</span></span>
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. <span data-ttu-id="9432b-150">Zaloguj się jako nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="9432b-150">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="9432b-151">Zostanie wyświetlony monit o hasło.</span><span class="sxs-lookup"><span data-stu-id="9432b-151">You are prompted for the password.</span></span> <span data-ttu-id="9432b-152">Podaj hasło, które można określić podczas tworzenia aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="9432b-152">Provide the password you specified when creating the AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="9432b-153">Obecnie użytkownik jest uwierzytelniony jako nazwy głównej usługi dla nazwy głównej usługi, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="9432b-153">You are now authenticated as the service principal for the service principal that you created.</span></span>

<span data-ttu-id="9432b-154">Alternatywnie można wywołać operacji REST w wierszu polecenia, aby się zalogować.</span><span class="sxs-lookup"><span data-stu-id="9432b-154">Alternatively, you can invoke REST operations from the command line to log in.</span></span> <span data-ttu-id="9432b-155">Z odpowiedzi uwierzytelniania można pobrać tokenu dostępu do użycia z innych operacji.</span><span class="sxs-lookup"><span data-stu-id="9432b-155">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="9432b-156">Na przykład pobierania tokenu dostępu za pomocą operacji REST, zobacz [generowania tokenu dostępu](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="9432b-156">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="9432b-157">Tworzenie nazwy głównej usługi o certyfikat</span><span class="sxs-lookup"><span data-stu-id="9432b-157">Create service principal with certificate</span></span>
<span data-ttu-id="9432b-158">W tej sekcji możesz wykonać kroki, aby:</span><span class="sxs-lookup"><span data-stu-id="9432b-158">In this section, you perform the steps to:</span></span>

* <span data-ttu-id="9432b-159">Utwórz certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="9432b-159">create a self-signed certificate</span></span>
* <span data-ttu-id="9432b-160">Tworzenie aplikacji usługi AD z certyfikatu i nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="9432b-160">create the AD application with the certificate, and the service principal</span></span>
* <span data-ttu-id="9432b-161">przypisać rolę czytelnika do nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="9432b-161">assign the Reader role to the service principal</span></span>

<span data-ttu-id="9432b-162">Aby wykonać te kroki, musisz mieć [OpenSSL](http://www.openssl.org/) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="9432b-162">To complete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="9432b-163">Tworzenie certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="9432b-163">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="9432b-164">Poprzedni krok utworzyć dwa pliki - privkey.pem i cert.pem.</span><span class="sxs-lookup"><span data-stu-id="9432b-164">The preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="9432b-165">Łączenie klucze publiczne i prywatne w jednym pliku.</span><span class="sxs-lookup"><span data-stu-id="9432b-165">Combine the public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="9432b-166">Otwórz **examplecert.pem** pliku i poszukaj długo sekwencja znaków między **---BEGIN CERTIFICATE---** i **---END CERTIFICATE---**.</span><span class="sxs-lookup"><span data-stu-id="9432b-166">Open the **examplecert.pem** file and look for the long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="9432b-167">Skopiuj dane certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="9432b-167">Copy the certificate data.</span></span> <span data-ttu-id="9432b-168">Te dane należy przekazać jako parametru podczas tworzenia głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="9432b-168">You pass this data as a parameter when creating the service principal.</span></span>

4. <span data-ttu-id="9432b-169">Zaloguj się do swojego konta.</span><span class="sxs-lookup"><span data-stu-id="9432b-169">Sign in to your account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="9432b-170">Aby utworzyć nazwy głównej usługi, należy podać nazwę aplikacji i danych certyfikatu, jak pokazano w poniższym poleceniu:</span><span class="sxs-lookup"><span data-stu-id="9432b-170">To create the service principal, provide the name of the app and the certificate data, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="9432b-171">Zwracany jest nową główną nazwę usługi.</span><span class="sxs-lookup"><span data-stu-id="9432b-171">The new service principal is returned.</span></span> <span data-ttu-id="9432b-172">Identyfikator obiektu jest potrzebna do przyznawania uprawnień.</span><span class="sxs-lookup"><span data-stu-id="9432b-172">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="9432b-173">Identyfikator guid na liście z główne nazwy usług jest potrzebne podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="9432b-173">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="9432b-174">Ten identyfikator guid jest taką samą wartość jak identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9432b-174">This guid is the same value as the app id.</span></span> <span data-ttu-id="9432b-175">W przykładowych aplikacji ta wartość jest określana jako identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="9432b-175">In the sample applications, this value is referred to as the Client ID.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. <span data-ttu-id="9432b-176">Przyznaj uprawnienia głównej usługi w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9432b-176">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="9432b-177">W tym przykładzie należy dodać nazwy głównej usługi do roli Czytelnik, co powoduje przyznanie uprawnień do odczytu wszystkich zasobów w subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9432b-177">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="9432b-178">Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="9432b-178">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="9432b-179">Dla parametru objectid Podaj identyfikator obiektu, który został użyty podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9432b-179">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="9432b-180">Przed uruchomieniem tego polecenia, musisz zezwolić na pewien czas dla nowej nazwy głównej usługi propagację w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9432b-180">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="9432b-181">Po uruchomieniu tych poleceń ręcznie, zwykle wystarczająco dużo czasu upłynął między zadaniami.</span><span class="sxs-lookup"><span data-stu-id="9432b-181">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="9432b-182">W skrypcie, należy dodać krok w stan uśpienia poleceń (takich jak `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="9432b-182">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="9432b-183">Jeśli zostanie wyświetlony komunikat o błędzie informujący, że podmiot zabezpieczeń nie istnieje w katalogu, ponownie uruchom polecenie.</span><span class="sxs-lookup"><span data-stu-id="9432b-183">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="9432b-184">Podaj certyfikat przy użyciu zautomatyzowanego skryptu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9432b-184">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="9432b-185">Teraz musisz zalogować się jako aplikacji w celu wykonania operacji.</span><span class="sxs-lookup"><span data-stu-id="9432b-185">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="9432b-186">Gdy zalogujesz się jako nazwy głównej usługi, należy podać identyfikator dzierżawcy katalogu dla aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="9432b-186">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="9432b-187">Dzierżawa jest wystąpieniem usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9432b-187">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="9432b-188">Aby pobrać identyfikator dzierżawcy, uwierzytelnionym subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="9432b-188">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="9432b-189">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="9432b-189">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="9432b-190">Jeśli konieczne jest uzyskanie identyfikatora dzierżawy innej subskrypcji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9432b-190">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="9432b-191">Aby pobrać odcisk palca certyfikatu i usunąć niepotrzebne znaków, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="9432b-191">To retrieve the certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="9432b-192">Która zwróci wartość odcisku palca są podobne do:</span><span class="sxs-lookup"><span data-stu-id="9432b-192">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="9432b-193">Można pobrać identyfikatora klienta na potrzeby logowania, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="9432b-193">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="9432b-194">Wartość do użycia na potrzeby rejestrowania jest identyfikatorem guid, na liście głównych nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="9432b-194">The value to use for logging in is the guid listed in the service principal names.</span></span>
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. <span data-ttu-id="9432b-195">Zaloguj się jako nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="9432b-195">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="9432b-196">Obecnie użytkownik jest uwierzytelniony jako nazwy głównej usługi dla aplikacji usługi Azure Active Directory, utworzony.</span><span class="sxs-lookup"><span data-stu-id="9432b-196">You are now authenticated as the service principal for the Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="9432b-197">Zmiana poświadczeń</span><span class="sxs-lookup"><span data-stu-id="9432b-197">Change credentials</span></span>

<span data-ttu-id="9432b-198">Aby zmienić poświadczenia dla aplikacji usługi AD, albo z powodu naruszenia zabezpieczeń lub wygaśnięcia poświadczeń, należy użyć `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="9432b-198">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="9432b-199">Aby zmienić hasło, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="9432b-199">To change a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="9432b-200">Aby zmienić wartość certyfikatu, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="9432b-200">To change a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="9432b-201">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="9432b-201">Debug</span></span>

<span data-ttu-id="9432b-202">Podczas tworzenia nazwy głównej usługi, mogą wystąpić następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="9432b-202">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="9432b-203">**"Authentication_Unauthorized"** lub **"subskrypcji nie znaleziono w kontekście".**</span><span class="sxs-lookup"><span data-stu-id="9432b-203">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="9432b-204">— Został wyświetlony ten błąd, gdy Twoje konto nie ma [wymagane uprawnienia](#required-permissions) w usłudze Azure Active Directory w celu rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9432b-204">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="9432b-205">Zwykle zostanie wyświetlony ten błąd, gdy tylko Administrator użytkowników w usłudze Azure Active Directory można zarejestrować aplikacji, a konto użytkownika nie jest administratorem.</span><span class="sxs-lookup"><span data-stu-id="9432b-205">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="9432b-206">Skontaktuj się z administratorem, albo przypisanie do roli administratora lub aby użytkownicy mogli zarejestrować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9432b-206">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="9432b-207">Twoje konto **"nie ma autoryzacji do wykonania akcji"Microsoft.Authorization/roleAssignments/write"w zakresie"/subscriptions/ {guid}"."**  — Zostanie wyświetlony ten błąd, gdy Twoje konto nie ma wystarczających uprawnień, aby przypisać rolę do tożsamości.</span><span class="sxs-lookup"><span data-stu-id="9432b-207">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="9432b-208">Poproś administratora subskrypcji możesz dodać do roli Administrator dostępu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9432b-208">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="9432b-209">Przykładowe aplikacje</span><span class="sxs-lookup"><span data-stu-id="9432b-209">Sample applications</span></span>
<span data-ttu-id="9432b-210">Aby uzyskać informacje o zalogowanie się jako aplikacji za pomocą różnych platform zobacz:</span><span class="sxs-lookup"><span data-stu-id="9432b-210">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="9432b-211">.NET</span><span class="sxs-lookup"><span data-stu-id="9432b-211">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="9432b-212">Java</span><span class="sxs-lookup"><span data-stu-id="9432b-212">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="9432b-213">Node.js</span><span class="sxs-lookup"><span data-stu-id="9432b-213">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="9432b-214">Python</span><span class="sxs-lookup"><span data-stu-id="9432b-214">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="9432b-215">Ruby</span><span class="sxs-lookup"><span data-stu-id="9432b-215">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="9432b-216">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9432b-216">Next steps</span></span>
* <span data-ttu-id="9432b-217">Aby uzyskać szczegółowe instrukcje dotyczące integrowania aplikacji na platformie Azure do zarządzania zasobami, zobacz [przewodnik dewelopera do autoryzacji przy użyciu interfejsu API Menedżera zasobów Azure](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9432b-217">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="9432b-218">Aby uzyskać więcej informacji o używaniu certyfikatów i interfejsu wiersza polecenia Azure, zobacz [uwierzytelniania opartego na certyfikatach z podmiotami zabezpieczeń usługi Azure z wiersza polecenia systemu Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="9432b-218">To get more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="9432b-219">Aby uzyskać listę dostępnych akcji, które można udzielić lub odmówić dla użytkowników, zobacz [operacji dostawcy zasobów usługi Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="9432b-219">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
