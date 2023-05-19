$os = Get-CimInstance Win32_OperatingSystem
Write-Host "Operating system: $($os.Caption) $($os.Version)"
$processor = Get-CimInstance Win32_Processor
Write-Host "Processor: $($processor.Name) $($processor.NumberOfCores) cores"

$memory = Get-CimInstance Win32_PhysicalMemory | Measure-Object -Property Capacity -Sum
Write-Host "Memory: $([math]::Round($memory.Sum / 1GB, 2)) GB"

$disk = Get-CimInstance Win32_DiskDrive | Measure-Object -Property Size -Sum
Write-Host "Disk: $([math]::Round($disk.Sum / 1TB, 2)) TB"

$display = Get-CimInstance Win32_VideoController
Write-Host "Display adapter: $($display.Name)"

$network = Get-CimInstance Win32_NetworkAdapterConfiguration | Where-Object { $_.IPAddress -ne $null }
foreach ($adapter in $network) {
    Write-Host "Network adapter: $($adapter.Description)"
    Write-Host "IP address: $($adapter.IPAddress[0])"
}

# Installed software
$software = Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName
Write-Host "Installed software:"
foreach ($app in $software) {
    Write-Host "- $($app.DisplayName)"
}
