# Adding the Password Reset role to a user

```powershell

$RoleGroupName = "Password Reset 01"  # Or whatever you want to name your group
$UserToGrant = "UserName"   # Here put the user you want to grant the Reset Password to...

# First we create a new Role Group
New-RoleGroup $RoleGroupName

# Then we create a new Management Role Assignment
new-ManagementRoleAssignment -Role "Reset Password" -SecurityGroup $RoleGroupName

# And finally we add our user to this new Role Group
Add-RoleGroupMember $RoleGroupName -Member $UserToGrant


# To check if the user has this role granted through the above Group:
Get-ManagementRoleAssignment -GetEffectiveUsers | Where-Object {$_.EffectiveUserName -eq $UserToGrant} | select-object RoleAssigneeName,RoleAssigneeType,Role | ft -a


```

If you happen to have an error containg the below:

```
You must be assigned a delegating role assignment to the management role or its parent in the hierarchy without a scope restriction.
```

Then you can atry to repair the default RBAC roles using the below, and you will need to close and re-open your Powershell window/session.

```powershell

Add-pssnapin microsoft*

Install-CannedRbacRoles
Install-CannedRbacRoleAssignments

```
