$maxAge = $env:MaximumBackupAge
$VssMsSqlBackupPlugin = $env:VssMsSqlBackupPlugin
$VMWareBackupPlugin = $env:VMWareBackupPlugin
$SystemStateBackupPlugin = $env:SystemStateBackupPlugin
$FsBackupPlugin = $env:FsBackupPlugin

$VssMsSqlBackupPlugin = $true
$VMWareBackupPlugin  = $true
$SystemStateBackupPlugin = $true
$FsBackupPlugin = $true
$maxAge = 72

$currentDate = Get-Date
$maxBackupAge = $currentDate.AddHours(-$maxAge)

$xmlFileSession = "C:\ProgramData\MXB\Backup Manager\SessionReport.xml"
[xml]$backupSessions = Get-Content -Path $xmlFileSession

If (!$backupSessions)
{
    $xmlFileSession = "C:\ProgramData\Managed Online Backup\Backup Manager\SessionReport.xml"
    [xml]$backupSessions = Get-Content -Path $xmlFileSession
}

If (!$backupSessions)
{
    $Result = "SessionReport.xml not found"
    $Exitcode = 2
}

$Exitcode = $NULL
$resultDiagnostic = @()
$resultDisplay = @() 
$resultDisplay += "Result="

If ($VssMsSqlBackupPlugin -eq $true)
{
    $VssMsSqlBackup = $backupSessions.SessionStatistics.Session | Where {$_.Plugin -eq "VssMsSqlBackupPlugin"}  | Select -First 1
    $VssMsSqlBackupStartTime = $VssMsSqlBackup.StartTimeUTC
    $VssMsSqlBackupDate = [datetime]::ParseExact($VssMsSqlBackupStartTime, "yyyy-MM-dd HH:mm:ss", $null)
    $VssMsSqlBackupStatus = $VssMsSqlBackup.Status
    If ($VssMsSqlBackupDate -lt $maxBackupAge)
    {
        If ($VssMsSqlBackup -eq $NULL)
        {
            
        }
        Else 
        {
            $Exitcode = 1
            $resultDiagnostic += "Following Backup is older than $maxAge hours:"
        }
    }   
    Switch ($VssMsSqlBackup.Status)
    {
        "Completed" 
        {
        }    
        "InProcess"
        {
        }
        "CompletedWithErros"
        {
            $Exitcode = 2
        }
        "NotStarted"
        {
            $Exitcode = 3
        }
        "Aborted"
        {
            $Exitcode = 4
        }
        "Interrupted"
        {
            $Exitcode = 5
        }
        "Failed"
        {
            $Exitcode = 6
        }
        "Restarted"
        {
        }
        default
        {
            $VssMsSqlBackupStatus = "Not Set Up"
        }
    }
    $resultDisplay += "VssMsSqlBackup: $($VssMsSqlBackupStatus) - "
    $resultDiagnostic += "VssMsSqlBackup $($VssMsSqlBackup.Status)"
    $resultDiagnostic += $VssMsSqlBackupDate
    $resultDiagnostic += $VssMsSqlBackupStatus
    $resultDiagnostic += "---"
}

If ($VMWareBackupPlugin -eq $true)
{
    $VMWareBackup = $backupSessions.SessionStatistics.Session | Where {$_.Plugin -eq "VMWareBackupPlugin"}  | Select -First 1
    $VMWareBackupStartTime = $VMWareBackup.StartTimeUTC
    $VMWareBackupDate = [datetime]::ParseExact($VMWareBackupStartTime, "yyyy-MM-dd HH:mm:ss", $null)
    $VMWareBackupStatus = $VMWareBackup.Status
    If ($VMWareBackupDate -lt $maxBackupAge)
    {
        If ($VMWareBackup -eq $NULL)
        {
            
        }
        Else 
        {
            $Exitcode = 1
            $resultDiagnostic += "Following Backup is older than $maxAge hours:"
        }
    }  
    Switch ($VMWareBackup.Status)
    {
        "Completed" 
        {
        }    
        "InProcess"
        {
        }
        "CompletedWithErrors"
        {
            $Exitcode = 2
        }
        "NotStarted"
        {
            $Exitcode = 3
        }
        "Aborted"
        {
            $Exitcode = 4
        }
        "Interrupted"
        {
            $Exitcode = 5
        }
        "Failed"
        {
            $Exitcode = 6
        }
        "Restarted"
        {
        }
        default
        {
            $VMWareBackupStatus = "Not Set Up"
        }
    }
    $resultDisplay += "VMWareBackup: $($VMWareBackupStatus) - "
    $resultDiagnostic += "VMWareBackup"
    $resultDiagnostic += $VMWareBackupDate
    $resultDiagnostic += $VMWareBackupStatus
    $resultDiagnostic += "---"
} 


If ($SystemStateBackupPlugin -eq $true)
{
    $SystemStateBackup = $backupSessions.SessionStatistics.Session | Where {$_.Plugin -eq "SystemStateBackupPlugin"}  | Select -First 1
    $SystemStateBackupStartTime = $SystemStateBackup.StartTimeUTC
    $SystemStateBackupDate = [datetime]::ParseExact($SystemStateBackupStartTime, "yyyy-MM-dd HH:mm:ss", $null)
    $SystemStateBackupStatus = $SystemStateBackup.Status
    If ($SystemStateBackupDate -lt $maxBackupAge)
    {
        If ($SystemStateBackup -eq $NULL)
        {
            
        }
        Else 
        {
            $Exitcode = 1
            $resultDiagnostic += "Following Backup is older than $maxAge hours:"
        }
    }  
    Switch ($SystemStateBackup.Status)
    {
        "Completed" 
        {
        }    
        "InProcess"
        {
        }
        "CompletedWithErrors"
        {
            $Exitcode = 2
        }
        "NotStarted"
        {
            $Exitcode = 3
        }
        "Aborted"
        {
            $Exitcode = 4
        }
        "Interrupted"
        {
            $Exitcode = 5
        }
        "Failed"
        {
            $Exitcode = 6
        }
        "Restarted"
        {
        }
        default
        {
            $SystemStateBackupStatus = "Not Set Up"
        }
    }
    $resultDisplay += "SystemStateBackup: $($SystemStateBackupStatus) - "
    $resultDiagnostic += "SystemStateBackup"
    $resultDiagnostic += $SystemStateBackupDate
    $resultDiagnostic += $SystemStateBackupStatus
    $resultDiagnostic += "---"
} 

If ($FsBackupPlugin -eq $true)
{
    $FsBackup = $backupSessions.SessionStatistics.Session | Where {$_.Plugin -eq "FsBackupPlugin"}  | Select -First 1
    $FsBackupStartTime = $FsBackup.StartTimeUTC
    $FsBackupDate = [datetime]::ParseExact($FsBackupStartTime, "yyyy-MM-dd HH:mm:ss", $null)
    $FsBackupStatus = $FsBackup.Status
    If ($FsBackupDate -lt $maxBackupAge)
    {
        If ($FsBackup -eq $NULL)
        {
            
        }
        Else 
        {
            $Exitcode = 1
            $resultDiagnostic += "Following Backup is older than $maxAge hours:"
        }
    }  
    Switch ($FsBackup.Status)
    {
        "Completed" 
        {
        }    
        "InProcess"
        {
        }
        "CompletedWithErrors"
        {
            $Exitcode = 2
        }
        "NotStarted"
        {
            $Exitcode = 3
        }
        "Aborted"
        {
            $Exitcode = 4
        }
        "Interrupted"
        {
            $Exitcode = 5
        }
        "Failed"
        {
            $Exitcode = 6
        }
        "Restarted"
        {
        }
        default
        {
            $FsBackupStatus = "Not Set Up"
        }
    }
    $resultDisplay += "FsBackup: $($FsBackupStatus)"
    $resultDiagnostic += "FsBackup"
    $resultDiagnostic += $FsBackupDate
    $resultDiagnostic += $FsBackupStatus
    $resultDiagnostic += "---"
} 

Write-Host "<-Start Result->"
$resultDisplay -join '';
Write-Host "<-End Result->"

Write-Host "<-Start Diagnostic->"
$resultDiagnostic
Write-Host "<-End Diagnostic->"

Exit $Exitcode
