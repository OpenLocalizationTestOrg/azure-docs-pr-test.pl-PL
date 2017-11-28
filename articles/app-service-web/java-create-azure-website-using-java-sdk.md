---
title: "Tworzenie aplikacji sieci Web w usłudze Azure App Service przy użyciu zestawu Azure SDK dla języka Java"
description: "Dowiedz się, jak utworzyć aplikację sieci Web w usłudze Azure App Service, programowo przy użyciu zestawu Azure SDK dla języka Java."
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
ms.openlocfilehash: 08bb53de8cf437a5a2b1c3b38bce9f81b8349493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-the-azure-sdk-for-java"></a><span data-ttu-id="cc9f0-103">Tworzenie aplikacji sieci Web w usłudze Azure App Service przy użyciu zestawu Azure SDK dla języka Java</span><span class="sxs-lookup"><span data-stu-id="cc9f0-103">Create a Web App in Azure App Service using the Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on the Azure Portal -->

## <a name="overview"></a><span data-ttu-id="cc9f0-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="cc9f0-104">Overview</span></span>
<span data-ttu-id="cc9f0-105">W tym przewodniku przedstawiono sposób tworzenia zestawu Azure SDK dla aplikacji Java, która tworzy aplikację sieci Web w [usłudze Azure App Service][Azure App Service], następnie wdrożyć aplikację do niego.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-105">This walkthrough shows you how to create an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application to it.</span></span> <span data-ttu-id="cc9f0-106">Składa się z dwóch części:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-106">It consists of two parts:</span></span>

* <span data-ttu-id="cc9f0-107">Część 1 demonstruje sposób tworzenia aplikacji Java, która tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-107">Part 1 demonstrates how to build a Java application that creates a web app.</span></span>
* <span data-ttu-id="cc9f0-108">Część 2 przedstawia sposób tworzenia prostego JSP "Hello World" aplikacji, a następnie użyj FTP klienta można wdrożyć kod w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-108">Part 2 demonstrates how to create a simple JSP "Hello World" application, then use an FTP client to deploy code to App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc9f0-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cc9f0-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="cc9f0-110">Instalacje oprogramowania</span><span class="sxs-lookup"><span data-stu-id="cc9f0-110">Software Installations</span></span>
<span data-ttu-id="cc9f0-111">AzureWebDemo kod aplikacji w tym artykule został napisany za pomocą usługi Azure zestawu Java SDK 0.7.0, które można zainstalować przy użyciu [Instalatora platformy sieci Web] [ Web Platform Installer] (WebPI).</span><span class="sxs-lookup"><span data-stu-id="cc9f0-111">The AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using the [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="cc9f0-112">Ponadto upewnij się używać najnowszej wersji [zestawu narzędzi platformy Azure dla programu Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="cc9f0-112">In addition, make sure to use the latest version of the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="cc9f0-113">Po zainstalowaniu zestawu SDK, należy zaktualizować zależności w projekcie Eclipse, uruchamiając **zaktualizować indeksu** w **repozytoria Maven**, potem ponownie Dodaj najnowsza wersja każdego pakietu w  **Zależności** okna.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-113">After you install the SDK, update the dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add the latest version of each package in the **Dependencies** window.</span></span> <span data-ttu-id="cc9f0-114">Można sprawdzić wersji zainstalowanego oprogramowania w środowisku Eclipse, klikając **Pomoc > szczegółowe informacje dotyczące instalacji**; wymaga co najmniej następujące wersje:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-114">You can verify the version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least the following versions:</span></span>

* <span data-ttu-id="cc9f0-115">Pakiet dla biblioteki Microsoft Azure dla języka Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="cc9f0-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="cc9f0-116">Środowisko Eclipse IDE for Java EE Developers 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="cc9f0-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="cc9f0-117">Tworzenie i konfigurowanie zasobów w chmurze na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="cc9f0-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="cc9f0-118">Przed rozpoczęciem tej procedury, musisz mieć subskrypcję usługi Azure active i ustawić domyślne Active Directory (AD) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-118">Before you begin this procedure, you need to have an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="cc9f0-119">Tworzenie usługi Active Directory (AD) na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="cc9f0-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="cc9f0-120">W przypadku usługi Active Directory (AD) nie jest już ma w Twojej subskrypcji platformy Azure, zaloguj się do [klasycznego portalu Azure] [ Azure classic portal] z kontem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into the [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="cc9f0-121">Jeśli masz wiele subskrypcji, kliknij przycisk **subskrypcje** i wybierz domyślny katalog dla subskrypcji, którego chcesz użyć dla tego projektu.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-121">If you have multiple subscriptions, click **Subscriptions** and select the default directory for the subscription you want to use for this project.</span></span> <span data-ttu-id="cc9f0-122">Następnie kliknij przycisk **Zastosuj** Aby przełączyć się do tego widoku subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-122">Then click **Apply** to switch to that subscription view.</span></span>

1. <span data-ttu-id="cc9f0-123">Wybierz **usługi Active Directory** z menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-123">Select **Active Directory** from the menu at left.</span></span> <span data-ttu-id="cc9f0-124">**Kliknij przycisk Nowy > katalogu > Utwórz niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="cc9f0-125">W **Dodaj katalog**, wybierz pozycję **Utwórz nowy katalog**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="cc9f0-126">W **nazwa**, wprowadź nazwę katalogu.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="cc9f0-127">W **domeny**, wprowadź nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="cc9f0-128">Jest to nazwy domeny podstawowe jest włączone domyślnie z katalogu; ma on postać `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-128">This is a basic domain name that is included by default with your directory; it has the form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="cc9f0-129">Można określić nazwę na podstawie nazwy katalogu lub innego własnej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-129">You can name it based on the directory name or another domain name that you own.</span></span> <span data-ttu-id="cc9f0-130">Później możesz dodać Twoja organizacja już korzysta z inną nazwą domeny.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="cc9f0-131">W **kraj lub region**, wybierz ustawienia regionalne.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="cc9f0-132">Aby uzyskać więcej informacji dotyczących usługi AD, zobacz [co to jest katalog usługi Azure AD][What is an Azure AD directory]?</span><span class="sxs-lookup"><span data-stu-id="cc9f0-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="cc9f0-133">Utwórz certyfikat zarządzania platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cc9f0-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="cc9f0-134">Zestaw Azure SDK for Java korzysta z certyfikatów zarządzania do uwierzytelniania za pomocą subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-134">The Azure SDK for Java uses management certificates to authenticate with Azure subscriptions.</span></span> <span data-ttu-id="cc9f0-135">Są to certyfikaty X.509 v3, który używany do uwierzytelniania aplikacji klienckiej, która wykorzystuje interfejs API zarządzania usługami działać w imieniu właściciela subskrypcji do zarządzania zasobami subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-135">These are X.509 v3 certificates you use to authenticate a client application that uses the Service Management API to act on behalf of the subscription owner to manage subscription resources.</span></span>

<span data-ttu-id="cc9f0-136">Kod w tej procedurze używa certyfikatu z podpisem własnym do uwierzytelniania w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-136">The code in this procedure uses a self-signed certificate to authenticate with Azure.</span></span> <span data-ttu-id="cc9f0-137">Do wykonania tej procedury, należy utworzyć certyfikat i przekaż go do [klasycznego portalu Azure] [ Azure classic portal] wcześniej.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-137">For this procedure, you need to create a certificate and upload it to the [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="cc9f0-138">Obejmuje to następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-138">This involves the following steps:</span></span>

* <span data-ttu-id="cc9f0-139">Generowanie pliku PFX reprezentujący Twój certyfikat klienta i zapisz ją lokalnie.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="cc9f0-140">Wygeneruj certyfikat zarządzania (plik CER) z pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-140">Generate a management certificate (CER file) from the PFX file.</span></span>
* <span data-ttu-id="cc9f0-141">Przekaż plik CER do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-141">Upload the CER file to your Azure subscription.</span></span>
* <span data-ttu-id="cc9f0-142">Konwertowanie pliku PFX JKS, ponieważ Java użyje tego formatu do uwierzytelniania za pomocą certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-142">Convert the PFX file into JKS, because Java uses that format to authenticate using certificates.</span></span>
* <span data-ttu-id="cc9f0-143">Napisać kod uwierzytelniania aplikacji, która odwołuje się do pliku lokalnego JKS.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-143">Write the application's authentication code, which refers to the local JKS file.</span></span>

<span data-ttu-id="cc9f0-144">Po zakończeniu tej procedury, certyfikat CER będą znajdować się w Twojej subskrypcji platformy Azure i certyfikat JKS będą znajdować się na lokalnym dysku.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-144">When you complete this procedure, the CER certificate will reside in your Azure subscription and the JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="cc9f0-145">Aby uzyskać więcej informacji o certyfikatach zarządzania, zobacz [tworzenie i przekazywanie certyfikatu zarządzania platformy Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="cc9f0-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="cc9f0-146">Tworzenie certyfikatu</span><span class="sxs-lookup"><span data-stu-id="cc9f0-146">Create a certificate</span></span>
<span data-ttu-id="cc9f0-147">Aby utworzyć własny certyfikat z podpisem własnym, otwórz konsolę polecenia w systemie operacyjnym i uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-147">To create your own self-signed certificate, open a command console on your operating system and run the following commands.</span></span>

> <span data-ttu-id="cc9f0-148">**Uwaga:** komputera, na którym uruchomiono polecenie muszą mieć zainstalowany zestaw JDK.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-148">**Note:**  The computer on which you run this command must have the JDK installed.</span></span> <span data-ttu-id="cc9f0-149">Ponadto ścieżka do keytool zależy od lokalizacji, w którym chcesz zainstalować zestaw JDK.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-149">Also, the path to the keytool depends on the location in which you install the JDK.</span></span> <span data-ttu-id="cc9f0-150">Aby uzyskać więcej informacji, zobacz [klucza i certyfikat zarządzania narzędzia (Narzędzie klucza)] [ Key and Certificate Management Tool (keytool)] w dokumentów online Java.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in the Java online docs.</span></span>
> 
> 

<span data-ttu-id="cc9f0-151">Aby utworzyć plik PFX:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-151">To create the .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="cc9f0-152">Aby utworzyć plik .cer:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-152">To create the .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="cc9f0-153">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-153">where:</span></span>

* <span data-ttu-id="cc9f0-154">`<java-install-dir>`to ścieżka do katalogu, w którym zainstalowano Java.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-154">`<java-install-dir>` is the path to the directory in which you installed Java.</span></span>
* <span data-ttu-id="cc9f0-155">`<keystore-id>`jest to identyfikator wpisu magazynu kluczy (na przykład `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="cc9f0-155">`<keystore-id>` is the keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="cc9f0-156">`<cert-store-dir>`jest to ścieżka do katalogu, w którym mają być przechowywane certyfikaty (na przykład `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="cc9f0-156">`<cert-store-dir>` is the path to the directory in which you want to store certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="cc9f0-157">`<cert-file-name>`to nazwa pliku certyfikatu (na przykład `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="cc9f0-157">`<cert-file-name>` is the name of the certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="cc9f0-158">`<password>`to hasło, które chcesz chronić certyfikat; musi być co najmniej 6 znaków.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-158">`<password>` is the password you choose to protect the certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="cc9f0-159">Hasło nie można wprowadzić, chociaż nie jest to zalecane.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="cc9f0-160">`<dname>`to nazwa wyróżniająca X.500 ma zostać skojarzony z aliasem i jest używany jako pola wystawcy i podmiotu certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-160">`<dname>` is the X.500 Distinguished Name to be associated with alias, and is used as the issuer and subject fields in the self-signed certificate.</span></span>

<span data-ttu-id="cc9f0-161">Aby uzyskać więcej informacji, zobacz [tworzenie i przekazywanie certyfikatu zarządzania platformy Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="cc9f0-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-the-certificate"></a><span data-ttu-id="cc9f0-162">Przekaż certyfikat</span><span class="sxs-lookup"><span data-stu-id="cc9f0-162">Upload the certificate</span></span>
<span data-ttu-id="cc9f0-163">Aby przekazać certyfikat z podpisem własnym na platformie Azure, przejdź do **ustawienia** w portalu klasycznym, a następnie kliknij przycisk **certyfikaty zarządzania** kartę. Kliknij przycisk **przekazać** w dolnej części strony i przejdź do lokalizacji pliku CER został utworzony.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-163">To upload a self-signed certificate to Azure, go to the **Settings** page in the classic portal, then click the **Management Certificates** tab. Click **Upload** at the bottom of the page and navigate to the location of the CER file you created.</span></span>

#### <a name="convert-the-pfx-file-into-jks"></a><span data-ttu-id="cc9f0-164">Konwertowanie pliku PFX JKS</span><span class="sxs-lookup"><span data-stu-id="cc9f0-164">Convert the PFX file into JKS</span></span>
<span data-ttu-id="cc9f0-165">W wierszu polecenia systemu Windows (uruchomionego jako administrator), dysk cd do katalogu zawierającego certyfikaty i uruchom następujące polecenie, gdzie `<java-install-dir>` jest katalogiem zainstalowane Java na komputerze:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-165">In the Windows Command Prompt (running as admin), cd to the directory containing the certificates and run the following command, where `<java-install-dir>` is the directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="cc9f0-166">Po wyświetleniu monitu wprowadź hasło magazynu kluczy docelowej. są to hasło dla pliku JKS.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-166">When prompted, enter the destination keystore password; this will be the password for the JKS file.</span></span>
2. <span data-ttu-id="cc9f0-167">Po wyświetleniu monitu wprowadź hasło źródła magazynu kluczy. jest to hasło określone dla pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-167">When prompted, enter the source keystore password; this is the password you specified for the PFX file.</span></span>

<span data-ttu-id="cc9f0-168">Dwa hasła nie mają być takie same.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-168">The two passwords do not have to be the same.</span></span> <span data-ttu-id="cc9f0-169">Hasło nie można wprowadzić, chociaż nie jest to zalecane.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="cc9f0-170">Tworzenie aplikacji do tworzenia aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="cc9f0-170">Build a Web App creation application</span></span>
### <a name="create-the-eclipse-workspace-and-maven-project"></a><span data-ttu-id="cc9f0-171">Tworzenie obszaru roboczego Eclipse i projekt Maven</span><span class="sxs-lookup"><span data-stu-id="cc9f0-171">Create the Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="cc9f0-172">W tej sekcji utworzysz obszaru roboczego i projekt Maven aplikacji tworzenia aplikacji sieci web, o nazwie AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-172">In this section you create a workspace and a Maven project for the web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="cc9f0-173">Utwórz nowy projekt Maven.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-173">Create a new Maven project.</span></span> <span data-ttu-id="cc9f0-174">Kliknij przycisk **Plik > Nowy > Projekt Maven**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="cc9f0-175">W **nowy projekt Maven**, wybierz pozycję **Tworzenie prostego projektu** i **Użyj domyślnej lokalizacji obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="cc9f0-176">Na drugiej stronie **nowy projekt Maven**, podaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-176">On the second page of **New Maven Project**, specify the following:</span></span>
   
   * <span data-ttu-id="cc9f0-177">Identyfikator grupy:`com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="cc9f0-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="cc9f0-178">Identyfikator artefaktu: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="cc9f0-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="cc9f0-179">Wersja: 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="cc9f0-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="cc9f0-180">Pakowanie: jar</span><span class="sxs-lookup"><span data-stu-id="cc9f0-180">Packaging: jar</span></span>
   * <span data-ttu-id="cc9f0-181">Nazwa: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="cc9f0-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="cc9f0-182">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-182">Click **Finish**.</span></span>
3. <span data-ttu-id="cc9f0-183">Otwórz plik pom.xml nowy projekt w Eksploratorze projektu.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-183">Open the new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="cc9f0-184">Wybierz **zależności** kartę. Jak jest to nowy projekt, wymieniono jeszcze żadnych pakietów.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-184">Select the **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="cc9f0-185">Otwórz widok repozytoria Maven.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-185">Open the Maven Repositories view.</span></span> <span data-ttu-id="cc9f0-186">**Kliknij przycisk okna > Pokaż widok > Inne > Maven > repozytoria Maven** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="cc9f0-187">**Repozytoria Maven** widoku będą wyświetlane w dolnej części IDE.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-187">The **Maven Repositories** view will appear at the bottom of the IDE.</span></span>
5. <span data-ttu-id="cc9f0-188">Otwórz **globalne repozytoria**, kliknij prawym przyciskiem myszy **centralnej** repozytorium, a następnie wybierz **Rebuild Index**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-188">Open **Global Repositories**, right-click the **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="cc9f0-189">Ten krok może potrwać kilka minut w zależności od prędkości połączenia.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-189">This step can take several minutes depending on the speed of your connection.</span></span> <span data-ttu-id="cc9f0-190">Jeśli spowoduje odbudowanie indeksu, powinny pojawić się pakietów Microsoft Azure w **centralnej** Maven repozytorium.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-190">When the index rebuilds, you should see the Microsoft Azure packages in the **central** Maven repository.</span></span>
6. <span data-ttu-id="cc9f0-191">W **zależności**, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="cc9f0-192">W **wprowadź identyfikator grupy...**  wprowadź `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="cc9f0-193">Wybierz pakiety do zarządzania podstawowej i zarządzania aplikacjami sieci Web usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-193">Select the packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="cc9f0-194">**Uwaga:** Jeśli aktualizujesz zależności po wydaniu nowej wersji, należy ponownie dodać wszystkich zależności na tej liście.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-194">**Note:** If you are updating the dependencies after a new version release, you need to re-add each of the dependencies in this list.</span></span>
   > <span data-ttu-id="cc9f0-195">Po kliknięciu **Dodaj** i wybierz poszczególne zależności wydaje się przy użyciu nowego numeru wersji w **zależności** listy.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-195">After you click **Add** and select each dependency, it appears with the new version number in the **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="cc9f0-196">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-196">Click **OK**.</span></span> <span data-ttu-id="cc9f0-197">Następnie Azure pakiety są wyświetlane w **zależności** listy.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-197">The Azure packages then appear in the **Dependencies** list.</span></span>

### <a name="writing-java-code-to-create-a-web-app-by-calling-the-azure-sdk"></a><span data-ttu-id="cc9f0-198">Pisanie kodu języka Java do utworzenia aplikacji sieci Web przez wywołanie metody Azure SDK</span><span class="sxs-lookup"><span data-stu-id="cc9f0-198">Writing Java Code to Create a Web App by Calling the Azure SDK</span></span>
<span data-ttu-id="cc9f0-199">Następnie należy napisać kod, który wywołuje interfejsy API w zestawie SDK Azure dla języka Java można utworzyć aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-199">Next, write the code that calls APIs in the Azure SDK for Java to create the App Service web app.</span></span>

1. <span data-ttu-id="cc9f0-200">Utwórz klasę języka Java, zawiera kod punktu wejścia głównego.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-200">Create a Java class to contain the main entry point code.</span></span> <span data-ttu-id="cc9f0-201">W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy węzeł projektu i wybierz **nowy > klasy**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-201">In Project Explorer, right-click on the project node and select **New > Class**.</span></span>
2. <span data-ttu-id="cc9f0-202">W **Nowa Klasa Java**, nazwa klasy `WebCreator` i sprawdź **publiczne statyczne void main** wyboru.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-202">In **New Java Class**, name the class `WebCreator` and check the **public static void main** checkbox.</span></span> <span data-ttu-id="cc9f0-203">Wybór powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-203">The selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="cc9f0-204">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-204">Click **Finish**.</span></span> <span data-ttu-id="cc9f0-205">Plik WebCreator.java pojawia się w obszarze Eksplorator projektów.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-205">The WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-the-azure-api-to-create-an-app-service-web-app"></a><span data-ttu-id="cc9f0-206">Wywołanie interfejsu API Azure do utworzenia aplikacji sieci Web usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="cc9f0-206">Calling the Azure API to Create an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="cc9f0-207">Dodaj niezbędne importów</span><span class="sxs-lookup"><span data-stu-id="cc9f0-207">Add necessary imports</span></span>
<span data-ttu-id="cc9f0-208">W WebCreator.java Dodaj następujące instrukcje importu; Importy te zapewniają dostęp do klas w bibliotekach zarządzania służący do konsumowania interfejsów API usługi Azure:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-208">In WebCreator.java, add the following imports; these imports provide access to classes in the management libraries for consuming Azure APIs:</span></span>

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


#### <a name="define-the-main-entry-point-class"></a><span data-ttu-id="cc9f0-209">W definicji klasy punktu wejścia głównego</span><span class="sxs-lookup"><span data-stu-id="cc9f0-209">Define the main entry point class</span></span>
<span data-ttu-id="cc9f0-210">Ponieważ aplikacja AzureWebDemo ma na celu utworzyć aplikację usługi aplikacji sieci Web, nazw klasy głównym dla tej aplikacji `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-210">Because the purpose of the AzureWebDemo application is to create an App Service Web App, name the main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="cc9f0-211">Ta klasa zawiera kod punktu wejścia głównego, który wywołuje interfejs API zarządzania usługami Azure do utworzenia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-211">This class provides the main entry point code that calls the Azure Service Management API to create the web app.</span></span>

<span data-ttu-id="cc9f0-212">Dodaj następujące definicje parametr przestrzeni sieci Web i aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-212">Add the following parameter definitions for the web app and webspace.</span></span> <span data-ttu-id="cc9f0-213">Należy podać informacje identyfikator i certyfikat własne subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-213">You will need to provide your own Azure subscription ID and certificate information.</span></span>

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

<span data-ttu-id="cc9f0-214">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-214">where:</span></span>

* <span data-ttu-id="cc9f0-215">`<subscription-id>`jest identyfikator subskrypcji platformy Azure, w którym chcesz utworzyć zasobu.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-215">`<subscription-id>` is the Azure subscription ID in which you want to create the resource.</span></span>
* <span data-ttu-id="cc9f0-216">`<certificate-store-path>`to ścieżka i nazwa pliku JKS w katalogu magazynu lokalnego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-216">`<certificate-store-path>` is the path and filename to the JKS file in your local certificate store directory.</span></span> <span data-ttu-id="cc9f0-217">Na przykład `C:/Certificates/CertificateName.jks` dla systemu Linux i `C:\Certificates\CertificateName.jks` dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="cc9f0-218">`<certificate-password>`jest to hasło określone podczas tworzenia certyfikatu JKS.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-218">`<certificate-password>` is the password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="cc9f0-219">`webAppName`może być dowolna nazwa, którą wybierzesz; Ta procedura używa nazwy `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-219">`webAppName` can be any name you choose; this procedure uses the name `WebDemoWebApp`.</span></span> <span data-ttu-id="cc9f0-220">Pełna nazwa domeny jest `webAppName` z `domainName` dołączone, w tym przypadku pełną domenę jest `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-220">The full domain name is the `webAppName` with the `domainName` appended, so in this case the full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="cc9f0-221">`domainName`należy określić, jak pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="cc9f0-222">`webSpaceName`musi mieć jedną z wartości zdefiniowanych w [WebSpaceNames] [ WebSpaceNames] klasy.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-222">`webSpaceName` should be one of the values defined in the [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="cc9f0-223">`appServicePlanName`należy określić, jak pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="cc9f0-224">**Uwaga:** zawsze uruchomić tę aplikację, należy zmienić wartość `webAppName` i `appServicePlanName` (lub usunąć aplikacji sieci web w portalu Azure) przed uruchomieniem aplikacji ponownie.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-224">**Note:** Each time you run this application, you need to change the value of `webAppName` and `appServicePlanName` (or delete the web app on the Azure Portal) before running the application again.</span></span> <span data-ttu-id="cc9f0-225">W przeciwnym razie wykonanie zakończy się niepowodzeniem, ponieważ istnieje już tego samego zasobu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-225">Otherwise, execution will fail because the same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-the-web-creation-method"></a><span data-ttu-id="cc9f0-226">Zdefiniuj metodę tworzenia sieci web</span><span class="sxs-lookup"><span data-stu-id="cc9f0-226">Define the web creation method</span></span>
<span data-ttu-id="cc9f0-227">Następnie określ metodę, aby utworzyć aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-227">Next, define a method to create the web app.</span></span> <span data-ttu-id="cc9f0-228">Ta metoda `createWebApp`, określa parametry przestrzeni sieci Web i aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-228">This method, `createWebApp`, specifies the parameters of the web app and the webspace.</span></span> <span data-ttu-id="cc9f0-229">Również tworzy i konfiguruje klienta zarządzania aplikacji usługi sieci Web aplikacji, który jest zdefiniowany przez [WebSiteManagementClient] [ WebSiteManagementClient] obiektu.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-229">It also creates and configures the App Service Web Apps management client, which is defined by the [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="cc9f0-230">Klient zarządzania jest kluczem do tworzenia aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-230">The management client is key to creating Web Apps.</span></span> <span data-ttu-id="cc9f0-231">Zapewnia usługi sieci web RESTful, które umożliwiają aplikacji do zarządzania aplikacjami sieci web (wykonywanie operacji, takich jak tworzenie, update i delete) przez wywołanie interfejsu API zarządzania usługami.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-231">It provides RESTful web services that allow applications to manage web apps (performing operations such as create, update, and delete) by calling the service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for the App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path to the JKS file
            keyStorePassword,  // Password for the JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create the App Service Web Apps management client to call Azure APIs
        // and pass it the App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for the web app with the specified parameters.
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
        // Note that the server farm name takes the Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define the web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create the web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output the HTTP status code of the response; 200 indicates the request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output the name of the web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="cc9f0-232">Kod stanu HTTP odpowiedzi wskazujący powodzenie lub niepowodzenie dane wyjściowe obejmują i w razie powodzenia dane wyjściowe obejmują nazwę utworzonej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-232">The code will output the HTTP status of the response indicating success or failure, and if successful, will output the name of the created web app.</span></span>

#### <a name="define-the-main-method"></a><span data-ttu-id="cc9f0-233">Zdefiniuj metodę main()</span><span class="sxs-lookup"><span data-stu-id="cc9f0-233">Define the main() method</span></span>
<span data-ttu-id="cc9f0-234">Podaj kod metody main(), który wywołuje createWebApp() do utworzenia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-234">Provide the main() method code that calls createWebApp() to create the web app.</span></span>

<span data-ttu-id="cc9f0-235">Na koniec wywołania `createWebApp` z `main`:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-the-application-and-verify-web-app-creation"></a><span data-ttu-id="cc9f0-236">Uruchom aplikację i sprawdzić, tworzenie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="cc9f0-236">Run the application and verify web app creation</span></span>
<span data-ttu-id="cc9f0-237">Aby sprawdzić, czy aplikacja działa, kliknij przycisk **Uruchom > Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-237">To verify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="cc9f0-238">Po zakończeniu działania aplikacji powinny być widoczne następujące dane wyjściowe w konsoli programu Eclipse:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-238">When the application completes running, you should see the following output in the Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="cc9f0-239">Zaloguj się do klasycznego portalu Azure i kliknij przycisk **aplikacje sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-239">Log into the Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="cc9f0-240">W nowej aplikacji sieci web powinna zostać wyświetlona na liście aplikacji sieci Web w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-240">The new web app should appear in the Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-to-the-web-app"></a><span data-ttu-id="cc9f0-241">Wdrażanie aplikacji w aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="cc9f0-241">Deploying an Application to the Web App</span></span>
<span data-ttu-id="cc9f0-242">Po uruchomiono AzureWebDemo i utworzyć nową aplikację sieci web, zaloguj się do klasycznego portalu kliknij **aplikacje sieci Web**i wybierz **WebDemoWebApp** w **aplikacje sieci Web** listy.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-242">After you have run AzureWebDemo and created the new web app, log into the classic portal, click **Web Apps**, and select **WebDemoWebApp** in the **Web Apps** list.</span></span> <span data-ttu-id="cc9f0-243">Na stronie pulpitu nawigacyjnego aplikacji sieci web, kliknij przycisk **Przeglądaj** (lub kliknij adres URL, `webdemowebapp.azurewebsites.net`) można przejść do niego.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-243">In the web app's dashboard page, click **Browse** (or click the URL, `webdemowebapp.azurewebsites.net`) to navigate to it.</span></span> <span data-ttu-id="cc9f0-244">Zostanie wyświetlona strona pusty symbol zastępczy, ponieważ żadna zawartość została opublikowana do aplikacji sieci web jeszcze.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-244">You will see a blank placeholder page, because no content has been published to the web app yet.</span></span>

<span data-ttu-id="cc9f0-245">Następnie utworzysz aplikację "Hello World" i wdrażanie dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-245">Next you will create a "Hello World" application and deploy it to the web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="cc9f0-246">Utwórz aplikację JSP Hello World</span><span class="sxs-lookup"><span data-stu-id="cc9f0-246">Create a JSP Hello World application</span></span>
#### <a name="create-the-application"></a><span data-ttu-id="cc9f0-247">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="cc9f0-247">Create the application</span></span>
<span data-ttu-id="cc9f0-248">W celu zaprezentowania sposobu wdrażania aplikacji w sieci Web, Poniższa procedura pokazuje sposób tworzenia prostej aplikacji Java "Hello World" i przekaż go do aplikacji sieci Web usługi aplikacji utworzony w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-248">In order to demonstrate how to deploy an application to the web, the following procedure shows you how to create a simple "Hello World" Java application and upload it to the App Service Web App that your application created.</span></span>

1. <span data-ttu-id="cc9f0-249">Kliknij przycisk **Plik > Nowy > Projekt sieci Web dynamiczne**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="cc9f0-250">Nadaj jej nazwę `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-250">Name it `JSPHello`.</span></span> <span data-ttu-id="cc9f0-251">Nie trzeba zmienić ustawienia w tym oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-251">You do not need to change any other settings in this dialog.</span></span> <span data-ttu-id="cc9f0-252">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="cc9f0-253">W obszarze Eksplorator projektów rozwiń **JSPHello** projektu, kliknij prawym przyciskiem myszy **WebContent**, następnie kliknij przycisk **nowy > pliku JSP**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-253">In Project Explorer, expand the **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="cc9f0-254">W oknie dialogowym Nowy plik JSP nazwę nowego pliku `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-254">In the New JSP File dialog, name the new file `index.jsp`.</span></span> <span data-ttu-id="cc9f0-255">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-255">Click **Next**.</span></span>
3. <span data-ttu-id="cc9f0-256">W **wybierz szablon JSP** zaznacz pozycję **New JSP File (html)** i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-256">In the **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="cc9f0-257">W index.jsp, Dodaj następujący kod w `<head>` i `<body>` tagu sekcje:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-257">In index.jsp, add the following code in the `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, the time is <%= date %> 
        </body>

#### <a name="run-the-hello-world-application-in-localhost"></a><span data-ttu-id="cc9f0-258">Uruchamianie aplikacji Hello World w localhost</span><span class="sxs-lookup"><span data-stu-id="cc9f0-258">Run the Hello World application in localhost</span></span>
<span data-ttu-id="cc9f0-259">Przed uruchomieniem tej aplikacji, musisz skonfigurować kilka właściwości.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-259">Before you run this application, you need to configure a few properties.</span></span>

1. <span data-ttu-id="cc9f0-260">Kliknij prawym przyciskiem myszy **JSPHello** projekt i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-260">Right-click the **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="cc9f0-261">W **właściwości** okna dialogowego: Wybierz **ścieżka kompilacji języka Java**, wybierz pozycję **kolejność i eksportowanie** karcie wyboru **biblioteka systemu środowiska JRE**, następnie kliknij przycisk **Się** Aby przenieść go na początku listy.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-261">In the **Properties** dialog: select **Java Build Path**, select the **Order and Export** tab, check **JRE System Library**, then click **Up** to move it to the top of the list.</span></span>
   
    ![][4]
3. <span data-ttu-id="cc9f0-262">Również w **właściwości** okna dialogowego: Wybierz **docelowe środowiska uruchomieniowe** i kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-262">Also in the **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="cc9f0-263">W **nowe środowisko uruchomieniowe serwera** okno dialogowe, wybierz serwer, takich jak **Apache Tomcat v7.0** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-263">In the **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="cc9f0-264">W **serwera Tomcat** okno dialogowe, zestaw **nazwa** do `Apache Tomcat v7.0`i ustaw **katalog instalacyjny serwera Tomcat** do katalogu, w którym zainstalowano wersję serwera Tomcat serwer, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-264">In the **Tomcat Server** dialog, set **Name** to `Apache Tomcat v7.0`, and set **Tomcat Installation Directory** to the directory in which you installed the version of Tomcat server you want to use.</span></span>
   
    ![][5]
   
    <span data-ttu-id="cc9f0-265">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-265">Click **Finish**.</span></span>
5. <span data-ttu-id="cc9f0-266">Następnie wróć do **docelowe środowiska uruchomieniowe** strony **właściwości** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-266">You then return to the **Targeted Runtimes** page of the **Properties** dialog.</span></span> <span data-ttu-id="cc9f0-267">Wybierz **Apache Tomcat v7.0**, następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="cc9f0-268">W środowisku Eclipse **Uruchom** menu, kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-268">In the Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="cc9f0-269">W **Uruchom jako** okno dialogowe, wybierz opcję **Uruchom na serwerze**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-269">In the **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="cc9f0-270">W **Uruchom na serwerze** okno dialogowe, wybierz opcję **Tomcat v7.0 Server**:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-270">In the **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="cc9f0-271">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-271">Click **Finish**.</span></span>
7. <span data-ttu-id="cc9f0-272">Gdy aplikacja zostanie uruchomiona, powinny pojawić się **JSPHello** strony są wyświetlane w oknie localhost w środowisku Eclipse (`http://localhost:8080/JSPHello/`), wyświetlanie następujący komunikat:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-272">When the application runs, you should see the **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying the following message:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-the-application-as-a-war"></a><span data-ttu-id="cc9f0-273">Wyeksportować aplikację jako plik WAR</span><span class="sxs-lookup"><span data-stu-id="cc9f0-273">Export the application as a WAR</span></span>
<span data-ttu-id="cc9f0-274">Wyeksportuj pliki projektu sieci web jako plik archiwum (plik WAR) w sieci web tak, aby umożliwić jej wdrażanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-274">Export the web project files as a web archive (WAR) file so that you can deploy it to the web app.</span></span> <span data-ttu-id="cc9f0-275">Następujące pliki projektu sieci web znajdują się w folderze WebContent:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-275">The following web project files reside in the WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="cc9f0-276">Kliknij prawym przyciskiem myszy WebContent folder i wybierz **wyeksportować**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-276">Right-click the WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="cc9f0-277">W **eksportu wybierz** okna dialogowego, kliknij przycisk **sieci Web > WAR** pliku, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-277">In the **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="cc9f0-278">W **wyeksportować plik WAR** okno dialogowe, wybierz katalog src w bieżącym projekcie i zawierać nazwę pliku WAR na końcu.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-278">In the **WAR Export** dialog, select the src directory in the current project, and include the name of the WAR file at the end.</span></span> <span data-ttu-id="cc9f0-279">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="cc9f0-280">Aby uzyskać więcej informacji na temat wdrażania WAR plików, zobacz [dodawania aplikacji Java do aplikacji sieci Web usługi aplikacji Azure](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="cc9f0-280">For more information on deploying WAR files, see [Add a Java application to Azure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-the-hello-world-application-using-ftp"></a><span data-ttu-id="cc9f0-281">Wdrażanie aplikacji World Hello za pomocą protokołu FTP</span><span class="sxs-lookup"><span data-stu-id="cc9f0-281">Deploying the Hello World Application Using FTP</span></span>
<span data-ttu-id="cc9f0-282">Wybierz klienta FTP innych firm, aby opublikować aplikację.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-282">Select a third-party FTP client to publish the application.</span></span> <span data-ttu-id="cc9f0-283">W tej procedurze opisano dwie opcje: konsoli Kudu wbudowanych w środowisku Azure. i FileZilla, narzędzie popularnych o wygodny graficznego interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-283">This procedure describes two options: the Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="cc9f0-284">**Uwaga:** zestawu narzędzi platformy Azure dla programu Eclipse obsługuje wdrażanie do kont magazynu i chmury usługi, ale nie obsługuje obecnie wdrożenia w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-284">**Note:** The Azure Toolkit for Eclipse supports deployment to storage accounts and cloud services, but does not currently support deployment to web apps.</span></span> <span data-ttu-id="cc9f0-285">Można wdrożyć do kont magazynu i usług przy użyciu projektu wdrożenia platformy Azure, zgodnie z opisem w chmurze [tworzenia aplikacji Hello World na platformie Azure w programie Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), ale nie do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-285">You can deploy to storage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not to web apps.</span></span> <span data-ttu-id="cc9f0-286">Użyj innych metod, takich jak FTP lub GitHub do transferu plików do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-286">Use other methods such as FTP or GitHub to transfer files to your web app.</span></span>
> 
> <span data-ttu-id="cc9f0-287">**Uwaga:** nie zaleca się używania protokołu FTP z wiersza polecenia systemu Windows (narzędzie wiersza polecenia FTP.EXE jest dostarczana z systemem Windows).</span><span class="sxs-lookup"><span data-stu-id="cc9f0-287">**Note:** We do not recommend using FTP from the Windows command prompt (the command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="cc9f0-288">Klienci FTP, którzy używają active FTP, takich jak FTP.EXE, często nie działać za pośrednictwem zapór.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-288">FTP clients that use active FTP, such as FTP.EXE, often fail to work over firewalls.</span></span> <span data-ttu-id="cc9f0-289">Aktywne FTP określa wewnętrzny adres sieci LAN, do którego serwer FTP prawdopodobnie nie będzie można połączyć.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-289">Active FTP specifies an internal LAN-based address, to which an FTP server will likely fail to connect.</span></span>
> 
> 

<span data-ttu-id="cc9f0-290">Aby uzyskać więcej informacji na wdrożenia dla aplikacji sieci web usługi aplikacji za pomocą protokołu FTP zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-290">For more information on deployment to an App Service web app using FTP, see the following topics:</span></span>

* [<span data-ttu-id="cc9f0-291">Wdrażanie przy użyciu narzędzia FTP</span><span class="sxs-lookup"><span data-stu-id="cc9f0-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="cc9f0-292">Konfigurowanie poświadczeń wdrożenia</span><span class="sxs-lookup"><span data-stu-id="cc9f0-292">Set up deployment credentials</span></span>
<span data-ttu-id="cc9f0-293">Upewnij się, że została uruchomiona **AzureWebDemo** aplikacji w celu utworzenia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-293">Make sure you have run the **AzureWebDemo** application to create a web app.</span></span> <span data-ttu-id="cc9f0-294">Przenieś pliki do tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-294">You will transfer files to this location.</span></span>

1. <span data-ttu-id="cc9f0-295">Zaloguj się do klasycznego portalu i kliknij przycisk **aplikacje sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-295">Log into the classic portal and click **Web Apps**.</span></span> <span data-ttu-id="cc9f0-296">Upewnij się, że **WebDemoWebApp** pojawią się na liście aplikacji sieci web i upewnij się, że jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-296">Make sure **WebDemoWebApp** appears in the list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="cc9f0-297">Kliknij przycisk **WebDemoWebApp** aby otworzyć jego **pulpitu nawigacyjnego** strony.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-297">Click **WebDemoWebApp** to open its **Dashboard** page.</span></span>
2. <span data-ttu-id="cc9f0-298">Na **pulpitu nawigacyjnego** w obszarze **szybki przegląd**, kliknij przycisk **skonfigurować poświadczenia wdrażania** (Jeśli masz już poświadczenia wdrażania, odczytuje  **Resetowanie poświadczeń wdrażania**).</span><span class="sxs-lookup"><span data-stu-id="cc9f0-298">On the **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="cc9f0-299">Wdrożenie poświadczenia są skojarzone z kontem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="cc9f0-300">Należy określić nazwę użytkownika i hasło, które można wdrożyć przy użyciu usługi Git i FTP.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-300">You need to specify a username and password that you can use to deploy using Git and FTP.</span></span> <span data-ttu-id="cc9f0-301">Te poświadczenia można użyć do wdrożenia do wszystkich aplikacji sieci web w ramach wszystkich subskrypcji platformy Azure skojarzonych z Twoim kontem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-301">You can use these credentials to deploy to any web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="cc9f0-302">Podaj poświadczenia wdrożenia usługi Git i FTP, w oknie dialogowym i Zapisz nazwę użytkownika i hasło do użycia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-302">Provide Git and FTP deployment credentials in the dialog, and record the username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="cc9f0-303">Uzyskiwanie informacji o połączeniu FTP</span><span class="sxs-lookup"><span data-stu-id="cc9f0-303">Get FTP connection information</span></span>
<span data-ttu-id="cc9f0-304">Aby użyć FTP do wdrażania plików aplikacji do nowo utworzonej aplikacji sieci web, należy uzyskać informacje o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-304">To use FTP to deploy application files to the newly created web app, you need to obtain connection information.</span></span> <span data-ttu-id="cc9f0-305">Istnieją dwie metody uzyskiwania informacji o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-305">There are two ways to obtain connection information.</span></span> <span data-ttu-id="cc9f0-306">Jednym ze sposobów jest odwiedzać aplikacji sieci web **pulpitu nawigacyjnego** strony; inny sposób jest do pobrania w sieci web w aplikacji profilu publikowania.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-306">One way is to visit the web app's **Dashboard** page; the other way is to download the web app's publish profile.</span></span> <span data-ttu-id="cc9f0-307">Profil publikowania jest plik XML, który zawiera informacje, takie jak hosta FTP poświadczenia nazwy i logowania dla aplikacji sieci web w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-307">The publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="cc9f0-308">Do wdrożenia do wszystkich aplikacji sieci web w ramach wszystkich subskrypcji skojarzonych z konta platformy Azure, a nie tylko ten jeden, można użyć tej nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-308">You can use this username and password to deploy to any web app in all subscriptions associated with the Azure account, not only this one.</span></span>

<span data-ttu-id="cc9f0-309">Aby uzyskać informacje o połączeniu FTP w bloku aplikacja sieci web w [Azure Portal][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-309">To obtain FTP connection information from the web app's blade in the [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="cc9f0-310">W obszarze **Essentials**, należy znaleźć i skopiować **nazwa hosta FTP**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-310">Under **Essentials**, find and copy the **FTP hostname**.</span></span> <span data-ttu-id="cc9f0-311">Jest to podobne do identyfikatora URI `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-311">This is a URI similar to `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="cc9f0-312">W obszarze **Essentials**, należy znaleźć i skopiować **nazwy użytkownika serwera FTP/wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="cc9f0-313">Będzie to mieć postać *webappname\deployment-username*, na przykład `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-313">This will have the form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="cc9f0-314">Aby uzyskać informacje o połączeniu FTP z profil publikowania:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-314">To obtain FTP connection information from the publish profile:</span></span>

1. <span data-ttu-id="cc9f0-315">W bloku aplikacja sieci web kliknij **profilu publikowania Get**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-315">In the web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="cc9f0-316">Pobierze plik .publishsettings na dysk lokalny.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-316">This will download a .publishsettings file to your local drive.</span></span>
2. <span data-ttu-id="cc9f0-317">Otwórz plik .publishsettings w edytorze XML lub edytorze tekstów i Znajdź `<publishProfile>` zawierający element `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-317">Open the .publishsettings file in an XML editor or text editor and find the `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="cc9f0-318">Jego wygląd powinien być podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-318">It should look like the following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="cc9f0-319">Należy pamiętać, że aplikacja sieci web `publishProfile` ustawienia mapy w celu ustawienia Menedżera lokacji FileZilla w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-319">Note that the web app's `publishProfile` settings map to the FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="cc9f0-320">`publishUrl`jest taka sama jak **nazwa hosta FTP**, wartość ustawiona w **hosta**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-320">`publishUrl` is the same as **FTP host name**, the value you set in **Host**.</span></span>
* <span data-ttu-id="cc9f0-321">`publishMethod="FTP"`oznacza, że ustawisz **protokołu** do **FTP - File Transfer Protocol**, i **szyfrowania** do **za pomocą zwykłego FTP**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-321">`publishMethod="FTP"` means that you set **Protocol** to **FTP - File Transfer Protocol**, and **Encryption** to **Use plain FTP**.</span></span>
* <span data-ttu-id="cc9f0-322">`userName`i `userPWD` są klucze rzeczywistej nazwy użytkownika i określone podczas resetowania poświadczenia wdrażania wartości hasła.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-322">`userName` and `userPWD` are keys for the actual username and password values you specified when you reset the deployment credentials.</span></span> <span data-ttu-id="cc9f0-323">`userName`jest taka sama jak **wdrożenia / FTP użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-323">`userName` is the same as **Deployment / FTP user**.</span></span> <span data-ttu-id="cc9f0-324">Są one wykonywane na **użytkownika** i **hasło** w FileZilla.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-324">They map to **User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="cc9f0-325">`ftpPassiveMode="True"`oznacza, że witryna FTP używa pasywnym transferu FTP; Wybierz **pasywnym** na **ustawienia transferu** kartę.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-325">`ftpPassiveMode="True"` means that the FTP site uses passive FTP transfer; select **Passive** on the **Transfer Settings** tab.</span></span>

#### <a name="configure-the-web-app-to-host-a-java-application"></a><span data-ttu-id="cc9f0-326">Konfigurowanie aplikacji sieci Web na potrzeby hostowania aplikacji języka Java</span><span class="sxs-lookup"><span data-stu-id="cc9f0-326">Configure the Web App to host a Java application</span></span>
<span data-ttu-id="cc9f0-327">Przed opublikowaniem aplikacji, musisz zmienić kilka ustawień konfiguracji, aby aplikacja sieci web mogą obsługiwać aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-327">Before you publish the application, you need to change a few configuration settings so that the web app can host a Java application.</span></span>

1. <span data-ttu-id="cc9f0-328">W klasycznym portalu, przejdź do aplikacji sieci web **pulpitu nawigacyjnego** i kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-328">In the classic portal, go to the web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="cc9f0-329">Na **Konfiguruj** określ następujące ustawienia.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-329">On the **Configure** page, specify the following settings.</span></span>
2. <span data-ttu-id="cc9f0-330">W **wersję Java** wartość domyślna to **poza**; wybierz wersję Java celów aplikacji, na przykład 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-330">In **Java version** the default is **Off**; select the Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="cc9f0-331">Po wykonaniu tej czynności również upewnij się, że **kontener sieci Web** jest ustawiona na wersję serwera Tomcat.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-331">After you do this, also make sure that **Web container** is set to a version of Tomcat Server.</span></span>
3. <span data-ttu-id="cc9f0-332">W **dokumenty domyślne**, Dodaj index.jsp i przenieść ją do początku listy.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-332">In **Default Documents**, add index.jsp and move it up to the top of the list.</span></span> <span data-ttu-id="cc9f0-333">(Domyślnego pliku dla aplikacji sieci web jest hostingstart.html).</span><span class="sxs-lookup"><span data-stu-id="cc9f0-333">(The default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="cc9f0-334">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="cc9f0-335">Publikowanie aplikacji przy użyciu Kudu</span><span class="sxs-lookup"><span data-stu-id="cc9f0-335">Publish your application using Kudu</span></span>
<span data-ttu-id="cc9f0-336">Jest jednym ze sposobów publikowania aplikacji do użycia konsoli debugowania aparatu Kudu wbudowanych w platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-336">One way to publish the application is to use the Kudu debug console built into Azure.</span></span> <span data-ttu-id="cc9f0-337">Program kudu jest znany jako stabilny i spójny z aplikacji sieci Web usługi aplikacji i serwer Tomcat.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-337">Kudu is known to be stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="cc9f0-338">Aby dostęp do konsoli dla aplikacji sieci web przechodząc do adresu URL mają następującą postać:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-338">You access the console for the web app by browsing to a URL of the following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="cc9f0-339">Do wykonania tej procedury konsoli Kudu znajduje się pod adresem URL; Przejdź do tej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-339">For this procedure, the Kudu console is located at the following URL; browse to this location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="cc9f0-340">Wybierz z górnego menu **konsoli debugowania > CMD**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-340">From the top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="cc9f0-341">W wierszu polecenia konsoli przejdź do `/site/wwwroot` (lub kliknij przycisk `site`, następnie `wwwroot` w katalogu widoku w górnej części strony):</span><span class="sxs-lookup"><span data-stu-id="cc9f0-341">In the console command line, navigate to `/site/wwwroot` (or click `site`, then `wwwroot` in the directory view at the top of the page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="cc9f0-342">Po określeniu **wersję Java**, serwer Tomcat należy utworzyć katalogu webapps.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="cc9f0-343">W wierszu polecenia konsoli przejdź do katalogu webapps:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-343">In the console command line, navigate to the webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="cc9f0-344">Przeciągnij JSPHello.war z `<project-path>/JSPHello/src/` i upuść go w widoku katalogu Kudu w `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into the Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="cc9f0-345">Nie przeciągnij go do obszaru "Przeciągnij tutaj, aby przekazać i zip", ponieważ Tomcat będzie Rozpakuj go.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-345">Do not drag it to the "Drag here to upload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="cc9f0-346">W pierwszym JSPHello.war pojawia się w obszarze Katalog samodzielnie:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-346">At first JSPHello.war appears in the directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="cc9f0-347">W krótkim czasie (prawdopodobnie mniej niż 5 minut) serwer Tomcat będzie Rozpakuj plik WAR do rozpakowanego katalogu JSPHello.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip the WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="cc9f0-348">Kliknij katalog główny, aby sprawdzić, czy index.jsp zostało rozpakowane i skopiować.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-348">Click the ROOT directory to see whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="cc9f0-349">Jeśli tak, przejdź do katalogu webapps, aby sprawdzić, czy rozpakowanego katalogu JSPHello została utworzona.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-349">If so, navigate back to the webapps directory to see whether the unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="cc9f0-350">Jeśli te elementy nie jest widoczny, poczekaj i powtórz.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="cc9f0-351">Publikowanie aplikacji przy użyciu FileZilla (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="cc9f0-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="cc9f0-352">Innego narzędzia używanego do publikowania aplikacji jest FileZilla, popularnych klient FTP innych firm z wygodny graficznego interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-352">Another tool you can use to publish the application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="cc9f0-353">Można pobrać i zainstalować FileZilla z [http://filezilla-project.org/](http://filezilla-project.org/) Jeśli użytkownik nie ma jeszcze go.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="cc9f0-354">Aby uzyskać więcej informacji na temat używania klienta, zobacz [dokumentacji FileZilla](https://wiki.filezilla-project.org/Documentation) i ten wpis w blogu na [klienci FTP — część 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc9f0-354">For more information on using the client, see the [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="cc9f0-355">W FileZilla, kliknij przycisk **Plik > Menedżer lokacji**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="cc9f0-356">W **Menedżer lokacji** okna dialogowego, kliknij przycisk **nowej lokacji**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-356">In the **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="cc9f0-357">Nowa, pusta witryna FTP będą wyświetlane w **wybierz wpis** monitowania użytkownika o podanie nazwy.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-357">A new blank FTP site will appear in **Select Entry** prompting you to provide a name.</span></span> <span data-ttu-id="cc9f0-358">Do wykonania tej procedury, nadaj mu nazwę `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="cc9f0-359">Na **ogólne** karcie, określ następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-359">On the **General** tab, specify the following settings:</span></span>
   
   * <span data-ttu-id="cc9f0-360">**Host:** Enter **nazwa hosta FTP** skopiowany z poziomu pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-360">**Host:** Enter the **FTP Host Name** that you copied from the dashboard.</span></span>
   * <span data-ttu-id="cc9f0-361">**Port:** (to pole pozostanie puste, jak to przeniesienie pasywny oraz określić port używany serwer.)</span><span class="sxs-lookup"><span data-stu-id="cc9f0-361">**Port:** (Leave this blank, as this is a passive transfer and the server will determine the port to use.)</span></span>
   * <span data-ttu-id="cc9f0-362">**Protokół:** protokół transferu plików FTP</span><span class="sxs-lookup"><span data-stu-id="cc9f0-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="cc9f0-363">**Szyfrowanie:** za pomocą zwykłego FTP</span><span class="sxs-lookup"><span data-stu-id="cc9f0-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="cc9f0-364">**Typ logowania:** normalny</span><span class="sxs-lookup"><span data-stu-id="cc9f0-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="cc9f0-365">**Użytkownik:** wprowadzić rozmieszczenia / FTP użytkownika, które zostały skopiowane z poziomu pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-365">**User:** Enter the Deployment / FTP user that you copied from the dashboard.</span></span> <span data-ttu-id="cc9f0-366">Jest to pełna username FTP, która ma postać *webappname\username*.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-366">This is the full FTP username, which has the form *webappname\username*.</span></span>
   * <span data-ttu-id="cc9f0-367">**Hasło:** wprowadź hasło określone podczas ustawiania poświadczeń wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-367">**Password:** Enter the password that you specified when you set the deployment credentials.</span></span>
     
     <span data-ttu-id="cc9f0-368">Na **ustawienia transferu** wybierz opcję **pasywnym**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-368">On the **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="cc9f0-369">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-369">Click **Connect**.</span></span> <span data-ttu-id="cc9f0-370">Jeśli powodzenia FileZilla na konsoli zostanie wyświetlony `Status: Connected` komunikat i problem `LIST` polecenie, aby wyświetlić listę zawartości katalogu.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command to list the directory contents.</span></span>
4. <span data-ttu-id="cc9f0-371">W **lokalnego** lokacji panelu, wybierz katalog źródłowy, w którym znajduje się plik JSPHello.war; ścieżka będzie podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-371">In the **Local** site panel, select the source directory in which the JSPHello.war file resides; the path will be similar to the following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="cc9f0-372">W **zdalnego** lokacji panelu, wybierz folder docelowy.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-372">In the **Remote** site panel, select the destination folder.</span></span> <span data-ttu-id="cc9f0-373">Zostanie wdrożona plik WAR do `webapps` katalog główny aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-373">You will deploy the WAR file to the `webapps` directory under the web app's root.</span></span> <span data-ttu-id="cc9f0-374">Przejdź do `/site/wwwroot`, kliknij prawym przyciskiem myszy `wwwroot`i wybierz **Utwórz katalog**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-374">Navigate to `/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="cc9f0-375">Nazwa katalogu `webapps` , a następnie wprowadź tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-375">Name the directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="cc9f0-376">Transfer JSPHello.war do `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-376">Transfer JSPHello.war to `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="cc9f0-377">Wybierz JSPHello.war w **lokalnego** listy plików, kliknij prawym przyciskiem myszy na nim i wybierz **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-377">Select JSPHello.war in the **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="cc9f0-378">Powinny pojawić się ją na `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="cc9f0-379">Po skopiowaniu JSPHello.war do katalogu webapps serwera Tomcat zostanie automatycznie Rozpakuj (Rozpakuj) plików w pliku WAR.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-379">After you copy JSPHello.war to the webapps directory, Tomcat Server will automatically unpack (unzip) the files in the WAR file.</span></span> <span data-ttu-id="cc9f0-380">Mimo że serwer Tomcat rozpoczyna się rozpakowanie niemal natychmiast, może trwać bardzo długo czas (prawdopodobnie godz. dla plików, które mają być widoczne w klient FTP).</span><span class="sxs-lookup"><span data-stu-id="cc9f0-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for the files to appear in the FTP client.</span></span>

#### <a name="run-the-hello-world-application-on-the-web-app"></a><span data-ttu-id="cc9f0-381">Uruchamianie aplikacji Hello World w aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="cc9f0-381">Run the Hello World application on the Web App</span></span>
1. <span data-ttu-id="cc9f0-382">Po przekazany plik WAR i zweryfikować, że serwer Tomcat utworzył rozpakowanego `JSPHello` katalogu, przejdź do `http://webdemowebapp.azurewebsites.net/JSPHello` do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-382">After you have uploaded the WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse to `http://webdemowebapp.azurewebsites.net/JSPHello` to run the application.</span></span>
   
   > <span data-ttu-id="cc9f0-383">**Uwaga:** kliknięcie **Przeglądaj** z klasycznego portalu można uzyskać domyślnej strony sieci Web, informujący o tym "tej aplikacji sieci web Java na podstawie został pomyślnie utworzony."</span><span class="sxs-lookup"><span data-stu-id="cc9f0-383">**Note:** If you click **Browse** from the classic portal, you might get the default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="cc9f0-384">Może być konieczne odświeżania strony sieci Web, aby wyświetlić dane wyjściowe aplikacji zamiast domyślnej strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-384">You might have to refresh the webpage in order to view the application output instead of the default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="cc9f0-385">Po uruchomieniu aplikacji, powinny być widoczne strony sieci web z następujących danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="cc9f0-385">When the application runs, you should see a web page with the following output:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="cc9f0-386">Oczyszczanie zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cc9f0-386">Clean up Azure resources</span></span>
<span data-ttu-id="cc9f0-387">Ta procedura powoduje utworzenie aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="cc9f0-388">Opłaty będą naliczane zasobu tak długo, jak istnieje.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-388">You will be billed for the resource as long as it exists.</span></span> <span data-ttu-id="cc9f0-389">Jeśli nie chcesz nadal używać do testowania lub rozwoju aplikacji sieci web, należy rozważyć zatrzymanie lub usunięcie go.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-389">Unless you plan to continue using the web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="cc9f0-390">Aplikacja sieci web, który został zatrzymany nadal spowoduje naliczenie opłaty mały, ale w dowolnym momencie można uruchomić go ponownie.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="cc9f0-391">Usunięcie aplikacji sieci web spowoduje usunięcie wszystkich danych, które zostały przekazane do niej.</span><span class="sxs-lookup"><span data-stu-id="cc9f0-391">Deleting a web app erases all data you have uploaded to it.</span></span>

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
