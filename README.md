# Adding the Password Reset role to a user

```powershell

$RoleGroupName = "Password Reset 01"
$UserToGrant = "samdrey"

New-RoleGroup $RoleGroupName
new-ManagementRoleAssignment -Role "Reset Password" -SecurityGroup $RoleGroupName

Add-RoleGroupMember $RoleGroupName -Member $UserToGrant



Get-ManagementRoleAssignment -GetEffectiveUsers | Where-Object {$_.EffectiveUserName -eq $UserToGrant} | select-object RoleAssigneeName,RoleAssigneeType,Role | ft -a


<# if you have issues createing the abaove, try the below #>

New-ManagementRoleAssignment -Role "reset password” –SecurityGroup $RoleGroupName -Name "Reset Password – Delegate”  –Delegating

Add-pssnapin microsoft*

Install-CannedRbacRoles
Install-CannedRbacRoleAssignments

```
