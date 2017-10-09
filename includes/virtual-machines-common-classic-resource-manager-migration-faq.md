# <a name="frequently-asked-questions-about-classic-tooazure-resource-manager-migration"></a>Często zadawane pytania dotyczące klasycznego tooAzure migracji Menedżera zasobów

## <a name="does-this-migration-plan-affect-any-of-my-existing-services-or-applications-that-run-on-azure-virtual-machines"></a>Czy ten plan migracji wpływa na moje istniejące usługi lub aplikacje uruchomione na maszynach wirtualnych platformy Azure? 

Nie. maszyny wirtualne Hello (klasyczne) są pełni obsługiwane usługi w ogólnodostępnej. Można kontynuować toouse tooexpand tych zasobów użytkownika została zrozumiana. dzięki w systemie Microsoft Azure.

## <a name="what-happens-toomy-vms-if-i-dont-plan-on-migrating-in-hello-near-future"></a>Co się stanie toomy maszyn wirtualnych, jeśli nie należy zaplanować na temat przeprowadzania migracji w hello Najbliższa przyszłość? 

Firma Microsoft nie są wycofano hello istniejących interfejsów API i zasobów modelu klasycznego. Chcemy migracji toomake łatwe, biorąc pod uwagę hello zaawansowane funkcje, które są dostępne w modelu wdrażania usługi Resource Manager hello. Zdecydowanie zaleca się przejrzenie [niektóre korzyści hello](../articles/azure-resource-manager/resource-manager-deployment-model.md) które są częścią IaaS w obszarze usługi Resource Manager.

## <a name="what-does-this-migration-plan-mean-for-my-existing-tooling"></a>Co oznacza ten plan migracji dla moich istniejących narzędzi? 

Aktualizowanie modelu wdrażania usługi Resource Manager toohello narzędzi jest jednym z najważniejszych zmian hello, jakie ma tooaccount dla planów migracji.

## <a name="how-long-will-hello-management-plane-downtime-be"></a>Czas przestoju płaszczyzny zarządzania hello będzie? 

To zależy od hello liczby zasobów, które są migrowane. W przypadku wdrożeń mniejszych (dziesiątki kilka maszyn wirtualnych) migracji całej hello powinny zająć mniej niż godzinę. W przypadku wdrożeń na dużą skalę (setki maszyn wirtualnych) hello migracja może zająć kilka godzin.

## <a name="can-i-roll-back-after-my-migrating-resources-are-committed-in-resource-manager"></a>Czy mogę wykonać wycofanie po zatwierdzeniu migrowanych zasobów w usłudze Resource Manager? 

Migracja może przerwać tak długo, jak zasoby hello są hello przygotowane stanu. Wycofanie nie jest obsługiwana po hello zasoby zostały pomyślnie zmigrowane za pośrednictwem operacji przekazywania hello.

## <a name="can-i-roll-back-my-migration-if-hello-commit-operation-fails"></a>I wycofać Moje migracji w przypadku niepowodzenia operacji przekazywania hello? 

Nie można przerwać migracji, jeśli operacja przekazywania hello nie powiedzie się. Wszystkimi operacjami migracji, w tym hello operacji przekazywania, są idempotentności. Dlatego zaleca się, ponów próbę wykonania operacji powitania po pewnym czasie. Jeśli nadal czoła błąd, Utwórz bilet pomocy technicznej lub Utwórz wpis na forum o hello ClassicIaaSMigration tagu na naszych [forum wirtualna](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).

## <a name="do-i-have-toobuy-another-express-route-circuit-if-i-have-toouse-iaas-under-resource-manager"></a>Należy toobuy innego obwodu usługi express route posiadający toouse IaaS w obszarze usługi Resource Manager? 

Nie. Ostatnio włączone [przenoszenie obwody usługi ExpressRoute z modelu wdrażania Menedżera zasobów klasycznych toohello hello](../articles/expressroute/expressroute-move.md). Nie masz toobuy nowego obwodu ExpressRoute Jeśli już istnieje.

## <a name="what-if-i-had-configured-role-based-access-control-policies-for-my-classic-iaas-resources"></a>Co stanie się, jeśli mam skonfigurowane zasady kontroli dostępu opartej na rolach dla moich klasycznych zasobów IaaS? 

Podczas migracji zasobów hello przekształcenia z klasycznym tooResource Manager. Dlatego zaleca się zaplanowanie hello RBAC zasad aktualizacji, które wymagają toohappen po migracji.

## <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Mam utworzone kopie zapasowe moich klasycznych maszyn wirtualnych w magazynie usługi Backup. Można I migracji maszyn wirtualnych z trybu klasycznego tooResource menedżera trybu i chronić je w magazynie usług odzyskiwania? 

Klasycznym punktów odzyskiwania maszyny Wirtualnej w magazynie kopii zapasowych nie automatycznie zostanie przeprowadzona migracja magazynu usług odzyskiwania tooa po przeniesieniu hello maszyny Wirtualnej z tooResource klasycznym trybie menedżera. Wykonaj te kroki tootransfer kopii zapasowych maszyny Wirtualnej:

1. W magazynie kopii zapasowych hello, przejdź do pozycji toohello **chronione elementy** i wybierz hello maszyny Wirtualnej. Kliknij pozycję [Zatrzymaj ochronę](../articles/backup/backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Pozostaw opcję *Usuń powiązane dane kopii zapasowych* **niezaznaczoną**.
2. Usuń rozszerzenie kopii zapasowej/migawki hello z hello maszyny Wirtualnej.
3. Migruj maszynę wirtualną hello z trybu Menedżera tooResource trybu klasycznego. Upewnij się, że hello magazynu i sieci jest również odpowiedniego maszyny wirtualnej toohello poddane migracji informacje o trybie Menedżera tooResource.
4. Tworzenie magazynu usług odzyskiwania i konfigurowanie tworzenia kopii zapasowej na powitania migracji maszyny wirtualnej przy użyciu **kopii zapasowej** akcji na pulpicie nawigacyjnym magazynu. Szczegółowe informacje na temat tworzenia kopii zapasowej usług odzyskiwania maszyny Wirtualnej tooa magazynu, zobacz artykuł hello [ochrony maszyn wirtualnych platformy Azure w magazynie usług odzyskiwania](../articles/backup/backup-azure-vms-first-look-arm.md).

## <a name="can-i-validate-my-subscription-or-resources-toosee-if-theyre-capable-of-migration"></a>Można sprawdzania poprawności Mój toosee zasobów lub subskrypcji, gdy są one w stanie migracji? 

Tak. W przypadku opcji migracji z obsługiwanych platform hello hello pierwszym etapem przygotowania do migracji jest toovalidate czy hello zasoby są w stanie migracji. W przypadku, gdy hello zweryfikować operacja kończy się niepowodzeniem, komunikaty wszystkich powodów hello, którego nie można ukończyć powitalnych migracji.

## <a name="what-happens-if-i-run-into-a-quota-error-while-preparing-hello-iaas-resources-for-migration"></a>Co się stanie, jeśli podczas przygotowania do migracji zasobów IaaS hello błąd przydziału Uruchom? 

Zalecamy przerwać migracji, a następnie zaloguj się obsługa żądania tooincrease hello przydziały hello regionie hello Migrowanie maszyn wirtualnych. Po zatwierdzeniu żądania limitu przydziału hello można rozpocząć wykonywania kroków migracji hello ponownie.

## <a name="how-do-i-report-an-issue"></a>Jak mogę zgłosić problem? 

Problemów i pytania dotyczące migracji tooour [forum wirtualna](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows), ze słowem kluczowym hello ClassicIaaSMigration. Zalecamy publikowanie wszystkich pytań na tym forum. Jeśli masz umowy pomocy technicznej możesz powitalnej toolog również biletu pomocy technicznej.

## <a name="what-if-i-dont-like-hello-names-of-hello-resources-that-hello-platform-chose-during-migration"></a>Co zrobić, jeśli nie podoba hello nazw hello zasobów, które hello platformy nieinstalowanie podczas migracji? 

Wszystkie zasoby hello, które jawnie nadać nazwy w hello klasycznego modelu wdrażania są zachowywane podczas migracji. W niektórych przypadkach zostaną utworzone nowe zasoby. Na przykład dla każdej maszyny wirtualnej zostanie utworzony interfejs sieciowy. Obecnie nie obsługujemy hello możliwości toocontrol hello nazwy tych nowych zasobów utworzony podczas migracji. Logowania z głosów dla tej funkcji na powitania [forum opinii Azure](http://feedback.azure.com).

## <a name="can-i-migrate-expressroute-circuits-used-across-subscriptions-with-authorization-links"></a>Czy mogę zmigrować obwody usługi ExpressRoute używane w subskrypcjach wraz z łączami autoryzacji? 

Obwodów usługi ExpressRoute używających łącz autoryzacji między subskrypcjami nie można zmigrować automatycznie bez przestoju. Udostępniamy przewodnik z opisem wykonywania takiej migracji ręcznie. Zobacz [ExpressRoute migracji obwody i skojarzone sieci wirtualne od modelu wdrażania Menedżera zasobów klasycznych toohello hello](../articles/expressroute/expressroute-migration-classic-resource-manager.md) kroki i dodatkowe informacje.

## <a name="i-got-a-message-vm-is-reporting-hello-overall-agent-status-as-not-ready-hence-hello-vm-cannot-be-migrated-ensure-that-hello-vm-agent-is-reporting-overall-agent-status-as-ready-or-vm-contains-extension-whose-status-is-not-being-reported-from-hello-vm-hence-this-vm-cannot-be-migrated-"></a>Otrzymano komunikat *"maszyny Wirtualnej jest raportowania hello ogólny stan agenta jako nie jest gotowy. W związku z tym nie można migrować hello maszyny Wirtualnej. Upewnij się, że hello agenta maszyny Wirtualnej jest raportowania ogólny stan agenta jako gotowy"* lub *"maszyny Wirtualnej zawiera rozszerzenia, których stan nie jest raportowany przez hello maszyny Wirtualnej. Hence, the VM cannot be migrated”. (Maszyna wirtualna zawiera rozszerzenie, którego stan nie jest raportowany z maszyny wirtualnej. Dlatego nie można zmigrować tej maszyny wirtualnej). *

Ta wiadomość zostanie odebrana, gdy hello maszyna wirtualna ma łączność wychodząca toohello internet. agent maszyny Wirtualnej Hello używa kontem magazynu platformy Azure hello tooreach łączność wychodząca aktualizowania stanu agenta hello co pięć minut.
