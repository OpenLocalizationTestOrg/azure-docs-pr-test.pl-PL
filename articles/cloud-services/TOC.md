# Omówienie
## [Co to jest Cloud Services?](cloud-services-choose-me.md)
## [Pliki konfiguracji usługi Cloud Service i tworzenie pakietów](cloud-services-model-and-package.md)

# Wprowadzenie
## [Przykładowa usługa Cloud Service — .NET](cloud-services-dotnet-get-started.md)
## [Przykładowy kod w języku Python dla usługi w chmurze w programie Visual Studio](cloud-services-python-ptvs.md)
## [Konfigurowanie hybrydowego klastra HPC za pomocą pakietu Microsoft HPC Pack](cloud-services-setup-hybrid-hpcpack-cluster.md)

# Instrukcje
## Planowanie
### [Rozmiary maszyn wirtualnych](cloud-services-sizes-specs.md)
### [Aktualizacje](cloud-services-update-azure-service.md)

## Programowanie
### [PHP — tworzenie roli Sieć Web i roli Proces roboczy](../cloud-services-php-create-web-role.md)
### [Tworzenie i wdrażanie aplikacji Node.js](cloud-services-nodejs-develop-deploy-app.md)
### [Tworzenie aplikacji sieci Web Node.js za pomocą usługi Express](cloud-services-nodejs-develop-deploy-express-app.md)
### Storage i Visual Studio
#### [Magazyn obiektów blob i połączone usługi](../visual-studio/vs-storage-cloud-services-getting-started-blobs.md)
#### [Magazyn kolejek i połączone usługi](../visual-studio/vs-storage-cloud-services-getting-started-queues.md)
#### [Magazyn tabel i połączone usługi](../visual-studio/vs-storage-cloud-services-getting-started-tables.md)
### Konfigurowanie pakietów dla kompilacji ciągłej i wdrażania
#### [TFS i Team Build](cloud-services-dotnet-continuous-delivery.md)
### [Konfigurowanie reguł ruchu dla roli](cloud-services-enable-communication-role-instances.md)
### [Obsługa zdarzeń cyklu życia usługi w chmurze](cloud-services-role-lifecycle-dotnet.md)
### [Biblioteka Socket.io (Node.js)](cloud-services-nodejs-chat-app-socketio.md)
### [Nawiązywanie połączenia telefonicznego za pomocą usługi Twilio (.NET)](../partner-twilio-cloud-services-dotnet-phone-call-web-role.md)
### [New Relic](../store-new-relic-cloud-services-dotnet-application-performance-management.md)

### Konfigurowanie zadań uruchamiania
#### [Tworzenie zadań uruchamiania](cloud-services-startup-tasks.md)
#### [Popularne zadania uruchamiania](cloud-services-startup-tasks-common.md)
#### [Instalowanie programu .NET w roli usługi w chmurze przy użyciu zadania](cloud-services-dotnet-install-dotnet.md)

### Konfigurowanie pulpitu zdalnego
#### [Portal](cloud-services-role-enable-remote-desktop-new-portal.md)
#### [Portal klasyczny](cloud-services-role-enable-remote-desktop.md)
#### [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)

## Wdrożenie
### Tworzenie i wdrażanie usługi w chmurze w portalu
#### [Portal](cloud-services-how-to-create-deploy-portal.md)
#### [Portal klasyczny](cloud-services-how-to-create-deploy.md)
### [Tworzenie pustego kontenera usługi w chmurze w programie PowerShell](cloud-services-powershell-create-cloud-container.md)
### Konfigurowanie niestandardowej nazwy domeny
#### [Portal](cloud-services-custom-domain-name-portal.md)
#### [Portal klasyczny](cloud-services-custom-domain-name.md)
### [Testowanie wdrażania usługi w chmurze (Node.js)](cloud-services-nodejs-stage-application.md)
### [Połączenie z niestandardowym kontrolerem domeny](cloud-services-connect-to-custom-domain.md)

## Zarządzanie usługą
### Typowe zadania zarządzania
#### [Portal](cloud-services-how-to-manage-portal.md)
#### [Portal klasyczny](cloud-services-how-to-manage.md)
### Konfigurowanie usługi w chmurze
#### [Portal](cloud-services-how-to-configure-portal.md)
#### [Portal klasyczny](cloud-services-how-to-configure.md)
### [Zarządzanie usługą w chmurze przy użyciu usługi Azure Automation](automation-manage-cloud-services.md)
### Konfigurowanie automatycznego skalowania
#### [Portal](cloud-services-how-to-scale-portal.md)
#### [Portal klasyczny](cloud-services-how-to-scale.md)
### [Zarządzanie zasobami platformy Azure przy użyciu języka Python](cloud-services-python-how-to-use-service-management.md)

### [Poprawki systemu operacyjnego gościa](cloud-services-guestos-msrc-releases.md)
### Wycofanie systemu operacyjnego gościa
#### [Zasady wycofywania](cloud-services-guestos-retirement-policy.md)
#### [Powiadomienie o wycofaniu rodziny 1](cloud-services-guestos-family1-retirement.md)
### [Informacje o nowych wersjach systemu operacyjnego gościa](cloud-services-guestos-update-matrix.md)
### [Konfiguracja roli usług Cloud Services (XPath) — ściągawka](cloud-services-role-config-xpath.md)

## Zarządzanie certyfikatami
### [Certyfikaty usług w chmurze i zarządzania](cloud-services-certs-create.md)
### Konfigurowanie protokołu SSL 
#### [Portal](cloud-services-configure-ssl-certificate-portal.md)
#### [Portal klasyczny](cloud-services-configure-ssl-certificate.md)

## Monitorowanie
### [Monitorowanie usługi w chmurze](cloud-services-how-to-monitor.md)
### [Testowanie wydajności](../vs-azure-tools-performance-profiling-cloud-services.md)
#### [Testowanie przy użyciu programu Visual Studio Profiler](cloud-services-performance-testing-visual-studio-profiler.md)
### Włączanie diagnostyki
#### [Program PowerShell](cloud-services-diagnostics-powershell.md)
#### [.NET](cloud-services-dotnet-diagnostics.md)
#### [Program Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
### [Używanie liczników wydajności w usłudze Diagnostyka Azure](cloud-services-dotnet-diagnostics-performance-counters.md)
### [Przechowywanie i przeglądanie danych diagnostycznych w usłudze Azure Storage](cloud-services-dotnet-diagnostics-storage.md)
### [Śledzenie usługi w chmurze przy użyciu usługi Diagnostyka](cloud-services-dotnet-diagnostics-trace-flow.md)
### [Wysyłanie danych diagnostycznych do usługi App Insights](cloud-services-dotnet-diagnostics-applicationinsights.md)

## Rozwiązywanie problemów
### Debugowanie 
#### [Włączanie debugowania zdalnego z dostarczaniem ciągłym](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md)
#### [Opcje dla usługi w chmurze](../vs-azure-tools-debugging-cloud-services-overview.md)
#### [Lokalna usługa w chmurze przy użyciu programu Visual Studio](../vs-azure-tools-debug-cloud-services-virtual-machines.md)
#### [Opublikowana usługa w chmurze przy użyciu programu Visual Studio](../vs-azure-tools-intellitrace-debug-published-cloud-services.md)
### [Niepowodzenie alokacji usługi w chmurze](cloud-services-allocation-failures.md)
### [Typowe przyczyny powtarzania cykli ról usługi w chmurze](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)
### [Domyślny rozmiar folderu TEMP jest zbyt mały dla roli](cloud-services-troubleshoot-default-temp-folder-size-too-small-web-worker-role.md)
### [Typowe problemy z wdrażaniem](cloud-services-troubleshoot-deployment-problems.md)
### [Nie można uruchomić roli](cloud-services-troubleshoot-roles-that-fail-start.md)
### [Wskazówki dotyczące odzyskiwania](cloud-services-disaster-recovery-guidance.md)
### Cloud Services — często zadawane pytania
#### [Często zadawane pytania dotyczące dostępności aplikacji i usług](cloud-services-application-and-service-availability-faq.md)
#### [Często zadawane pytania dotyczące konfiguracji i zarządzania](cloud-services-configuration-and-management-faq.md)
#### [Często zadawane pytania dotyczące łączności i sieci](cloud-services-connectivity-and-networking-faq.md)
#### [Często zadawane pytania dotyczące wdrażania](cloud-services-deployment-faq.md)

# Dokumentacja
## [Przykłady kodu](https://azure.microsoft.com/en-us/resources/samples/?service=cloud-services)
## [Schemat XML .csdef](https://msdn.microsoft.com/library/azure/ee758711)
## [Schemat XML .cscfg](https://msdn.microsoft.com/library/azure/ee758710)
## [REST](https://msdn.microsoft.com/library/azure/ee460812)

# Zasoby
## [Harmonogram działania dla platformy Azure](https://azure.microsoft.com/roadmap/?category=compute)
## [Ścieżka szkoleniowa](https://azure.microsoft.com/documentation/learning-paths/cloud-services/)
## [Forum MSDN](https://social.msdn.microsoft.com/Forums/en-us/home?forum=windowsazuredevelopment)
## [Cennik](https://azure.microsoft.com/pricing/details/cloud-services/)
## [Kalkulator cen](https://azure.microsoft.com/pricing/calculator/)
## [Aktualizacje usług](https://azure.microsoft.com/updates/?product=cloud-services&updatetype=&platform=)
## [Filmy wideo](https://azure.microsoft.com/documentation/videos/index/?services=cloud-services)
