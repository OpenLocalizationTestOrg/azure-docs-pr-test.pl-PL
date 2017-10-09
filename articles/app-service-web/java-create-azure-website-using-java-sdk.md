---
title: "aaaCreate aplikacji sieci Web w usłudze Azure App Service przy użyciu hello Azure SDK dla języka Java"
description: "Dowiedz się, jak toocreate aplikacji sieci Web w usłudze Azure App Service, programowo przy użyciu hello Azure SDK dla języka Java."
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a><span data-ttu-id="23347-103">Tworzenie aplikacji sieci Web w usłudze Azure App Service przy użyciu hello Azure SDK dla języka Java</span><span class="sxs-lookup"><span data-stu-id="23347-103">Create a Web App in Azure App Service using hello Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a><span data-ttu-id="23347-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="23347-104">Overview</span></span>
<span data-ttu-id="23347-105">W tym przewodniku przedstawiono sposób toocreate zestawu Azure SDK dla aplikacji Java, która tworzy aplikację sieci Web w [usłudze Azure App Service][Azure App Service], następnie wdrożyć tooit aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23347-105">This walkthrough shows you how toocreate an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application tooit.</span></span> <span data-ttu-id="23347-106">Składa się z dwóch części:</span><span class="sxs-lookup"><span data-stu-id="23347-106">It consists of two parts:</span></span>

* <span data-ttu-id="23347-107">Część 1 pokazuje, jak toobuild aplikacji Java tworzącą aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="23347-107">Part 1 demonstrates how toobuild a Java application that creates a web app.</span></span>
* <span data-ttu-id="23347-108">Część 2 przedstawiono sposób toocreate proste JSP "Hello World" aplikacji, a następnie użyj FTP klienta toodeploy kodu tooApp usługi.</span><span class="sxs-lookup"><span data-stu-id="23347-108">Part 2 demonstrates how toocreate a simple JSP "Hello World" application, then use an FTP client toodeploy code tooApp Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23347-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="23347-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="23347-110">Instalacje oprogramowania</span><span class="sxs-lookup"><span data-stu-id="23347-110">Software Installations</span></span>
<span data-ttu-id="23347-111">Hello AzureWebDemo kod aplikacji, w tym artykule został napisany za pomocą usługi Azure zestawu Java SDK 0.7.0, które można zainstalować przy użyciu hello [Instalatora platformy sieci Web] [ Web Platform Installer] (WebPI).</span><span class="sxs-lookup"><span data-stu-id="23347-111">hello AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using hello [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="23347-112">Ponadto należy upewnić się, że najnowszej wersji hello toouse hello [zestawu narzędzi platformy Azure dla programu Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="23347-112">In addition, make sure toouse hello latest version of hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="23347-113">Po zainstalowaniu hello zestawu SDK, należy zaktualizować hello zależności w projekcie Eclipse, uruchamiając **zaktualizować indeksu** w **repozytoria Maven**, potem ponownie Dodaj hello najnowsza wersja każdego pakietu w hello  **Zależności** okna.</span><span class="sxs-lookup"><span data-stu-id="23347-113">After you install hello SDK, update hello dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add hello latest version of each package in hello **Dependencies** window.</span></span> <span data-ttu-id="23347-114">Sprawdź hello wersji zainstalowanego oprogramowania w środowisku Eclipse, klikając **Pomoc > szczegółowe informacje dotyczące instalacji**; powinien mieć co najmniej hello następujące wersje:</span><span class="sxs-lookup"><span data-stu-id="23347-114">You can verify hello version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least hello following versions:</span></span>

* <span data-ttu-id="23347-115">Pakiet dla biblioteki Microsoft Azure dla języka Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="23347-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="23347-116">Środowisko Eclipse IDE for Java EE Developers 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="23347-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="23347-117">Tworzenie i konfigurowanie zasobów w chmurze na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="23347-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="23347-118">Przed rozpoczęciem tej procedury należy toohave aktywną subskrypcją platformy Azure i skonfigurować domyślne Active Directory (AD) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="23347-118">Before you begin this procedure, you need toohave an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="23347-119">Tworzenie usługi Active Directory (AD) na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="23347-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="23347-120">W przypadku usługi Active Directory (AD) nie jest już ma w Twojej subskrypcji platformy Azure, zaloguj się do hello [klasycznego portalu Azure] [ Azure classic portal] z kontem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="23347-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into hello [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="23347-121">Jeśli masz wiele subskrypcji, kliknij przycisk **subskrypcje** i wybierz hello domyślnym katalogiem dla subskrypcji hello ma toouse dla tego projektu.</span><span class="sxs-lookup"><span data-stu-id="23347-121">If you have multiple subscriptions, click **Subscriptions** and select hello default directory for hello subscription you want toouse for this project.</span></span> <span data-ttu-id="23347-122">Następnie kliknij przycisk **Zastosuj** Widok subskrypcji toothat tooswitch.</span><span class="sxs-lookup"><span data-stu-id="23347-122">Then click **Apply** tooswitch toothat subscription view.</span></span>

1. <span data-ttu-id="23347-123">Wybierz **usługi Active Directory** hello menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="23347-123">Select **Active Directory** from hello menu at left.</span></span> <span data-ttu-id="23347-124">**Kliknij przycisk Nowy > katalogu > Utwórz niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="23347-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="23347-125">W **Dodaj katalog**, wybierz pozycję **Utwórz nowy katalog**.</span><span class="sxs-lookup"><span data-stu-id="23347-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="23347-126">W **nazwa**, wprowadź nazwę katalogu.</span><span class="sxs-lookup"><span data-stu-id="23347-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="23347-127">W **domeny**, wprowadź nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="23347-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="23347-128">Jest to nazwy domeny podstawowe jest włączone domyślnie z katalogu; ma ona formularza hello `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="23347-128">This is a basic domain name that is included by default with your directory; it has hello form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="23347-129">Można określić nazwę na podstawie nazwy katalogu hello lub innego własnej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="23347-129">You can name it based on hello directory name or another domain name that you own.</span></span> <span data-ttu-id="23347-130">Później możesz dodać Twoja organizacja już korzysta z inną nazwą domeny.</span><span class="sxs-lookup"><span data-stu-id="23347-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="23347-131">W **kraj lub region**, wybierz ustawienia regionalne.</span><span class="sxs-lookup"><span data-stu-id="23347-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="23347-132">Aby uzyskać więcej informacji dotyczących usługi AD, zobacz [co to jest katalog usługi Azure AD][What is an Azure AD directory]?</span><span class="sxs-lookup"><span data-stu-id="23347-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="23347-133">Utwórz certyfikat zarządzania platformy Azure</span><span class="sxs-lookup"><span data-stu-id="23347-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="23347-134">Hello Azure SDK dla języka Java używa zarządzania certyfikatami tooauthenticate z subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="23347-134">hello Azure SDK for Java uses management certificates tooauthenticate with Azure subscriptions.</span></span> <span data-ttu-id="23347-135">Są to certyfikaty X.509 v3, że używasz tooauthenticate aplikacji klienckiej, która używa hello interfejs API zarządzania usługami tooact imieniu hello subskrypcji właściciela toomanage subskrypcji zasobów.</span><span class="sxs-lookup"><span data-stu-id="23347-135">These are X.509 v3 certificates you use tooauthenticate a client application that uses hello Service Management API tooact on behalf of hello subscription owner toomanage subscription resources.</span></span>

<span data-ttu-id="23347-136">Kod Hello w tej procedurze używa tooauthenticate certyfikatu z podpisem własnym z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="23347-136">hello code in this procedure uses a self-signed certificate tooauthenticate with Azure.</span></span> <span data-ttu-id="23347-137">Dla tej procedury należy toocreate certyfikatu i przekaż go toohello [klasycznego portalu Azure] [ Azure classic portal] wcześniej.</span><span class="sxs-lookup"><span data-stu-id="23347-137">For this procedure, you need toocreate a certificate and upload it toohello [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="23347-138">Obejmuje to hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="23347-138">This involves hello following steps:</span></span>

* <span data-ttu-id="23347-139">Generowanie pliku PFX reprezentujący Twój certyfikat klienta i zapisz ją lokalnie.</span><span class="sxs-lookup"><span data-stu-id="23347-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="23347-140">Wygeneruj certyfikat zarządzania (plik CER) z pliku PFX hello.</span><span class="sxs-lookup"><span data-stu-id="23347-140">Generate a management certificate (CER file) from hello PFX file.</span></span>
* <span data-ttu-id="23347-141">Przekaż tooyour pliku CER hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="23347-141">Upload hello CER file tooyour Azure subscription.</span></span>
* <span data-ttu-id="23347-142">Konwertowanie pliku PFX hello JKS, ponieważ Java używa tego tooauthenticate format za pomocą certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="23347-142">Convert hello PFX file into JKS, because Java uses that format tooauthenticate using certificates.</span></span>
* <span data-ttu-id="23347-143">Napisać kod uwierzytelniania aplikacji hello, która odwołuje się lokalnego pliku JKS toohello.</span><span class="sxs-lookup"><span data-stu-id="23347-143">Write hello application's authentication code, which refers toohello local JKS file.</span></span>

<span data-ttu-id="23347-144">Po zakończeniu tej procedury hello CER certyfikatu będzie znajdować się w ramach subskrypcji platformy Azure i hello JKS certyfikatu będzie znajdować się na dysku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="23347-144">When you complete this procedure, hello CER certificate will reside in your Azure subscription and hello JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="23347-145">Aby uzyskać więcej informacji o certyfikatach zarządzania, zobacz [tworzenie i przekazywanie certyfikatu zarządzania platformy Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="23347-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="23347-146">Tworzenie certyfikatu</span><span class="sxs-lookup"><span data-stu-id="23347-146">Create a certificate</span></span>
<span data-ttu-id="23347-147">toocreate własny certyfikat z podpisem własnym, otwórz konsolę polecenia w systemie operacyjnym i uruchom następujące polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="23347-147">toocreate your own self-signed certificate, open a command console on your operating system and run hello following commands.</span></span>

> <span data-ttu-id="23347-148">**Uwaga:** hello komputera, na którym uruchomiono to polecenie musi mieć hello JDK zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="23347-148">**Note:**  hello computer on which you run this command must have hello JDK installed.</span></span> <span data-ttu-id="23347-149">Ponadto hello ścieżki toohello keytool zależy od hello lokalizacji, w którym chcesz zainstalować hello JDK.</span><span class="sxs-lookup"><span data-stu-id="23347-149">Also, hello path toohello keytool depends on hello location in which you install hello JDK.</span></span> <span data-ttu-id="23347-150">Aby uzyskać więcej informacji, zobacz [klucza i certyfikat zarządzania narzędzia (Narzędzie klucza)] [ Key and Certificate Management Tool (keytool)] w hello dokumentów online dotyczących Java.</span><span class="sxs-lookup"><span data-stu-id="23347-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in hello Java online docs.</span></span>
> 
> 

<span data-ttu-id="23347-151">plik PFX hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="23347-151">toocreate hello .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="23347-152">plik .cer hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="23347-152">toocreate hello .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="23347-153">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="23347-153">where:</span></span>

* <span data-ttu-id="23347-154">`<java-install-dir>`jest hello ścieżka toohello katalog, w którym zainstalowano Java.</span><span class="sxs-lookup"><span data-stu-id="23347-154">`<java-install-dir>` is hello path toohello directory in which you installed Java.</span></span>
* <span data-ttu-id="23347-155">`<keystore-id>`Identyfikator wpisu magazynu kluczy hello jest (na przykład `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="23347-155">`<keystore-id>` is hello keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="23347-156">`<cert-store-dir>`jest hello ścieżka toohello katalog, w którym mają certyfikaty toostore (na przykład `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="23347-156">`<cert-store-dir>` is hello path toohello directory in which you want toostore certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="23347-157">`<cert-file-name>`jest nazwą hello hello pliku certyfikatu (na przykład `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="23347-157">`<cert-file-name>` is hello name of hello certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="23347-158">`<password>`to hasło hello wybrania certyfikatu hello tooprotect; musi być co najmniej 6 znaków.</span><span class="sxs-lookup"><span data-stu-id="23347-158">`<password>` is hello password you choose tooprotect hello certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="23347-159">Hasło nie można wprowadzić, chociaż nie jest to zalecane.</span><span class="sxs-lookup"><span data-stu-id="23347-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="23347-160">`<dname>`jest skojarzony z aliasem toobe nazwy wyróżniającej x 500 hello i jest używany jako Witaj wystawca i pola podmiot certyfikatu z podpisem własnym hello.</span><span class="sxs-lookup"><span data-stu-id="23347-160">`<dname>` is hello X.500 Distinguished Name toobe associated with alias, and is used as hello issuer and subject fields in hello self-signed certificate.</span></span>

<span data-ttu-id="23347-161">Aby uzyskać więcej informacji, zobacz [tworzenie i przekazywanie certyfikatu zarządzania platformy Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="23347-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-hello-certificate"></a><span data-ttu-id="23347-162">Przekaż certyfikat hello</span><span class="sxs-lookup"><span data-stu-id="23347-162">Upload hello certificate</span></span>
<span data-ttu-id="23347-163">tooupload tooAzure certyfikatu z podpisem własnym, przejdź toohello **ustawienia** strony w portalu klasycznym hello, a następnie kliknij przycisk hello **certyfikaty zarządzania** kartę. Kliknij przycisk **przekazać** u dołu hello hello strony i przejdź toohello lokalizację pliku CER hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="23347-163">tooupload a self-signed certificate tooAzure, go toohello **Settings** page in hello classic portal, then click hello **Management Certificates** tab. Click **Upload** at hello bottom of hello page and navigate toohello location of hello CER file you created.</span></span>

#### <a name="convert-hello-pfx-file-into-jks"></a><span data-ttu-id="23347-164">Konwertowanie pliku PFX hello JKS</span><span class="sxs-lookup"><span data-stu-id="23347-164">Convert hello PFX file into JKS</span></span>
<span data-ttu-id="23347-165">Hello wiersza polecenia systemu Windows (uruchomionego jako administrator), dysk cd toohello katalog zawierający hello certyfikatów i uruchamiania hello następujące polecenie, gdzie `<java-install-dir>` jest katalogiem hello zainstalowane Java na komputerze:</span><span class="sxs-lookup"><span data-stu-id="23347-165">In hello Windows Command Prompt (running as admin), cd toohello directory containing hello certificates and run hello following command, where `<java-install-dir>` is hello directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="23347-166">Po wyświetleniu monitu wprowadź hasło magazynu kluczy docelowej hello; są to hasło hello hello JKS pliku.</span><span class="sxs-lookup"><span data-stu-id="23347-166">When prompted, enter hello destination keystore password; this will be hello password for hello JKS file.</span></span>
2. <span data-ttu-id="23347-167">Po wyświetleniu monitu wprowadź hasło keystore źródła hello; to hasło hello hello pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="23347-167">When prompted, enter hello source keystore password; this is hello password you specified for hello PFX file.</span></span>

<span data-ttu-id="23347-168">dwa hasła Hello nie mają toobe hello takie same.</span><span class="sxs-lookup"><span data-stu-id="23347-168">hello two passwords do not have toobe hello same.</span></span> <span data-ttu-id="23347-169">Hasło nie można wprowadzić, chociaż nie jest to zalecane.</span><span class="sxs-lookup"><span data-stu-id="23347-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="23347-170">Tworzenie aplikacji do tworzenia aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="23347-170">Build a Web App creation application</span></span>
### <a name="create-hello-eclipse-workspace-and-maven-project"></a><span data-ttu-id="23347-171">Utwórz hello Eclipse obszaru roboczego i projekt Maven</span><span class="sxs-lookup"><span data-stu-id="23347-171">Create hello Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="23347-172">W tej sekcji utworzysz obszaru roboczego i projekt Maven hello aplikacji sieci web aplikacji tworzenia o nazwie AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="23347-172">In this section you create a workspace and a Maven project for hello web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="23347-173">Utwórz nowy projekt Maven.</span><span class="sxs-lookup"><span data-stu-id="23347-173">Create a new Maven project.</span></span> <span data-ttu-id="23347-174">Kliknij przycisk **Plik > Nowy > Projekt Maven**.</span><span class="sxs-lookup"><span data-stu-id="23347-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="23347-175">W **nowy projekt Maven**, wybierz pozycję **Tworzenie prostego projektu** i **Użyj domyślnej lokalizacji obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="23347-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="23347-176">Na drugiej stronie powitania z **nowy projekt Maven**, określ następujące hello:</span><span class="sxs-lookup"><span data-stu-id="23347-176">On hello second page of **New Maven Project**, specify hello following:</span></span>
   
   * <span data-ttu-id="23347-177">Identyfikator grupy:`com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="23347-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="23347-178">Identyfikator artefaktu: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="23347-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="23347-179">Wersja: 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="23347-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="23347-180">Pakowanie: jar</span><span class="sxs-lookup"><span data-stu-id="23347-180">Packaging: jar</span></span>
   * <span data-ttu-id="23347-181">Nazwa: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="23347-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="23347-182">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="23347-182">Click **Finish**.</span></span>
3. <span data-ttu-id="23347-183">Otwórz plik pom.xml hello nowy projekt w Eksploratorze projektu.</span><span class="sxs-lookup"><span data-stu-id="23347-183">Open hello new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="23347-184">Wybierz hello **zależności** kartę. Jak jest to nowy projekt, wymieniono jeszcze żadnych pakietów.</span><span class="sxs-lookup"><span data-stu-id="23347-184">Select hello **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="23347-185">Wyświetl Otwórz hello Maven repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="23347-185">Open hello Maven Repositories view.</span></span> <span data-ttu-id="23347-186">**Kliknij przycisk okna > Pokaż widok > Inne > Maven > repozytoria Maven** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="23347-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="23347-187">Witaj **repozytoria Maven** widok będzie wyświetlany u dołu hello hello IDE.</span><span class="sxs-lookup"><span data-stu-id="23347-187">hello **Maven Repositories** view will appear at hello bottom of hello IDE.</span></span>
5. <span data-ttu-id="23347-188">Otwórz **globalne repozytoria**, powitania kliknij prawym przyciskiem myszy **centralnej** repozytorium, a następnie wybierz **Rebuild Index**.</span><span class="sxs-lookup"><span data-stu-id="23347-188">Open **Global Repositories**, right-click hello **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="23347-189">Ten krok może potrwać kilka minut w zależności od prędkości hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="23347-189">This step can take several minutes depending on hello speed of your connection.</span></span> <span data-ttu-id="23347-190">Podczas odtwarza hello indeksu, powinny być widoczne hello pakietów Microsoft Azure w hello **centralnej** Maven repozytorium.</span><span class="sxs-lookup"><span data-stu-id="23347-190">When hello index rebuilds, you should see hello Microsoft Azure packages in hello **central** Maven repository.</span></span>
6. <span data-ttu-id="23347-191">W **zależności**, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="23347-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="23347-192">W **wprowadź identyfikator grupy...**  wprowadź `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="23347-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="23347-193">Wybierz pakiety hello bmc i zarządzania aplikacjami sieci Web usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="23347-193">Select hello packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="23347-194">**Uwaga:** Jeśli aktualizujesz zależności powitania po wydaniu nowej wersji, należy toore — Dodaj wszystkie zależności hello na tej liście.</span><span class="sxs-lookup"><span data-stu-id="23347-194">**Note:** If you are updating hello dependencies after a new version release, you need toore-add each of hello dependencies in this list.</span></span>
   > <span data-ttu-id="23347-195">Po kliknięciu **Dodaj** i wybierz poszczególne zależności, prawdopodobnie z hello nowego numeru wersji w hello **zależności** listy.</span><span class="sxs-lookup"><span data-stu-id="23347-195">After you click **Add** and select each dependency, it appears with hello new version number in hello **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="23347-196">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="23347-196">Click **OK**.</span></span> <span data-ttu-id="23347-197">Witaj pakietów platformy Azure, a następnie wyświetlane w hello **zależności** listy.</span><span class="sxs-lookup"><span data-stu-id="23347-197">hello Azure packages then appear in hello **Dependencies** list.</span></span>

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a><span data-ttu-id="23347-198">Pisanie kodu języka Java tooCreate aplikacji sieci Web przy hello wywoływania zestawu Azure SDK</span><span class="sxs-lookup"><span data-stu-id="23347-198">Writing Java Code tooCreate a Web App by Calling hello Azure SDK</span></span>
<span data-ttu-id="23347-199">Następnie należy napisać kod hello, który wywołuje interfejsy API w hello Azure SDK dla języka Java toocreate hello aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23347-199">Next, write hello code that calls APIs in hello Azure SDK for Java toocreate hello App Service web app.</span></span>

1. <span data-ttu-id="23347-200">Tworzenie Java klasy toocontain hello główny wpis punktu kodu.</span><span class="sxs-lookup"><span data-stu-id="23347-200">Create a Java class toocontain hello main entry point code.</span></span> <span data-ttu-id="23347-201">W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **nowy > klasy**.</span><span class="sxs-lookup"><span data-stu-id="23347-201">In Project Explorer, right-click on hello project node and select **New > Class**.</span></span>
2. <span data-ttu-id="23347-202">W **Nowa Klasa Java**, nazwa klasy hello `WebCreator` i sprawdź hello **publiczne statyczne void main** wyboru.</span><span class="sxs-lookup"><span data-stu-id="23347-202">In **New Java Class**, name hello class `WebCreator` and check hello **public static void main** checkbox.</span></span> <span data-ttu-id="23347-203">Opcje Hello powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="23347-203">hello selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="23347-204">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="23347-204">Click **Finish**.</span></span> <span data-ttu-id="23347-205">Plik WebCreator.java Hello jest widoczny w Eksploratorze projektu.</span><span class="sxs-lookup"><span data-stu-id="23347-205">hello WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a><span data-ttu-id="23347-206">Wywoływanie tooCreate interfejsu API Azure hello aplikację usługi aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="23347-206">Calling hello Azure API tooCreate an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="23347-207">Dodaj niezbędne importów</span><span class="sxs-lookup"><span data-stu-id="23347-207">Add necessary imports</span></span>
<span data-ttu-id="23347-208">W WebCreator.java Dodaj powitania po importów; Importy te zawierają tooclasses dostępu w hello biblioteki zarządzania służący do konsumowania interfejsów API usługi Azure:</span><span class="sxs-lookup"><span data-stu-id="23347-208">In WebCreator.java, add hello following imports; these imports provide access tooclasses in hello management libraries for consuming Azure APIs:</span></span>

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-hello-main-entry-point-class"></a><span data-ttu-id="23347-209">Zdefiniuj hello główny wpis punktu klasy</span><span class="sxs-lookup"><span data-stu-id="23347-209">Define hello main entry point class</span></span>
<span data-ttu-id="23347-210">Ponieważ hello hello aplikacji AzureWebDemo służy toocreate aplikację usługi sieci Web aplikacji, nazwy klasy głównym hello dla tej aplikacji `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="23347-210">Because hello purpose of hello AzureWebDemo application is toocreate an App Service Web App, name hello main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="23347-211">Ta klasa udostępnia hello główny wpis punktu kod, który wywołuje aplikacji hello toocreate hello interfejs API zarządzania usługami Azure w sieci web.</span><span class="sxs-lookup"><span data-stu-id="23347-211">This class provides hello main entry point code that calls hello Azure Service Management API toocreate hello web app.</span></span>

<span data-ttu-id="23347-212">Dodaj następujące definicje parametr przestrzeni sieci Web i aplikacji sieci web hello hello.</span><span class="sxs-lookup"><span data-stu-id="23347-212">Add hello following parameter definitions for hello web app and webspace.</span></span> <span data-ttu-id="23347-213">Konieczne będzie tooprovide własnych informacji identyfikator i certyfikatu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="23347-213">You will need tooprovide your own Azure subscription ID and certificate information.</span></span>

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

<span data-ttu-id="23347-214">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="23347-214">where:</span></span>

* <span data-ttu-id="23347-215">`<subscription-id>`jest identyfikator subskrypcji platformy Azure hello, w której ma zostać toocreate hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="23347-215">`<subscription-id>` is hello Azure subscription ID in which you want toocreate hello resource.</span></span>
* <span data-ttu-id="23347-216">`<certificate-store-path>`jest hello ścieżkę i nazwę pliku toohello JKS plik w katalogu magazynu lokalnego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="23347-216">`<certificate-store-path>` is hello path and filename toohello JKS file in your local certificate store directory.</span></span> <span data-ttu-id="23347-217">Na przykład `C:/Certificates/CertificateName.jks` dla systemu Linux i `C:\Certificates\CertificateName.jks` dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="23347-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="23347-218">`<certificate-password>`jest hello hasło podczas tworzenia certyfikatu JKS.</span><span class="sxs-lookup"><span data-stu-id="23347-218">`<certificate-password>` is hello password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="23347-219">`webAppName`może być dowolna nazwa, którą wybierzesz; Ta procedura używa nazwy hello `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="23347-219">`webAppName` can be any name you choose; this procedure uses hello name `WebDemoWebApp`.</span></span> <span data-ttu-id="23347-220">Witaj Pełna nazwa domeny jest hello `webAppName` z hello `domainName` dołączone, w tym przypadku pełną domenę hello jest `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="23347-220">hello full domain name is hello `webAppName` with hello `domainName` appended, so in this case hello full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="23347-221">`domainName`należy określić, jak pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="23347-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="23347-222">`webSpaceName`musi mieć jedną z wartości hello zdefiniowanych w hello [WebSpaceNames] [ WebSpaceNames] klasy.</span><span class="sxs-lookup"><span data-stu-id="23347-222">`webSpaceName` should be one of hello values defined in hello [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="23347-223">`appServicePlanName`należy określić, jak pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="23347-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="23347-224">**Uwaga:** zawsze uruchomić tę aplikację, konieczne wartość hello toochange `webAppName` i `appServicePlanName` (lub usunąć aplikacji sieci web hello na powitania Azure Portal) przed uruchomieniem aplikacji hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="23347-224">**Note:** Each time you run this application, you need toochange hello value of `webAppName` and `appServicePlanName` (or delete hello web app on hello Azure Portal) before running hello application again.</span></span> <span data-ttu-id="23347-225">W przeciwnym razie wykonanie zakończy się niepowodzeniem, ponieważ hello sam zasób już istnieje na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="23347-225">Otherwise, execution will fail because hello same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-hello-web-creation-method"></a><span data-ttu-id="23347-226">Zdefiniuj metodę tworzenia hello sieci web</span><span class="sxs-lookup"><span data-stu-id="23347-226">Define hello web creation method</span></span>
<span data-ttu-id="23347-227">Następnie określ aplikację sieci web hello toocreate metody.</span><span class="sxs-lookup"><span data-stu-id="23347-227">Next, define a method toocreate hello web app.</span></span> <span data-ttu-id="23347-228">Ta metoda `createWebApp`, określa parametry hello hello aplikacji sieci web i hello przestrzeni sieci Web.</span><span class="sxs-lookup"><span data-stu-id="23347-228">This method, `createWebApp`, specifies hello parameters of hello web app and hello webspace.</span></span> <span data-ttu-id="23347-229">Również tworzy i konfiguruje hello aplikacji usługi sieci Web aplikacji zarządzania klienta, który jest zdefiniowany przez hello [WebSiteManagementClient] [ WebSiteManagementClient] obiektu.</span><span class="sxs-lookup"><span data-stu-id="23347-229">It also creates and configures hello App Service Web Apps management client, which is defined by hello [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="23347-230">Klient zarządzania Hello jest klucza toocreating aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="23347-230">hello management client is key toocreating Web Apps.</span></span> <span data-ttu-id="23347-231">Zapewnia usługi sieci web RESTful, które pozwalają aplikacji sieci web (wykonywanie operacji, takich jak tworzenie, update i delete) toomanage aplikacji przez wywołanie interfejsu API zarządzania usługami hello.</span><span class="sxs-lookup"><span data-stu-id="23347-231">It provides RESTful web services that allow applications toomanage web apps (performing operations such as create, update, and delete) by calling hello service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="23347-232">Kod Hello dane wyjściowe obejmują hello stanu HTTP odpowiedzi hello oznaczający powodzenie lub niepowodzenie, a jeśli to się powiedzie, dane wyjściowe obejmują nazwę hello hello utworzono aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="23347-232">hello code will output hello HTTP status of hello response indicating success or failure, and if successful, will output hello name of hello created web app.</span></span>

#### <a name="define-hello-main-method"></a><span data-ttu-id="23347-233">Zdefiniuj metodę main() hello</span><span class="sxs-lookup"><span data-stu-id="23347-233">Define hello main() method</span></span>
<span data-ttu-id="23347-234">Podaj kod metody main() hello tej aplikacji sieci web wywołania createWebApp() toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="23347-234">Provide hello main() method code that calls createWebApp() toocreate hello web app.</span></span>

<span data-ttu-id="23347-235">Na koniec wywołania `createWebApp` z `main`:</span><span class="sxs-lookup"><span data-stu-id="23347-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a><span data-ttu-id="23347-236">Uruchamianie aplikacji hello i sprawdź tworzenie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="23347-236">Run hello application and verify web app creation</span></span>
<span data-ttu-id="23347-237">tooverify działającą aplikację, kliknij przycisk **Uruchom > Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="23347-237">tooverify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="23347-238">Po zakończeniu działania aplikacji hello powinny być widoczne następujące dane wyjściowe w konsoli programu Eclipse hello hello:</span><span class="sxs-lookup"><span data-stu-id="23347-238">When hello application completes running, you should see hello following output in hello Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="23347-239">Zaloguj się do klasycznego portalu Azure hello i kliknij przycisk **aplikacje sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="23347-239">Log into hello Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="23347-240">Hello nowej aplikacji sieci web powinna zostać wyświetlona na liście aplikacji sieci Web hello w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="23347-240">hello new web app should appear in hello Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-toohello-web-app"></a><span data-ttu-id="23347-241">Wdrażanie aplikacji toohello aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="23347-241">Deploying an Application toohello Web App</span></span>
<span data-ttu-id="23347-242">Po uruchomiono AzureWebDemo i utworzyć hello nowej aplikacji sieci web, zaloguj się do klasycznego portalu hello kliknij **aplikacje sieci Web**i wybierz **WebDemoWebApp** w hello **aplikacje sieci Web** listy.</span><span class="sxs-lookup"><span data-stu-id="23347-242">After you have run AzureWebDemo and created hello new web app, log into hello classic portal, click **Web Apps**, and select **WebDemoWebApp** in hello **Web Apps** list.</span></span> <span data-ttu-id="23347-243">Na stronie pulpitu nawigacyjnego aplikacji sieci web powitania kliknij **Przeglądaj** (lub kliknij adres URL hello, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span><span class="sxs-lookup"><span data-stu-id="23347-243">In hello web app's dashboard page, click **Browse** (or click hello URL, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span></span> <span data-ttu-id="23347-244">Zostanie wyświetlona strona pusty symbol zastępczy, ponieważ żadna zawartość jeszcze został toohello opublikowanej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="23347-244">You will see a blank placeholder page, because no content has been published toohello web app yet.</span></span>

<span data-ttu-id="23347-245">Następnie utworzysz aplikację "Hello World" i wdrożyć aplikację sieci web toohello.</span><span class="sxs-lookup"><span data-stu-id="23347-245">Next you will create a "Hello World" application and deploy it toohello web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="23347-246">Utwórz aplikację JSP Hello World</span><span class="sxs-lookup"><span data-stu-id="23347-246">Create a JSP Hello World application</span></span>
#### <a name="create-hello-application"></a><span data-ttu-id="23347-247">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="23347-247">Create hello application</span></span>
<span data-ttu-id="23347-248">W kolejności toodemonstrate jak toodeploy sieci web toohello aplikacji hello procedury przedstawiono toocreate prostą aplikację "Hello World" w języku Java i przekaż go toohello aplikację usługi sieci Web aplikacji utworzony w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23347-248">In order toodemonstrate how toodeploy an application toohello web, hello following procedure shows you how toocreate a simple "Hello World" Java application and upload it toohello App Service Web App that your application created.</span></span>

1. <span data-ttu-id="23347-249">Kliknij przycisk **Plik > Nowy > Projekt sieci Web dynamiczne**.</span><span class="sxs-lookup"><span data-stu-id="23347-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="23347-250">Nadaj jej nazwę `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="23347-250">Name it `JSPHello`.</span></span> <span data-ttu-id="23347-251">Nie trzeba toochange inne ustawienia, w tym oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="23347-251">You do not need toochange any other settings in this dialog.</span></span> <span data-ttu-id="23347-252">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="23347-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="23347-253">W obszarze Eksplorator projektów rozwiń hello **JSPHello** projektu, kliknij prawym przyciskiem myszy **WebContent**, następnie kliknij przycisk **nowy > pliku JSP**.</span><span class="sxs-lookup"><span data-stu-id="23347-253">In Project Explorer, expand hello **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="23347-254">W oknie dialogowym Nowy plik JSP hello hello nowego pliku o nazwie `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="23347-254">In hello New JSP File dialog, name hello new file `index.jsp`.</span></span> <span data-ttu-id="23347-255">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="23347-255">Click **Next**.</span></span>
3. <span data-ttu-id="23347-256">W hello **wybierz szablon JSP** zaznacz pozycję **New JSP File (html)** i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="23347-256">In hello **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="23347-257">W index.jsp, Dodaj hello następującego kodu w hello `<head>` i `<body>` tagu sekcje:</span><span class="sxs-lookup"><span data-stu-id="23347-257">In index.jsp, add hello following code in hello `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a><span data-ttu-id="23347-258">Uruchamianie aplikacji Hello World hello w localhost</span><span class="sxs-lookup"><span data-stu-id="23347-258">Run hello Hello World application in localhost</span></span>
<span data-ttu-id="23347-259">Aby uruchomić tę aplikację, musisz tooconfigure kilka właściwości.</span><span class="sxs-lookup"><span data-stu-id="23347-259">Before you run this application, you need tooconfigure a few properties.</span></span>

1. <span data-ttu-id="23347-260">Kliknij prawym przyciskiem myszy hello **JSPHello** projekt i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="23347-260">Right-click hello **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="23347-261">W hello **właściwości** okna dialogowego: Wybierz **ścieżka kompilacji języka Java**, wybierz pozycję hello **kolejność i eksportowanie** karcie wyboru **biblioteka systemu środowiska JRE**, następnie kliknij przycisk **Się** toomove on toohello u góry listy hello.</span><span class="sxs-lookup"><span data-stu-id="23347-261">In hello **Properties** dialog: select **Java Build Path**, select hello **Order and Export** tab, check **JRE System Library**, then click **Up** toomove it toohello top of hello list.</span></span>
   
    ![][4]
3. <span data-ttu-id="23347-262">Również w hello **właściwości** okna dialogowego: Wybierz **docelowe środowiska uruchomieniowe** i kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="23347-262">Also in hello **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="23347-263">W hello **nowe środowisko uruchomieniowe serwera** okno dialogowe, wybierz serwer, takich jak **Apache Tomcat v7.0** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="23347-263">In hello **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="23347-264">W hello **serwera Tomcat** okno dialogowe, zestaw **nazwa** za`Apache Tomcat v7.0`i ustaw **katalog instalacyjny serwera Tomcat** toohello katalogu, w którym zainstalowano wersję hello Serwer Tomcat ma toouse.</span><span class="sxs-lookup"><span data-stu-id="23347-264">In hello **Tomcat Server** dialog, set **Name** too`Apache Tomcat v7.0`, and set **Tomcat Installation Directory** toohello directory in which you installed hello version of Tomcat server you want toouse.</span></span>
   
    ![][5]
   
    <span data-ttu-id="23347-265">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="23347-265">Click **Finish**.</span></span>
5. <span data-ttu-id="23347-266">Następnie wróć toohello **docelowe środowiska uruchomieniowe** strony hello **właściwości** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="23347-266">You then return toohello **Targeted Runtimes** page of hello **Properties** dialog.</span></span> <span data-ttu-id="23347-267">Wybierz **Apache Tomcat v7.0**, następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="23347-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="23347-268">W hello Eclipse **Uruchom** menu, kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="23347-268">In hello Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="23347-269">W hello **Uruchom jako** okno dialogowe, wybierz opcję **Uruchom na serwerze**.</span><span class="sxs-lookup"><span data-stu-id="23347-269">In hello **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="23347-270">W hello **Uruchom na serwerze** okno dialogowe, wybierz opcję **Tomcat v7.0 Server**:</span><span class="sxs-lookup"><span data-stu-id="23347-270">In hello **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="23347-271">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="23347-271">Click **Finish**.</span></span>
7. <span data-ttu-id="23347-272">Gdy hello jest uruchamiana aplikacja, powinny pojawić się hello **JSPHello** strony są wyświetlane w oknie localhost w środowisku Eclipse (`http://localhost:8080/JSPHello/`), wyświetlania hello następujący komunikat:</span><span class="sxs-lookup"><span data-stu-id="23347-272">When hello application runs, you should see hello **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying hello following message:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a><span data-ttu-id="23347-273">Eksportowanie aplikacji hello jako plik WAR</span><span class="sxs-lookup"><span data-stu-id="23347-273">Export hello application as a WAR</span></span>
<span data-ttu-id="23347-274">Pliki projektu sieci web hello należy wyeksportować w postaci pliku archiwum (plik WAR) sieci web, dzięki czemu można wdrożyć aplikację sieci web toohello.</span><span class="sxs-lookup"><span data-stu-id="23347-274">Export hello web project files as a web archive (WAR) file so that you can deploy it toohello web app.</span></span> <span data-ttu-id="23347-275">Witaj następujące pliki projektu sieci web znajdują się w folderze WebContent hello:</span><span class="sxs-lookup"><span data-stu-id="23347-275">hello following web project files reside in hello WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="23347-276">Kliknij prawym przyciskiem myszy hello WebContent folder i wybierz **wyeksportować**.</span><span class="sxs-lookup"><span data-stu-id="23347-276">Right-click hello WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="23347-277">W hello **eksportu wybierz** okna dialogowego, kliknij przycisk **sieci Web > WAR** pliku, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="23347-277">In hello **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="23347-278">W hello **wyeksportować plik WAR** okno dialogowe, wybierz katalog src hello w bieżącym projekcie hello i zawierać nazwę pliku WAR hello na końcu hello hello.</span><span class="sxs-lookup"><span data-stu-id="23347-278">In hello **WAR Export** dialog, select hello src directory in hello current project, and include hello name of hello WAR file at hello end.</span></span> <span data-ttu-id="23347-279">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="23347-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="23347-280">Aby uzyskać więcej informacji na temat wdrażania WAR plików, zobacz [dodać tooAzure aplikacji Java aplikacji usługi sieci Web aplikacji](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="23347-280">For more information on deploying WAR files, see [Add a Java application tooAzure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-hello-hello-world-application-using-ftp"></a><span data-ttu-id="23347-281">Wdrażanie FTP przy użyciu aplikacji Hello World hello</span><span class="sxs-lookup"><span data-stu-id="23347-281">Deploying hello Hello World Application Using FTP</span></span>
<span data-ttu-id="23347-282">Wybierz aplikację hello toopublish klienta FTP innych firm.</span><span class="sxs-lookup"><span data-stu-id="23347-282">Select a third-party FTP client toopublish hello application.</span></span> <span data-ttu-id="23347-283">W tej procedurze opisano dwie opcje: hello Kudu konsoli wbudowanych w środowisku Azure. i FileZilla, narzędzie popularnych o wygodny graficznego interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="23347-283">This procedure describes two options: hello Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="23347-284">**Uwaga:** hello Azure zestawu narzędzi Eclipse obsługuje konta toostorage wdrożenia i chmury usługi, ale nie obsługuje obecnie wdrożenia tooweb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23347-284">**Note:** hello Azure Toolkit for Eclipse supports deployment toostorage accounts and cloud services, but does not currently support deployment tooweb apps.</span></span> <span data-ttu-id="23347-285">Można wdrożyć toostorage konta i w chmurze usługi przy użyciu projektu wdrożenia platformy Azure, zgodnie z opisem w [tworzenia aplikacji Hello World na platformie Azure w programie Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), ale nie tooweb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23347-285">You can deploy toostorage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not tooweb apps.</span></span> <span data-ttu-id="23347-286">Użyj innych metod, takich jak FTP lub GitHub tootransfer plików tooyour aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="23347-286">Use other methods such as FTP or GitHub tootransfer files tooyour web app.</span></span>
> 
> <span data-ttu-id="23347-287">**Uwaga:** nie zaleca się używania protokołu FTP w wierszu polecenia systemu Windows hello (hello narzędzia wiersza polecenia FTP.EXE dostarczanych z systemem Windows).</span><span class="sxs-lookup"><span data-stu-id="23347-287">**Note:** We do not recommend using FTP from hello Windows command prompt (hello command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="23347-288">Klienci FTP, używający active FTP, takich jak FTP.EXE, często nie toowork za pośrednictwem zapór.</span><span class="sxs-lookup"><span data-stu-id="23347-288">FTP clients that use active FTP, such as FTP.EXE, often fail toowork over firewalls.</span></span> <span data-ttu-id="23347-289">Active FTP określa wewnętrzny adres sieci LAN, serwer toowhich FTP prawdopodobnie nie powiedzie się tooconnect.</span><span class="sxs-lookup"><span data-stu-id="23347-289">Active FTP specifies an internal LAN-based address, toowhich an FTP server will likely fail tooconnect.</span></span>
> 
> 

<span data-ttu-id="23347-290">Aby uzyskać więcej informacji dotyczących wdrażania tooan aplikacji usługi sieci web app przy użyciu protokołu FTP Zobacz hello następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="23347-290">For more information on deployment tooan App Service web app using FTP, see hello following topics:</span></span>

* [<span data-ttu-id="23347-291">Wdrażanie przy użyciu narzędzia FTP</span><span class="sxs-lookup"><span data-stu-id="23347-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="23347-292">Konfigurowanie poświadczeń wdrożenia</span><span class="sxs-lookup"><span data-stu-id="23347-292">Set up deployment credentials</span></span>
<span data-ttu-id="23347-293">Upewnij się, że zostało uruchomione hello **AzureWebDemo** toocreate aplikacji w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="23347-293">Make sure you have run hello **AzureWebDemo** application toocreate a web app.</span></span> <span data-ttu-id="23347-294">Przenieś pliki toothis lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="23347-294">You will transfer files toothis location.</span></span>

1. <span data-ttu-id="23347-295">Zaloguj się do klasycznego portalu hello i kliknij przycisk **aplikacje sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="23347-295">Log into hello classic portal and click **Web Apps**.</span></span> <span data-ttu-id="23347-296">Upewnij się, że **WebDemoWebApp** jest widoczna na liście hello aplikacji sieci web i upewnij się, że jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="23347-296">Make sure **WebDemoWebApp** appears in hello list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="23347-297">Kliknij przycisk **WebDemoWebApp** tooopen jej **pulpitu nawigacyjnego** strony.</span><span class="sxs-lookup"><span data-stu-id="23347-297">Click **WebDemoWebApp** tooopen its **Dashboard** page.</span></span>
2. <span data-ttu-id="23347-298">Na powitania **pulpitu nawigacyjnego** w obszarze **szybki przegląd**, kliknij przycisk **skonfigurować poświadczenia wdrażania** (Jeśli masz już poświadczenia wdrażania, odczytuje  **Resetowanie poświadczeń wdrażania**).</span><span class="sxs-lookup"><span data-stu-id="23347-298">On hello **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="23347-299">Wdrożenie poświadczenia są skojarzone z kontem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="23347-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="23347-300">Należy toospecify nazwę użytkownika i hasło, których można używać toodeploy przy użyciu usługi Git i FTP.</span><span class="sxs-lookup"><span data-stu-id="23347-300">You need toospecify a username and password that you can use toodeploy using Git and FTP.</span></span> <span data-ttu-id="23347-301">Można użyć tych aplikacji sieci web tooany toodeploy poświadczenia w ramach wszystkich subskrypcji platformy Azure skojarzonych z Twoim kontem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="23347-301">You can use these credentials toodeploy tooany web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="23347-302">Podaj w dialogowym hello i rekordów hello nazwy użytkownika i hasła usługi Git i FTP poświadczenia wdrożenia do użycia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="23347-302">Provide Git and FTP deployment credentials in hello dialog, and record hello username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="23347-303">Uzyskiwanie informacji o połączeniu FTP</span><span class="sxs-lookup"><span data-stu-id="23347-303">Get FTP connection information</span></span>
<span data-ttu-id="23347-304">toouse FTP toodeploy aplikacji pliki toohello nowo utworzona aplikacja sieci web, należy tooobtain informacje o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="23347-304">toouse FTP toodeploy application files toohello newly created web app, you need tooobtain connection information.</span></span> <span data-ttu-id="23347-305">Istnieją dwa sposoby tooobtain informacje o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="23347-305">There are two ways tooobtain connection information.</span></span> <span data-ttu-id="23347-306">Jednym ze sposobów jest toovisit hello aplikacji sieci web firmy **pulpitu nawigacyjnego** strony; hello inny sposób jest profil publikowania aplikacji toodownload hello sieci web.</span><span class="sxs-lookup"><span data-stu-id="23347-306">One way is toovisit hello web app's **Dashboard** page; hello other way is toodownload hello web app's publish profile.</span></span> <span data-ttu-id="23347-307">profil publikowania Hello jest plik XML, który zawiera informacje, takie jak hosta FTP poświadczenia nazwy i logowania dla aplikacji sieci web w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="23347-307">hello publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="23347-308">W ramach wszystkich subskrypcji skojarzonych z hello konto platformy Azure, nie tylko ten jeden, można użyć tej nazwy użytkownika i hasła toodeploy tooany aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="23347-308">You can use this username and password toodeploy tooany web app in all subscriptions associated with hello Azure account, not only this one.</span></span>

<span data-ttu-id="23347-309">informacje o połączeniu tooobtain FTP w bloku aplikacja sieci web hello w hello [Azure Portal][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="23347-309">tooobtain FTP connection information from hello web app's blade in hello [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="23347-310">W obszarze **Essentials**, znaleźć i skopiować hello **nazwa hosta FTP**.</span><span class="sxs-lookup"><span data-stu-id="23347-310">Under **Essentials**, find and copy hello **FTP hostname**.</span></span> <span data-ttu-id="23347-311">To jest identyfikator URI podobne zbyt`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="23347-311">This is a URI similar too`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="23347-312">W obszarze **Essentials**, należy znaleźć i skopiować **nazwy użytkownika serwera FTP/wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="23347-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="23347-313">Będzie to mieć formularza hello *webappname\deployment-username*, na przykład `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="23347-313">This will have hello form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="23347-314">profil publikowania informacji o połączeniu FTP tooobtain z hello:</span><span class="sxs-lookup"><span data-stu-id="23347-314">tooobtain FTP connection information from hello publish profile:</span></span>

1. <span data-ttu-id="23347-315">W bloku aplikacja sieci web powitania kliknij **profilu publikowania Get**.</span><span class="sxs-lookup"><span data-stu-id="23347-315">In hello web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="23347-316">To spowoduje pobranie .publishsettings pliku tooyour dysk lokalny.</span><span class="sxs-lookup"><span data-stu-id="23347-316">This will download a .publishsettings file tooyour local drive.</span></span>
2. <span data-ttu-id="23347-317">Otwórz plik .publishsettings hello w edytorze XML lub edytorze tekstów i Znajdź hello `<publishProfile>` zawierający element `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="23347-317">Open hello .publishsettings file in an XML editor or text editor and find hello `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="23347-318">Go powinna wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="23347-318">It should look like hello following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="23347-319">Należy pamiętać, że hello aplikacji sieci web `publishProfile` ustawienia mapowania toohello FileZilla lokacji Menedżera ustawień w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="23347-319">Note that hello web app's `publishProfile` settings map toohello FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="23347-320">`publishUrl`jest identyczny hello **nazwa hosta FTP**, hello wartość ustawiona w **hosta**.</span><span class="sxs-lookup"><span data-stu-id="23347-320">`publishUrl` is hello same as **FTP host name**, hello value you set in **Host**.</span></span>
* <span data-ttu-id="23347-321">`publishMethod="FTP"`oznacza, że ustawisz **protokołu** za**FTP - File Transfer Protocol**, i **szyfrowania** za**za pomocą zwykłego FTP**.</span><span class="sxs-lookup"><span data-stu-id="23347-321">`publishMethod="FTP"` means that you set **Protocol** too**FTP - File Transfer Protocol**, and **Encryption** too**Use plain FTP**.</span></span>
* <span data-ttu-id="23347-322">`userName`i `userPWD` są klucze hello rzeczywiste wartości nazwy użytkownika i hasła określonego podczas resetowania hello poświadczenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="23347-322">`userName` and `userPWD` are keys for hello actual username and password values you specified when you reset hello deployment credentials.</span></span> <span data-ttu-id="23347-323">`userName`jest identyczny hello **wdrożenia / FTP użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="23347-323">`userName` is hello same as **Deployment / FTP user**.</span></span> <span data-ttu-id="23347-324">Mapują zbyt**użytkownika** i **hasło** w FileZilla.</span><span class="sxs-lookup"><span data-stu-id="23347-324">They map too**User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="23347-325">`ftpPassiveMode="True"`oznacza to, że korzysta z tej witryny hello FTP pasywnym transferu FTP; Wybierz **pasywnym** na powitania **ustawienia transferu** kartę.</span><span class="sxs-lookup"><span data-stu-id="23347-325">`ftpPassiveMode="True"` means that hello FTP site uses passive FTP transfer; select **Passive** on hello **Transfer Settings** tab.</span></span>

#### <a name="configure-hello-web-app-toohost-a-java-application"></a><span data-ttu-id="23347-326">Skonfiguruj hello toohost aplikacji sieci Web aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="23347-326">Configure hello Web App toohost a Java application</span></span>
<span data-ttu-id="23347-327">Przed opublikowaniem aplikacji hello należy toochange kilka ustawień konfiguracji, aby hello aplikacji sieci web mogą obsługiwać aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="23347-327">Before you publish hello application, you need toochange a few configuration settings so that hello web app can host a Java application.</span></span>

1. <span data-ttu-id="23347-328">W klasycznym portalu hello, przejdź do pozycji aplikacji sieci web toohello **pulpitu nawigacyjnego** i kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="23347-328">In hello classic portal, go toohello web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="23347-329">Na powitania **Konfiguruj** Określ hello następujące ustawienia.</span><span class="sxs-lookup"><span data-stu-id="23347-329">On hello **Configure** page, specify hello following settings.</span></span>
2. <span data-ttu-id="23347-330">W **wersję Java** hello domyślna to **poza**; wybierz wersję Java hello celów aplikacji, na przykład 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="23347-330">In **Java version** hello default is **Off**; select hello Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="23347-331">Po wykonaniu tej czynności również upewnij się, że **kontener sieci Web** ustawiono tooa wersję serwera Tomcat.</span><span class="sxs-lookup"><span data-stu-id="23347-331">After you do this, also make sure that **Web container** is set tooa version of Tomcat Server.</span></span>
3. <span data-ttu-id="23347-332">W **dokumenty domyślne**, Dodaj index.jsp i przesunięty toohello u góry listy hello.</span><span class="sxs-lookup"><span data-stu-id="23347-332">In **Default Documents**, add index.jsp and move it up toohello top of hello list.</span></span> <span data-ttu-id="23347-333">(hello domyślnego pliku dla aplikacji sieci web jest hostingstart.html).</span><span class="sxs-lookup"><span data-stu-id="23347-333">(hello default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="23347-334">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="23347-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="23347-335">Publikowanie aplikacji przy użyciu Kudu</span><span class="sxs-lookup"><span data-stu-id="23347-335">Publish your application using Kudu</span></span>
<span data-ttu-id="23347-336">Jednym ze sposobów toopublish aplikacji hello jest hello toouse Kudu debug console wbudowanych w platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="23347-336">One way toopublish hello application is toouse hello Kudu debug console built into Azure.</span></span> <span data-ttu-id="23347-337">Program kudu jest znany toobe stabilny i spójny z aplikacji sieci Web usługi aplikacji i serwer Tomcat.</span><span class="sxs-lookup"><span data-stu-id="23347-337">Kudu is known toobe stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="23347-338">Dostęp hello konsoli dla aplikacji sieci web hello przechodząc tooa adres URL hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="23347-338">You access hello console for hello web app by browsing tooa URL of hello following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="23347-339">Do wykonania tej procedury hello Kudu konsoli znajduje się pod adresem hello następującego adresu URL; Przeglądaj toothis lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="23347-339">For this procedure, hello Kudu console is located at hello following URL; browse toothis location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="23347-340">Wybierz z górnego menu hello **konsoli debugowania > CMD**.</span><span class="sxs-lookup"><span data-stu-id="23347-340">From hello top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="23347-341">W wierszu polecenia konsoli hello, przejdź zbyt`/site/wwwroot` (lub kliknij przycisk `site`, następnie `wwwroot` w widoku katalogu hello u góry strony hello hello):</span><span class="sxs-lookup"><span data-stu-id="23347-341">In hello console command line, navigate too`/site/wwwroot` (or click `site`, then `wwwroot` in hello directory view at hello top of hello page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="23347-342">Po określeniu **wersję Java**, serwer Tomcat należy utworzyć katalogu webapps.</span><span class="sxs-lookup"><span data-stu-id="23347-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="23347-343">W wierszu polecenia konsoli hello Przejdź katalogu webapps toohello:</span><span class="sxs-lookup"><span data-stu-id="23347-343">In hello console command line, navigate toohello webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="23347-344">Przeciągnij JSPHello.war z `<project-path>/JSPHello/src/` i upuść go w widoku katalogu Kudu hello w `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="23347-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into hello Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="23347-345">Nie przeciągnij go toohello obszaru "Przeciągnij tutaj tooupload i zip", ponieważ Tomcat będzie Rozpakuj go.</span><span class="sxs-lookup"><span data-stu-id="23347-345">Do not drag it toohello "Drag here tooupload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="23347-346">W pierwszym JSPHello.war pojawia się w obszarze katalogu hello samodzielnie:</span><span class="sxs-lookup"><span data-stu-id="23347-346">At first JSPHello.war appears in hello directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="23347-347">W krótkim czasie (prawdopodobnie mniej niż 5 minut) serwer Tomcat będzie Rozpakuj plik WAR hello w rozpakowanym katalogu JSPHello.</span><span class="sxs-lookup"><span data-stu-id="23347-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip hello WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="23347-348">Kliknij przycisk toosee katalogu głównego hello czy index.jsp zostało rozpakowane i skopiować.</span><span class="sxs-lookup"><span data-stu-id="23347-348">Click hello ROOT directory toosee whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="23347-349">Jeśli tak, przejdź wstecz toohello webapps katalogu toosee czy hello rozpakowane JSPHello katalog został utworzony.</span><span class="sxs-lookup"><span data-stu-id="23347-349">If so, navigate back toohello webapps directory toosee whether hello unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="23347-350">Jeśli te elementy nie jest widoczny, poczekaj i powtórz.</span><span class="sxs-lookup"><span data-stu-id="23347-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="23347-351">Publikowanie aplikacji przy użyciu FileZilla (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="23347-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="23347-352">Kolejnym narzędziem za pomocą aplikacji hello toopublish jest FileZilla, popularnych klient FTP innych firm z wygodny graficznego interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="23347-352">Another tool you can use toopublish hello application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="23347-353">Można pobrać i zainstalować FileZilla z [http://filezilla-project.org/](http://filezilla-project.org/) Jeśli użytkownik nie ma jeszcze go.</span><span class="sxs-lookup"><span data-stu-id="23347-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="23347-354">Aby uzyskać więcej informacji na temat używania powitania klienta, zobacz hello [dokumentacji FileZilla](https://wiki.filezilla-project.org/Documentation) i ten wpis w blogu na [klienci FTP — część 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="23347-354">For more information on using hello client, see hello [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="23347-355">W FileZilla, kliknij przycisk **Plik > Menedżer lokacji**.</span><span class="sxs-lookup"><span data-stu-id="23347-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="23347-356">W hello **Menedżer lokacji** okna dialogowego, kliknij przycisk **nowej lokacji**.</span><span class="sxs-lookup"><span data-stu-id="23347-356">In hello **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="23347-357">Nowa, pusta witryna FTP będą wyświetlane w **wybierz wpis** monitem tooprovide nazwę.</span><span class="sxs-lookup"><span data-stu-id="23347-357">A new blank FTP site will appear in **Select Entry** prompting you tooprovide a name.</span></span> <span data-ttu-id="23347-358">Do wykonania tej procedury, nadaj mu nazwę `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="23347-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="23347-359">Na powitania **ogólne** karcie, określ hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="23347-359">On hello **General** tab, specify hello following settings:</span></span>
   
   * <span data-ttu-id="23347-360">**Host:** Enter hello **nazwa hosta FTP** skopiowany z hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="23347-360">**Host:** Enter hello **FTP Host Name** that you copied from hello dashboard.</span></span>
   * <span data-ttu-id="23347-361">**Port:** (to pole pozostanie puste, to jest pasywny przeniesienia i powitania serwera określają hello portu toouse.)</span><span class="sxs-lookup"><span data-stu-id="23347-361">**Port:** (Leave this blank, as this is a passive transfer and hello server will determine hello port toouse.)</span></span>
   * <span data-ttu-id="23347-362">**Protokół:** protokół transferu plików FTP</span><span class="sxs-lookup"><span data-stu-id="23347-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="23347-363">**Szyfrowanie:** za pomocą zwykłego FTP</span><span class="sxs-lookup"><span data-stu-id="23347-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="23347-364">**Typ logowania:** normalny</span><span class="sxs-lookup"><span data-stu-id="23347-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="23347-365">**Użytkownik:** hello Enter wdrożenia / FTP użytkownika, który został skopiowany z hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="23347-365">**User:** Enter hello Deployment / FTP user that you copied from hello dashboard.</span></span> <span data-ttu-id="23347-366">Jest to pełna username FTP hello, mającej formularza hello *webappname\username*.</span><span class="sxs-lookup"><span data-stu-id="23347-366">This is hello full FTP username, which has hello form *webappname\username*.</span></span>
   * <span data-ttu-id="23347-367">**Hasło:** wprowadź hasło hello określony podczas ustawiania poświadczeń wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="23347-367">**Password:** Enter hello password that you specified when you set hello deployment credentials.</span></span>
     
     <span data-ttu-id="23347-368">Na powitania **ustawienia transferu** wybierz opcję **pasywnym**.</span><span class="sxs-lookup"><span data-stu-id="23347-368">On hello **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="23347-369">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="23347-369">Click **Connect**.</span></span> <span data-ttu-id="23347-370">Jeśli powodzenia FileZilla na konsoli zostanie wyświetlony `Status: Connected` komunikat i problem `LIST` polecenia zawartość katalogu hello toolist.</span><span class="sxs-lookup"><span data-stu-id="23347-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command toolist hello directory contents.</span></span>
4. <span data-ttu-id="23347-371">W hello **lokalnego** panelu lokacji hello wybierz katalog źródłowy w plik JSPHello.war hello, który znajduje się; ścieżka hello będzie podobne toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="23347-371">In hello **Local** site panel, select hello source directory in which hello JSPHello.war file resides; hello path will be similar toohello following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="23347-372">W hello **zdalnego** panelu lokacji, hello wybierz folder docelowy.</span><span class="sxs-lookup"><span data-stu-id="23347-372">In hello **Remote** site panel, select hello destination folder.</span></span> <span data-ttu-id="23347-373">Zostanie wdrożona toohello pliku WAR hello `webapps` katalog główny aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="23347-373">You will deploy hello WAR file toohello `webapps` directory under hello web app's root.</span></span> <span data-ttu-id="23347-374">Przejdź za`/site/wwwroot`, kliknij prawym przyciskiem myszy `wwwroot`i wybierz **Utwórz katalog**.</span><span class="sxs-lookup"><span data-stu-id="23347-374">Navigate too`/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="23347-375">Nazwa katalogu hello `webapps` , a następnie wprowadź tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="23347-375">Name hello directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="23347-376">Transfer JSPHello.war zbyt`/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="23347-376">Transfer JSPHello.war too`/site/wwwroot/webapps`.</span></span> <span data-ttu-id="23347-377">Wybierz JSPHello.war hello **lokalnego** listy plików, kliknij prawym przyciskiem myszy na nim i wybierz **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="23347-377">Select JSPHello.war in hello **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="23347-378">Powinny pojawić się ją na `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="23347-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="23347-379">Po skopiowaniu katalogu webapps toohello JSPHello.war serwera Tomcat zostanie automatycznie Rozpakuj (Rozpakuj) hello plików w pliku WAR hello.</span><span class="sxs-lookup"><span data-stu-id="23347-379">After you copy JSPHello.war toohello webapps directory, Tomcat Server will automatically unpack (unzip) hello files in hello WAR file.</span></span> <span data-ttu-id="23347-380">Mimo że serwer Tomcat rozpoczyna się rozpakowanie niemal natychmiast, może trwać bardzo długo czas prawdopodobnie dla tooappear plików powitania klienta hello FTP.</span><span class="sxs-lookup"><span data-stu-id="23347-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for hello files tooappear in hello FTP client.</span></span>

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a><span data-ttu-id="23347-381">Uruchamianie aplikacji Hello World hello na powitania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="23347-381">Run hello Hello World application on hello Web App</span></span>
1. <span data-ttu-id="23347-382">Po przekazany plik WAR hello i zweryfikować, że serwer Tomcat utworzył rozpakowanego `JSPHello` katalogu, Przeglądaj zbyt`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23347-382">After you have uploaded hello WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse too`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello application.</span></span>
   
   > <span data-ttu-id="23347-383">**Uwaga:** kliknięcie **Przeglądaj** z hello klasyczny portal może spowodować, że hello domyślnej strony sieci Web, informujący o tym "tej aplikacji sieci web Java na podstawie został pomyślnie utworzony."</span><span class="sxs-lookup"><span data-stu-id="23347-383">**Note:** If you click **Browse** from hello classic portal, you might get hello default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="23347-384">W danych wyjściowych aplikacji hello tooview kolejności zamiast hello domyślnej strony sieci Web może być toorefresh hello strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="23347-384">You might have toorefresh hello webpage in order tooview hello application output instead of hello default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="23347-385">Po uruchomieniu aplikacji hello powinna zostać wyświetlona strona sieci web z hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="23347-385">When hello application runs, you should see a web page with hello following output:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="23347-386">Oczyszczanie zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="23347-386">Clean up Azure resources</span></span>
<span data-ttu-id="23347-387">Ta procedura powoduje utworzenie aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23347-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="23347-388">Opłaty będą naliczane dla zasobu hello tak długo, jak istnieje.</span><span class="sxs-lookup"><span data-stu-id="23347-388">You will be billed for hello resource as long as it exists.</span></span> <span data-ttu-id="23347-389">Jeśli nie planujesz toocontinue przy użyciu hello aplikacji sieci web do testowania lub programowanie należy rozważyć zatrzymanie lub usunięcie go.</span><span class="sxs-lookup"><span data-stu-id="23347-389">Unless you plan toocontinue using hello web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="23347-390">Aplikacja sieci web, który został zatrzymany nadal spowoduje naliczenie opłaty mały, ale w dowolnym momencie można uruchomić go ponownie.</span><span class="sxs-lookup"><span data-stu-id="23347-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="23347-391">Usunięcie aplikacji sieci web spowoduje usunięcie wszystkich danych, które zostały przekazane tooit.</span><span class="sxs-lookup"><span data-stu-id="23347-391">Deleting a web app erases all data you have uploaded tooit.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
