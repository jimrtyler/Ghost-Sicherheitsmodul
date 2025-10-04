# 👻 Ghost Sicherheitsmodul
**PowerShell-basiertes Windows & Azure Sicherheitshärtung-Tool**

> **Proaktive Sicherheitshärtung für Windows-Endpunkte und Azure-Umgebungen.** Ghost bietet PowerShell-basierte Härtungsfunktionen, die helfen können, häufige Angriffsvektoren zu reduzieren, indem unnötige Dienste und Protokolle deaktiviert werden.

## ⚠️ Wichtige Haftungsausschlüsse

**TESTS ERFORDERLICH**: Testen Sie Ghost immer zuerst in Nicht-Produktionsumgebungen. Das Deaktivieren von Diensten kann legitime Geschäftsfunktionen beeinträchtigen.

**KEINE GARANTIEN**: Obwohl Ghost auf häufige Angriffsvektoren abzielt, kann kein Sicherheitstool alle Angriffe verhindern. Dies ist eine Komponente einer umfassenden Sicherheitsstrategie.

**BETRIEBSAUSWIRKUNGEN**: Einige Funktionen können die Systemfunktionalität beeinträchtigen. Überprüfen Sie jede Einstellung sorgfältig vor der Bereitstellung.

**PROFESSIONELLE BEWERTUNG**: Für Produktionsumgebungen konsultieren Sie Sicherheitsexperten, um sicherzustellen, dass die Einstellungen den Anforderungen Ihrer Organisation entsprechen.

## 📊 Die Sicherheitslandschaft

Ransomware-Schäden erreichten **57 Milliarden Dollar im Jahr 2025**, und Forschungen zeigen, dass viele erfolgreiche Angriffe grundlegende Windows-Dienste und Fehlkonfigurationen ausnutzen. Häufige Angriffsvektoren umfassen:

- **90% der Ransomware-Vorfälle** beinhalten RDP-Exploitation
- **SMBv1-Schwachstellen** ermöglichten Angriffe wie WannaCry und NotPetya
- **Dokumentmakros** bleiben eine primäre Malware-Übertragungsmethode
- **USB-basierte Angriffe** zielen weiterhin auf luftisolierte Netzwerke ab
- **PowerShell-Missbrauch** ist in den letzten Jahren erheblich gestiegen

## 🛡️ Ghost Sicherheitsfunktionen

Ghost bietet **16 Windows-Härtungsfunktionen** plus **Azure-Sicherheitsintegration**:

### Windows-Endpunkt-Härtung

| Funktion | Zweck | Überlegungen |
|----------|-------|--------------|
| `Set-RDP` | Verwaltet Remote Desktop-Zugriff | Kann Remote-Administration beeinträchtigen |
| `Set-SMBv1` | Steuert Legacy-SMB-Protokoll | Erforderlich für sehr alte Systeme |
| `Set-AutoRun` | Steuert AutoPlay/AutoRun | Kann Benutzerkomfort beeinträchtigen |
| `Set-USBStorage` | Beschränkt USB-Speichergeräte | Kann legitime USB-Nutzung beeinträchtigen |
| `Set-Macros` | Steuert Office-Makro-Ausführung | Kann makro-aktivierte Dokumente beeinträchtigen |
| `Set-PSRemoting` | Verwaltet PowerShell-Remoting | Kann Remote-Verwaltung beeinträchtigen |
| `Set-WinRM` | Steuert Windows Remote Management | Kann Remote-Administration beeinträchtigen |
| `Set-LLMNR` | Verwaltet Namensauflösungsprotokoll | Normalerweise sicher zu deaktivieren |
| `Set-NetBIOS` | Steuert NetBIOS über TCP/IP | Kann Legacy-Anwendungen beeinträchtigen |
| `Set-AdminShares` | Verwaltet administrative Freigaben | Kann Remote-Dateizugriff beeinträchtigen |
| `Set-Telemetry` | Steuert Datensammlung | Kann Diagnosefähigkeiten beeinträchtigen |
| `Set-GuestAccount` | Verwaltet Gastkonto | Normalerweise sicher zu deaktivieren |
| `Set-ICMP` | Steuert Ping-Antworten | Kann Netzwerkdiagnose beeinträchtigen |
| `Set-RemoteAssistance` | Verwaltet Remoteunterstützung | Kann Helpdesk-Operationen beeinträchtigen |
| `Set-NetworkDiscovery` | Steuert Netzwerkerkennung | Kann Netzwerkbrowsing beeinträchtigen |
| `Set-Firewall` | Verwaltet Windows-Firewall | Kritisch für Netzwerksicherheit |

### Azure Cloud-Sicherheit

| Funktion | Zweck | Anforderungen |
|----------|-------|---------------|
| `Set-AzureSecurityDefaults` | Aktiviert grundlegende Azure AD-Sicherheit | Microsoft Graph-Berechtigungen |
| `Set-AzureConditionalAccess` | Konfiguriert Zugriffsrichtlinien | Azure AD P1/P2-Lizenzen |
| `Set-AzurePrivilegedUsers` | Auditiert privilegierte Konten | Globale Administrator-Berechtigungen |

### Unternehmens-Bereitstellungsoptionen

| Methode | Anwendungsfall | Anforderungen |
|---------|----------------|---------------|
| **Direkte Ausführung** | Tests, kleine Umgebungen | Lokale Administratorrechte |
| **Group Policy** | Domänenumgebungen | Domänenadministrator, GP-Verwaltung |
| **Microsoft Intune** | Cloud-verwaltete Geräte | Intune-Lizenzen, Graph API |

## 🚀 Schnellstart

### Sicherheitsbewertung
```powershell
# Ghost-Modul laden
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')

# Aktuelle Sicherheitslage überprüfen
Get-Ghost
```

### Grundlegende Härtung (Erst testen)
```powershell
# Wesentliche Härtung - erst in Laborumgebung testen
Set-Ghost -SMBv1 -AutoRun -Macros

# Änderungen überprüfen
Get-Ghost
```

### Unternehmensbereitstellung
```powershell
# Group Policy-Bereitstellung (Domänenumgebungen)
Set-Ghost -SMBv1 -AutoRun -GroupPolicy

# Intune-Bereitstellung (cloud-verwaltete Geräte)
Set-Ghost -SMBv1 -RDP -USBStorage -Intune
```

## 📋 Installationsmethoden

### Option 1: Direkter Download (Tests)
```powershell
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')
```

### Option 2: Modulinstallation
```powershell
# Installation aus PowerShell Gallery (wenn verfügbar)
Install-Module Ghost -Scope CurrentUser
Import-Module Ghost
```

### Option 3: Unternehmensbereitstellung
```powershell
# Kopieren an Netzwerkstandort für Group Policy-Bereitstellung
# Intune PowerShell-Skripte für Cloud-Bereitstellung konfigurieren
```

## 💼 Anwendungsfall-Beispiele

### Kleines Unternehmen
```powershell
# Grundschutz mit minimaler Auswirkung
Set-Ghost -SMBv1 -AutoRun -Macros -ICMP
```

### Gesundheitswesen
```powershell
# HIPAA-fokussierte Härtung
Set-Ghost -SMBv1 -RDP -USBStorage -AdminShares -Telemetry
```

### Finanzdienstleistungen
```powershell
# Hochsicherheitskonfiguration
Set-Ghost -RDP -SMBv1 -AutoRun -USBStorage -Macros -PSRemoting -AdminShares
```

### Cloud-First Organisation
```powershell
# Intune-verwaltete Bereitstellung
Connect-IntuneGhost -Interactive
Set-Ghost -SMBv1 -RDP -AutoRun -Macros -Intune
```

## 📝 Funktionsdetails

### Kern-Härtungsfunktionen

#### Netzwerkdienste
- **RDP**: Blockiert Remote Desktop-Zugriff oder randomisiert Port
- **SMBv1**: Deaktiviert Legacy-Dateifreigabeprotokoll
- **ICMP**: Verhindert Ping-Antworten für Aufklärung
- **LLMNR/NetBIOS**: Blockiert Legacy-Namensauflösungsprotokolle

#### Anwendungssicherheit
- **Makros**: Deaktiviert Makroausführung in Office-Anwendungen
- **AutoRun**: Verhindert automatische Ausführung von Wechselmedien

#### Remote-Verwaltung
- **PSRemoting**: Deaktiviert PowerShell-Remote-Sitzungen
- **WinRM**: Stoppt Windows Remote Management
- **Remoteunterstützung**: Blockiert Remoteunterstützungsverbindungen

#### Zugriffskontrolle
- **Admin-Freigaben**: Deaktiviert C$, ADMIN$-Freigaben
- **Gastkonto**: Deaktiviert Gastkonto-Zugriff
- **USB-Speicher**: Beschränkt USB-Gerätenutzung

### Azure-Integration
```powershell
# Mit Azure-Mandant verbinden
Connect-AzureGhost -Interactive

# Sicherheitsstandards aktivieren
Set-AzureSecurityDefaults -Enable

# Bedingten Zugriff konfigurieren
Set-AzureConditionalAccess -BlockLegacyAuth -RequireMFA

# Privilegierte Benutzer auditieren
Set-AzurePrivilegedUsers -AuditOnly
```

### Intune-Integration (Neu in v2)
```powershell
# Mit Intune verbinden
Connect-IntuneGhost -Interactive

# Über Intune-Richtlinien bereitstellen
Set-IntuneGhost -Settings @{
    RDP = $true
    SMBv1 = $true
    USBStorage = $true
    Macros = $true
}
```

## ⚠️ Wichtige Überlegungen

### Testanforderungen
- **Laborumgebung**: Alle Einstellungen zuerst in isolierter Umgebung testen
- **Phasenweise Bereitstellung**: Schrittweise ausrollen, um Probleme zu identifizieren
- **Rollback-Plan**: Sicherstellen, dass Änderungen bei Bedarf rückgängig gemacht werden können
- **Dokumentation**: Aufzeichnen, welche Einstellungen für Ihre Umgebung funktionieren

### Potentielle Auswirkungen
- **Benutzerproduktivität**: Einige Einstellungen können tägliche Arbeitsabläufe beeinträchtigen
- **Legacy-Anwendungen**: Ältere Systeme benötigen möglicherweise bestimmte Protokolle
- **Remote-Zugriff**: Auswirkungen auf legitime Remote-Administration berücksichtigen
- **Geschäftsprozesse**: Überprüfen, dass Einstellungen kritische Funktionen nicht beeinträchtigen

### Sicherheitsbeschränkungen
- **Defense in Depth**: Ghost ist eine Sicherheitsschicht, keine vollständige Lösung
- **Kontinuierliche Verwaltung**: Sicherheit erfordert kontinuierliche Überwachung und Updates
- **Benutzerschulung**: Technische Kontrollen müssen mit Sicherheitsbewusstsein gepaart werden
- **Bedrohungsevolution**: Neue Angriffsmethoden können aktuelle Schutzmaßnahmen umgehen

## 🎯 Beispiel-Angriffsszenarien

Obwohl Ghost auf häufige Angriffsvektoren abzielt, hängt die spezifische Prävention von ordnungsgemäßer Implementierung und Tests ab:

### WannaCry-ähnliche Angriffe
- **Eindämmung**: `Set-Ghost -SMBv1` deaktiviert das anfällige Protokoll
- **Überlegung**: Sicherstellen, dass keine Legacy-Systeme SMBv1 benötigen

### RDP-basierte Ransomware
- **Eindämmung**: `Set-Ghost -RDP` blockiert Remote Desktop-Zugriff
- **Überlegung**: Könnte alternative Remote-Zugriffsmethoden erfordern

### Dokumentbasierte Malware
- **Eindämmung**: `Set-Ghost -Macros` deaktiviert Makroausführung
- **Überlegung**: Könnte legitime makro-aktivierte Dokumente beeinträchtigen

### USB-übertragene Bedrohungen
- **Eindämmung**: `Set-Ghost -USBStorage -AutoRun` beschränkt USB-Funktionalität
- **Überlegung**: Könnte legitime USB-Gerätenutzung beeinträchtigen

## 🏢 Unternehmensfunktionen

### Group Policy-Unterstützung
```powershell
# Einstellungen über Group Policy-Registry anwenden
Set-Ghost -SMBv1 -RDP -AutoRun -GroupPolicy

# Einstellungen werden domänenweit nach GP-Aktualisierung angewendet
gpupdate /force
```

### Microsoft Intune-Integration
```powershell
# Intune-Richtlinien für Ghost-Einstellungen erstellen
Set-IntuneGhost -Settings $GhostSettings -Interactive

# Richtlinien werden automatisch auf verwaltete Geräte bereitgestellt
```

### Compliance-Berichterstattung
```powershell
# Sicherheitsbewertungsbericht generieren
Get-Ghost | Export-Csv -Path "SicherheitsAudit-$(Get-Date -Format 'yyyy-MM-dd').csv"

# Azure-Sicherheitslage-Bericht
Get-AzureGhost | Out-File "AzureSicherheitsBericht.txt"
```

## 📚 Best Practices

### Vor der Bereitstellung
1. **Aktuellen Zustand dokumentieren**: `Get-Ghost` vor Änderungen ausführen
2. **Gründlich testen**: In Nicht-Produktionsumgebung validieren
3. **Rollback planen**: Wissen, wie jede Einstellung rückgängig gemacht wird
4. **Stakeholder-Review**: Sicherstellen, dass Geschäftsbereiche Änderungen genehmigen

### Während der Bereitstellung
1. **Phasenweiser Ansatz**: Zuerst in Pilotgruppen bereitstellen
2. **Auswirkungen überwachen**: Auf Benutzerbeschwerden oder Systemprobleme achten
3. **Probleme dokumentieren**: Alle Probleme für zukünftige Referenz aufzeichnen
4. **Änderungen kommunizieren**: Benutzer über Sicherheitsverbesserungen informieren

### Nach der Bereitstellung
1. **Regelmäßige Bewertung**: `Get-Ghost` regelmäßig ausführen, um Einstellungen zu überprüfen
2. **Dokumentation aktualisieren**: Sicherheitskonfigurationen aktuell halten
3. **Wirksamkeit bewerten**: Auf Sicherheitsvorfälle überwachen
4. **Kontinuierliche Verbesserung**: Einstellungen basierend auf Bedrohungslandschaft anpassen

## 🔧 Fehlerbehebung

### Häufige Probleme
- **Berechtigungsfehler**: Sicherstellen, dass PowerShell-Sitzung erhöht ist
- **Dienstabhängigkeiten**: Einige Dienste können Abhängigkeiten haben
- **Anwendungskompatibilität**: Mit Geschäftsanwendungen testen
- **Netzwerkkonnektivität**: Überprüfen, dass Remote-Zugriff noch funktioniert

### Wiederherstellungsoptionen
```powershell
# Spezifische Dienste bei Bedarf wieder aktivieren
Set-RDP -Enable
Set-SMBv1 -Enable
Set-AutoRun -Enable
Set-Macros -Enable
```

## 👨‍💻 Über den Autor

**Jim Tyler** - Microsoft MVP für PowerShell
- **YouTube**: [@PowerShellEngineer](https://youtube.com/@PowerShellEngineer) (10.000+ Abonnenten)
- **Newsletter**: [PowerShell.News](https://powershell.news) - Wöchentliche Sicherheits-Intelligence
- **Autor**: "PowerShell for Systems Engineers"
- **Erfahrung**: Jahrzehnte PowerShell-Automatisierung und Windows-Sicherheit

## 📄 Lizenz & Haftungsausschluss

### MIT-Lizenz
Ghost wird unter der MIT-Lizenz für freie Nutzung, Modifikation und Verteilung bereitgestellt.

### Sicherheits-Haftungsausschluss
- **Keine Gewährleistung**: Ghost wird "wie besehen" ohne jegliche Gewährleistung bereitgestellt
- **Tests erforderlich**: Immer zuerst in Nicht-Produktionsumgebungen testen
- **Professionelle Beratung**: Sicherheitsexperten für Produktionsbereitstellungen konsultieren
- **Betriebsauswirkungen**: Die Autoren sind nicht verantwortlich für betriebliche Störungen
- **Umfassende Sicherheit**: Ghost ist eine Komponente einer vollständigen Sicherheitsstrategie

### Support
- **GitHub Issues**: [Bugs melden oder Features anfordern](https://github.com/jimrtyler/Ghost/issues)
- **Dokumentation**: `Get-Help <Funktion> -Full` für detaillierte Hilfe verwenden
- **Community**: PowerShell- und Sicherheits-Community-Foren

---

**🔒 Stärken Sie Ihre Sicherheitslage mit Ghost - aber testen Sie immer zuerst.**

```powershell
# Beginnen Sie mit Bewertung, nicht mit Annahmen
Get-Ghost
```

**⭐ Geben Sie diesem Repository einen Stern, wenn Ghost hilft, Ihre Sicherheitslage zu verbessern!**