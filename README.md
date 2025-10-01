# 👩‍💻 Yael Solan

## 💼 Über mich 🇩🇪  
Ich bin Yael – eine engagierte IT-Fachkraft mit Erfahrung im technischen Support, Systemadministration und digitaler Kundenbetreuung.  
Ich lebe in Deutschland, spreche fließend Deutsch (telc B2 Zertifikat) und besuche aktuell einen C1-Kurs. Ich verfüge über einen akademischen Hintergrund sowie fundierte praktische Kenntnisse in der IT.  

Durch meine bisherigen Tätigkeiten in internationalen Unternehmen konnte ich vielseitige IT-Prozesse kennenlernen und eigene Automatisierungslösungen umsetzen.  
Ich arbeite gern strukturiert, lösungsorientiert und bin motiviert, mich kontinuierlich weiterzuentwickeln – insbesondere im Bereich Software, Service & Support.  

## 💼 About me 🇬🇧  
I'm Yael – a dedicated IT professional with hands-on experience in technical support, system administration, and digital customer service.  
I live in Germany, speak fluent German (telc B2 certificate) and am currently enrolled in a C1 course. I bring both an academic background and practical skills in the IT field.  

In previous roles at international companies, I gained insight into diverse IT workflows and developed custom automation tools.  
I enjoy working in a structured and solution-driven way and am motivated to grow further – especially in software, service, and support roles.

## 📬 Kontakt & Links  
🔗 [LinkedIn-Profil](https://www.linkedin.com/in/yaelsolan/)  
📬 yaelsolan5@gmail.com  
🌍 [Portfolio](https://yaelsolan.github.io)

Vielen Dank fürs Vorbeischauen! 😊  
Thanks for stopping by! 🙏  
----
PowerShell
1- 

#Automation to change user permissions due to job and department moving
Import-Module ActiveDirectory

#Deleting existing permissions (AD groups)

$x = Read-Host "Enter the username who needs to change permissions: "

try{
Get-ADUser -Identity $x

$ADgroups = Get-ADPrincipalGroupMembership -Identity $x | where {$_.Name -ne "Domain Users"}

Write-Host "The user $x is a member of the following groups: "
$ADgroups | select name  

if ($ADgroups -ne $null){
Remove-ADPrincipalGroupMembership -Identity $x -MemberOf $ADgroups
}
}

catch{
Write-Host "$x Is Not exist"
}

#Copy New Permissions From another User

$UserExist = Read-Host "copy permission from: "

Get-ADUser -Identity $UserExist -Properties memberof |
Select-Object -ExpandProperty memberof |
Add-ADGroupMember -Members $x

#change Department name

Get-ADUser $x -Properties * | Select department 

$NewDepartment = Read-Host "Enter New Department"

Set-ADUser -Identity $x -Department $NewDepartment

2-#Automation Adding permissions to user due to working in 2 departments

##Copy New Permissions From another User
$UserWeNeedToCopyfrom = Read-Host "copy permission from: "
$MoveUser = Read-Host "to: "

Get-ADUser -Identity $UserWeNeedToCopyFrom -Properties memberof |
Select-Object -ExpandProperty memberof |
Add-ADGroupMember -Members $MoveUser


#change Department name

Get-ADUser $x -Properties * | Select department 

$NewDepartment = Read-Host "Enter New Department"

Set-ADUser -Identity $x -Department $NewDepartment

#End

3- Remove_AllGroups_AD_User
Import-Module ActiveDirectory
$employeeSAN = Read-Host "SamAccountName "


try{
	Get-ADUser -Identity $employeeSAN
	#if that doesn't throw you to the catch this person exists. So you can continue

	$ADgroups = Get-ADPrincipalGroupMembership -Identity $employeeSAN | where {$_.Name -ne "Domain Users"}
    $ADgroups | select name
	if ($ADgroups -ne $null){
		Remove-ADPrincipalGroupMembership -Identity $employeeSAN -MemberOf $ADgroups #-Confirm:$false
	}
}#end of try block
catch{
	Write-Host "$employeeSAN Is Not in AD Or Misspelled"
}#end of catch block


Import-Module ActiveDirectory
$employeeSAN = Read-Host "SamAccountName "


try{
	Get-ADUser -Identity $employeeSAN
	#if that doesn't throw you to the catch this person exists. So you can continue

	$ADgroups = Get-ADPrincipalGroupMembership -Identity $employeeSAN | where {$_.Name -ne "Domain Users"}
    $ADgroups | select name
	if ($ADgroups -ne $null){
		Remove-ADPrincipalGroupMembership -Identity $employeeSAN -MemberOf $ADgroups #-Confirm:$false
	}
}#end of try block
catch{
	Write-Host "$employeeSAN Is Not in AD Or Misspelled"
}#end of catch block


4-Remove_AllGroups_AD_User

Import-Module ActiveDirectory
$employeeSAN = Read-Host "SamAccountName "


try{
	Get-ADUser -Identity $employeeSAN
	#if that doesn't throw you to the catch this person exists. So you can continue

	$ADgroups = Get-ADPrincipalGroupMembership -Identity $employeeSAN | where {$_.Name -ne "Domain Users"}
    $ADgroups | select name
	if ($ADgroups -ne $null){
		Remove-ADPrincipalGroupMembership -Identity $employeeSAN -MemberOf $ADgroups #-Confirm:$false
	}
}#end of try block
catch{
	Write-Host "$employeeSAN Is Not in AD Or Misspelled"
}#end of catch block
